A CDN starter template for [Wasmer Edge](https://wasmer.io/products/edge), served by [Static Web Server](https://github.com/static-web-server/static-web-server) with Wasmer Edge CDN Cache turned on.

> Follow the full guide in the [Wasmer docs](https://docs.wasmer.io/edge/guides/cdn/).

## What is inside

```text
app.yaml        Wasmer app config; enables CDN Cache
Staticfile      `root: public` tells the build which folder to serve
public/         everything here is served from the site root
  index.html    landing page
  favicon.ico   site icon
  image1.avif   AVIF, 1600 px on the long side, with image1.jpg as the JPEG fallback
  image1-800.*  800 px variants for small screens (srcset)
```

The images are AVIF with JPEG fallbacks, and each comes in two sizes. The page uses `<picture>`, `srcset`, `width`/`height`, and lazy loading, so browsers download only the smallest file they can use.

## Caching

Static Web Server adds a `Cache-Control` header to every response:

| Files | `Cache-Control` |
| --- | --- |
| `avif`, `bmp`, `gif`, `ico`, `jpeg`, `jpg`, `jxl`, `png`, `webp`, `css`, `js`, `mjs`, `map`, `woff`, `woff2`, `mp3`, `mp4`, `ogg`, `ogv`, `wav`, `weba`, `webm`, `pdf`, `doc`, `rtf`, `zip`, `gz`, `bz2`, `tar`, `tgz`, `rar`, `htc` | `max-age=31536000` (1 year) |
| `json`, `xml`, `rss`, `atom` | `max-age=3600` (1 hour) |
| Everything else, including `html`, `svg`, `ttf`, `otf` and `wasm` | `max-age=86400` (1 day) |

Wasmer Edge CDN Cache stores these responses at the edge. Each deploy starts with an empty cache, so a new version never serves old files from the edge.

Browsers keep these files for as long as `max-age` says, so plan file names:

- When you change a file, give it a new name (for example `logo.v2.avif`) and update the links to it, so returning visitors download the new file.
- A missing file gets the same header, so its `404` is also kept for a year. Deploy a file before you link to it.

## Run locally

Install Wasmer ([install guide](https://docs.wasmer.io/install)) and run the same server version that Wasmer Edge uses:

```bash
wasmer run wasmer/static-web-server@=1.1.0 --net --volume ./public:/public -- --root /public --port 8080
```

Open [http://localhost:8080](http://localhost:8080).

## Deploy on Wasmer Edge

```bash
wasmer deploy --build-remote
```

Wasmer builds the app from the `Staticfile` and the `public` folder. Run `wasmer deploy --build-remote` again after you add or change files.

Live example: https://cdn-wasmer-starter.wasmer.app/

## Check and purge the cache

Request a file twice and read the `x-cache-status` header. This example uses the live example app; for your own app, use its URL:

```bash
curl -s -o /dev/null -D - https://cdn-wasmer-starter.wasmer.app/image1.avif | grep -i x-cache-status
```

The first request is a `MISS`, and the next one from the same Edge node is a `HIT`. Each Edge node has its own cache.

Use a `GET` request, as above. A `HEAD` request (`curl -I`) can read the cache, but it does not fill it, so `HEAD` requests alone always show `MISS`.

To clear the cache of the current version:

```bash
wasmer app cdn purge
```

Read more in the [CDN Cache documentation](https://docs.wasmer.io/edge/learn/cdn-cache/).

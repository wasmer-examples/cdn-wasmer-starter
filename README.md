A CDN starter template using [Static Web Server](https://github.com/static-web-server/static-web-server).

> You can follow the full tutorial from [here](https://docs.wasmer.io/edge/tutorials/cdn)

## Usage

All the static files will be served from the `public` folder, and the static webserver will be configured using the `config.toml` file.

You can run the CDN template easily using Wasmer (check out the [install guide](https://docs.wasmer.io/install)):

```bash
wasmer run wasmer-examples/cdn-wasmer-starter --net
```

> [!TIP]
> You can also run `wasmer run . --net` in the root of this repo, after running `npm run build`

Open [http://localhost:8080](http://localhost:8080) with your browser to see the CDN.

## Deploy on Wasmer Edge

The easiest way to serve your public assets is to use the [Wasmer Edge](https://wasmer.io/products/edge) as your CDN.

Live example: https://cdn-wasmer-starter.wasmer.app/

Run this commmand to deploy to Wasmer Edge:

```bash
wasmer deploy
```

> [!NOTE]
> You will need to change the namespace in `wasmer.toml` to your own namespace and app name in `app.yaml` to your own app name.

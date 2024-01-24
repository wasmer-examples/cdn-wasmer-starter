A CDN starter template using [Static Web Server](https://github.com/static-web-server/static-web-server).

> You can follow the full tutorial from [here](https://docs.wasmer.io/edge/tutorials/cdn)

## Usage

You can add your static files to the `public` folder.

## Deploy on Wasmer Edge

The easiest way to serve your public assets is to use the [Wasmer Edge](https://wasmer.io/products/edge) as your CDN.

Live example: http://cdn-wasmer-starter.wasmer.app/

Run this commmand to deploy to Wasmer Edge:

```bash
wasmer deploy
```

> [!NOTE]
> You will need to change the namespace in `wasmer.toml` to your own namespace and app name in `app.yaml` to your own app name.

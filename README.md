# cdn-wasmer-starter

A CDN starter using Static Web Server. You can use this starter to deploy your static files/websites to the CDN. The CDN is powered by [Wasmer Edge](https://docs.wasmer.io/edge)

## Usage

### 1. Install the `wasmer` CLI

```bash
curl https://get.wasmer.io -sSfL | sh
```

### 2. Clone this repository

```bash
git clone https://github.com/wasmer-examples/cdn-wasmer-starter.git
```

### 3. Add your static files

You can add your static files to the `public` folder.

### 4. Deploy your static files to the CDN

```bash
wasmer deploy
```

You will get the CDN URL after the deployment and can access your static files from the CDN.

> You will need to change the namespace in `wasmer.toml` to your own namespace and app name in `app.yaml` to your own app name.

## Resources

You can learn the full tutorial from [here](https://docs.wasmer.io/edge/tutorials/cdn)

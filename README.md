# Cloudflare Workers Site Template

This repository contains a CI/CD-optimized Cloudflare Workers template written in TypeScript for serving static sites. It allows certain routes to be proxied so that all requests can be served under the same subdomain, and therefore avoids [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) issues and benefits from Cloudflare's ["under attack"](https://support.cloudflare.com/hc/en-us/articles/200170076-Understanding-Cloudflare-Under-Attack-mode-advanced-DDOS-protection-) DDoS protection mode.

The template is optimized for single page applications. Whenever a request hits a route where an asset cannot be found, a fallback to `index.html` is sent instead of a `404` error.

## Usage

The template is designed to be used by CI/CD pipelines. Such a pipeline shall first transform the website into static files, for example with a Webpack build; then it should clone this repository and replace content in the `public` folder with static files to be served.

Then, authenticate with cloudflare with the following command:

```sh
$ echo "${CLOUDFLARE_API_TOKEN}" | yarn wrangler config
```

Set the following environment variables:

- `CLOUDFLARE_WORKER_NAME`

  Name of the Cloudflare worker.

- `CLOUDFLARE_ACCOUNT_ID`

  Cloudflare account ID.

- `DOMAIN`

  Custom domain to be used for serving the website.

- `CLOUDFLARE_ZONE_ID`

  Cloudflare zone ID of the custom domain.

Finally, publish the site with:

```
$ yarn run publish
```

## License

[MIT](./LICENSE)

# Keen Kids website

Keen Kids, LLC’s public website provides [app support](https://www.keen.kids/support/) and the [privacy policy](https://www.keen.kids/privacy-policy/).

## Preview and publish

Start a local preview from the repository root.

```sh
python3 -m http.server 8000 --bind 127.0.0.1 --directory docs
```

Open [localhost:8000](http://localhost:8000/). Edit the static files in `docs/` and push to `main` to publish. GitHub Pages serves that directory directly. Cloudflare redirects requests for the bare domain and HTTP traffic to [www.keen.kids](https://www.keen.kids/), preserving paths and query strings.

## Local Cloudflare credentials

Previewing and publishing the website require no Cloudflare or R2 credentials. For DNS or redirect administration, create a private `.env` in the repository root on a new checkout.

```sh
test -e .env || install -m 600 .env.template .env
```

Set `CLOUDFLARE_ACCOUNT_ID` to the Keen account ID and `CLOUDFLARE_API_TOKEN` to a token with the permissions needed for the change. The optional `R2_ACCESS_KEY_ID`, `R2_SECRET_ACCESS_KEY`, and `R2_ENDPOINT_URL` fields are for S3-compatible storage tools if R2 is enabled.

Git ignores local `.env` files. Keep real values in the root `.env`, outside the published `docs/` directory. When adding a variable, commit its name with an empty value in [.env.template](.env.template).

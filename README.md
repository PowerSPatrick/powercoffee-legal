# powercoffee-legal

Static site hosting Terms of Use and Privacy Policy for the **Git-Integrated Markdown Editor** iOS app.

- Live: <https://legal.powercoffee.me/>
- Terms: <https://legal.powercoffee.me/terms/>
- Privacy: <https://legal.powercoffee.me/privacy/>

## How it's served

Cloudflare Pages project `powercoffee-legal`, custom domain `legal.powercoffee.me` (proxied through Cloudflare on the same account that owns the `powercoffee.me` zone). The site is plain HTML + CSS — no build step, no runtime.

## How to update content

1. Edit the relevant `index.html` (`/`, `/terms/`, or `/privacy/`) and bump the **Effective date** / **Last updated** / **Version** in the meta block.
2. Commit and push to `main`.
3. A GitHub Actions workflow at `.github/workflows/deploy.yml` deploys the site to Cloudflare Pages on every push to `main`.

If the workflow isn't configured (no `CLOUDFLARE_API_TOKEN` / `CLOUDFLARE_ACCOUNT_ID` secrets present), you can deploy manually from your machine:

```sh
wrangler login                                 # one-time, opens browser
wrangler pages deploy . --project-name=powercoffee-legal --branch=main
```

## Layout

```
.
├── index.html            # landing
├── terms/index.html      # EULA / Terms of Use
├── privacy/index.html    # Privacy Policy
├── styles.css            # shared styles
├── _headers              # Cloudflare Pages security headers
├── _redirects            # trailing-slash normalisation
└── .github/workflows/deploy.yml
```

## Security headers

Configured in `_headers`. Notable:

- `Content-Security-Policy: default-src 'none'; style-src 'self'; img-src 'self' data:; ...`
- `Strict-Transport-Security: max-age=31536000; includeSubDomains; preload`
- `X-Frame-Options: DENY`
- `X-Content-Type-Options: nosniff`
- `Referrer-Policy: strict-origin-when-cross-origin`
- `Permissions-Policy` denying all powerful features

## Contact

<hello@powercoffee.me>

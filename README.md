# Velkan Sector Tool

Single-page interactive sector-strategy brief.

- Canonical URL: <https://velkan-sector-tool.pages.dev/>
- Production host: Cloudflare Pages project `velkan-sector-tool`
- Deployment mode: Wrangler Direct Upload

## Deployment

The deployable artifact contains only `index.html`. Prepare an isolated directory
so repository metadata is not published:

```sh
PUBLISH_DIRECTORY="$(mktemp -d)"
cp index.html "$PUBLISH_DIRECTORY/"
```

Set `CLOUDFLARE_API_TOKEN` and `CLOUDFLARE_ACCOUNT_ID` from the 1Password
Employee-vault item `Cloudflare`, then deploy and remove the temporary directory:

```sh
npx --yes wrangler pages deploy "$PUBLISH_DIRECTORY" \
  --project-name velkan-sector-tool \
  --branch main \
  --commit-hash "$(git rev-parse HEAD)" \
  --commit-message "$(git log -1 --pretty=%s)"
rm -rf "$PUBLISH_DIRECTORY"
```

Do not re-enable GitHub Pages or add a GitHub Pages `CNAME` file. If deployment
is later automated in GitHub Actions, create a Pages-scoped Cloudflare token;
never reuse a broad DNS-capable credential.

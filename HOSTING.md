# Hosting: git-intermediate.rgtlab.org
*2026-07-25 19:46 PDT*

This repository renders with Quarto and deploys to Netlify
via GitHub Actions on every push to `main`. The workflow is
`.github/workflows/publish.yml`.

The push from the local machine creates the repository and
uploads the source. It does **not**, by itself, make
`https://git-intermediate.rgtlab.org` resolve. The remaining
steps below are one-time and must be done by a person with
Netlify access and control of the `rgtlab.org` DNS zone.

## One-time deployment setup

1. **Create the Netlify site.** In the Netlify dashboard, or
   with the CLI:

   ```bash
   netlify sites:create --name git-intermediate-rgtlab
   ```

   Note the site's API ID from the output.

2. **Set the GitHub Actions secrets** on this repository so
   the workflow can deploy:

   ```bash
   gh secret set NETLIFY_SITE_ID  --body '<site-api-id>'
   gh secret set NETLIFY_AUTH_TOKEN --body '<netlify-personal-access-token>'
   ```

   Generate the personal access token at
   Netlify > User settings > Applications > New access token.

3. **Point the subdomain at Netlify.** `rgtlab.org` is not on
   Netlify DNS, so add a CNAME at the DNS provider that hosts
   `rgtlab.org`:

   ```text
   git-intermediate   CNAME   <netlify-site>.netlify.app.
   ```

   Then add `git-intermediate.rgtlab.org` as a custom domain
   on the Netlify site so Netlify provisions the TLS
   certificate.

4. **Trigger the first deploy.** Either push a commit to
   `main` or run the workflow manually:

   ```bash
   gh workflow run 'Render and deploy to Netlify'
   ```

## Verifying

```bash
gh run list --workflow 'Render and deploy to Netlify'
gh run watch
```

Once the run succeeds and DNS has propagated, confirm:

```bash
curl -I https://git-intermediate.rgtlab.org
```

A `200` response confirms the site is live.

## Notes

- The workflow renders HTML only (`quarto render --to
  html`); the book contains no executable code chunks, so no
  R toolchain is installed on the runner. The PDF is built
  locally when needed and is not part of the deployed site.
- `_book/`, `*.html`, and `*.pdf` are git-ignored; the
  deployed site is built on the runner from source, not
  committed.

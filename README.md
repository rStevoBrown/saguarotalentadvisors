# saguarotalentadvisors.com — static site

Static mirror of https://saguarotalentadvisors.com (captured 2026-10-27), ready for GitHub Pages.
No build step: plain HTML + inline CSS, self-hosted fonts, one logo PNG.

```
index.html            /
about/index.html      /about
advisory/index.html   /advisory
hiring/index.html     /hiring
subscription/index.html /subscription
contact/index.html    /contact
assets/img/logo.png   logo (was base64-inlined twice on every page)
assets/fonts/         Playfair Display + Source Sans 3 (Google Fonts, SIL OFL 1.1), self-hosted
.nojekyll             serve files as-is
```

All internal links are relative, so the site works both at a custom domain root and at
`https://<user>.github.io/<repo>/`.

## Preview locally
    python3 -m http.server 8000   # then open http://localhost:8000/

## Known TODOs
- **Contact form** (`contact/index.html`) submits to Formspree (`https://formspree.io/f/xrppqwne`,
  free tier ~50 submissions/month) via `fetch`, with inline success/error messages and a hidden
  `_gotcha` honeypot field for spam. The first real submission triggers a Formspree email asking
  the form owner to confirm the form; submissions are only delivered after that confirmation.
  Fields: First Name*, Last Name*, Company*, Work Email*, Phone, Inquiry Type, Role, Message.
- **Netlify Forms do not work on GitHub Pages** (not used today anyway).

## Custom domain (not done yet)
1. Repo Settings → Pages → Source: deploy from branch `main` / root.
2. Add a file named `CNAME` containing `saguarotalentadvisors.com` (or set it in Settings → Pages,
   which commits it for you). Do this only when ready to cut over.
3. DNS (currently managed at Squarespace Domains):
   - apex `@` A records → 185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153
     (optional AAAA: 2606:50c0:8000::153, ...8001::153, ...8002::153, ...8003::153)
   - `www` CNAME → `<github-user>.github.io`
   - Remove the existing apex A `75.2.60.5` and `www` CNAME `verdant-pudding-3aef0e.netlify.app` (Netlify).
   - **Keep the Google Workspace MX records and the google-site-verification TXT** (email).
4. Tick "Enforce HTTPS" once the certificate is issued.

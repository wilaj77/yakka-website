# Yakka websites

Two static pages, one per domain. No build step, no dependencies — plain HTML with the
styles inline, so there is nothing to install and nothing that can break a deploy.

| Folder | Domain | Purpose |
|---|---|---|
| `yakkagroup/` | yakkagroup.com | Company page. **Apple requires this** for Developer Program Organization enrollment and rejects parked or placeholder pages. |
| `whispager/` | whispager.com | WhisPager product page. |

## Why this is a separate repository

The product repository is private and holds the architecture, the security design, the
message-encryption spec and the installer scripts. Hosting is configured by pointing a
service at a repository and naming a publish directory, and a mistyped publish directory
would put all of that on the public internet.

Keeping the public pages in their own public repository means that mistake is not available
to make. Nothing here is sensitive; everything here is meant to be read by strangers.

## Deploying (Render)

One static site per folder, both free — Render static sites are CDN-served, do not sleep,
and have no monthly cost. Only the owner console, which is a web service, is paid.

1. **New → Static Site**, connect this repository.
2. **Build command:** leave empty. **Publish directory:** `yakkagroup`.
3. **Settings → Custom Domain** → `yakkagroup.com` and `www.yakkagroup.com`. Render shows
   the DNS records to add at GoDaddy and issues the TLS certificate itself.
4. Repeat for `whispager` → `whispager.com`.

## whispager.app

Redirects to whispager.com; it serves no content of its own.

**If the redirect appears broken, suspect HSTS before DNS.** The entire `.app` TLD is on the
HSTS preload list, so browsers refuse plain HTTP to any `.app` address outright — whatever
answers has to do so over HTTPS, with a valid certificate, before a redirect ever happens.

## Editing

The pages are deliberately plain. `yakkagroup/` is kept broad on purpose: Yakka LLC holds
several unrelated ventures, and that page should not need rewriting whenever one of them
changes. It does need to stay **up** — Apple re-verifies at membership renewal, and a site
that has since vanished is what stalls a renewal.

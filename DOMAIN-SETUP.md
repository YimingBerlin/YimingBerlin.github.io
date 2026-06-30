# Pointing yimingliuecon.com at this GitHub Pages site

This guide moves your website off Weebly and onto **free** GitHub Pages hosting,
while keeping the domain **yimingliuecon.com**. Every fact below was verified
against official GitHub / Cloudflare / Porkbun / ICANN docs on 2026-06-30.

---

## First, the key reframe

**GitHub does not sell or hold domains.** You can't "transfer a domain to
GitHub." What you actually do is: keep your domain at *a* registrar, and point
its **DNS** at GitHub's servers. GitHub then hosts the site for free.

Two facts about your current setup (from WHOIS, 2026-06-30):

- The domain is registered at **Register.com / Network Solutions**, but it was
  set up *through Weebly*, so you most likely manage it from your **Square /
  Weebly dashboard** (Weebly is owned by Square/Block) — not a separate
  Register.com login.
- It **renews on 2026-08-22** (~7 weeks away). The website currently points to
  Weebly's server (`199.34.228.159`).

So you have two routes. Pick one:

| | Path 1 — DNS only | Path 2 — Transfer registrar (recommended) |
|---|---|---|
| What it does | Keep the domain where it is; just repoint DNS to GitHub | Move the domain to a cheap registrar (~$10–12/yr), then point DNS to GitHub |
| Speed | Live on your domain in a few hours | ~5–10 days for the transfer |
| Cost | Free now, but you still pay Register.com/Weebly's pricey renewal in Aug | ~$10–12/yr forever; drop Weebly entirely |
| Effort | Edit a few DNS records | Unlock + auth code + transfer, then DNS |

You can also do **Path 1 now** (get live fast) and **Path 2 later** (before
Aug 22, to cut cost) — you'd just redo the DNS records once at the new registrar.

---

## The GitHub Pages DNS values (used by both paths)

For the apex domain **yimingliuecon.com** — four **A** records:

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

…and four **AAAA** (IPv6) records:

```
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```

For **www.yimingliuecon.com** — one **CNAME** record pointing to:

```
yimingberlin.github.io
```

(Note: the CNAME target is your username `.github.io` with **no** repo name.)

**Do not** create a wildcard `*` record (takeover risk).

---

## Path 1 — DNS only (keep current registrar)

1. **Find where DNS is editable.** Log in at **squareup.com** (Dashboard →
   Online → Domains) and/or **weebly.com**. Whichever one lists
   yimingliuecon.com is where you edit DNS. (Your billing receipts also tell
   you: charges from Square/Weebly → managed there.)
2. In that dashboard's **DNS / Advanced records** area:
   - **Add** the four A records and four AAAA records above for the root/`@`.
   - **Add** the www CNAME → `yimingberlin.github.io`.
   - **Remove** the old A record pointing to Weebly (`199.34.228.159`) so it
     doesn't conflict.
3. In this repo on GitHub: **Settings → Pages → Custom domain**, type
   `yimingliuecon.com`, **Save**. (GitHub auto-adds a `CNAME` file to the repo —
   leave it.)
4. Wait for GitHub's DNS check to go green, then tick **Enforce HTTPS**
   (the box is greyed out until GitHub issues the free TLS certificate — can
   take a few minutes to a few hours).
5. Once it works, you can cancel your **Weebly website plan**. ⚠️ Cancelling the
   website does **not** cancel the domain — keep renewing the domain so you
   don't lose it.

DNS changes can take 24–48h to propagate worldwide.

---

## Path 2 — Transfer to a cheap registrar, then point DNS (recommended)

This drops Weebly/Register.com completely and cuts the domain to ~$10–12/yr.
**Porkbun** is the simplest; **Cloudflare** is ~$1 cheaper but has extra steps.

### Step 1 — Unlock the domain & get the auth code (you only)
In the **Square Dashboard**: Online → Domains → your domain → Manage →
turn **off** "Enable registrar lock." That generates the **auth / EPP code**
(also temporarily disables WHOIS privacy — normal). Copy the code; it's
case-sensitive, so **paste, never retype**.

(Legacy Weebly UI: Settings → Domains → your domain → Registrar Lock → Disable;
the EPP code shows on the same page.)

⚠️ **Do not edit the registrant name/email/address** right before transferring —
that triggers a fresh 60-day lock that would block the move past your Aug 22
renewal.

### Step 2 — Start the transfer at the new registrar (you only)

**Porkbun (simplest):** at porkbun.com, start a transfer, paste the auth code,
approve the confirmation email. Porkbun includes free DNS + free WHOIS privacy,
and the transfer adds 1 year (so your expiry becomes ~2027-08-22). After it
completes, add the GitHub Pages records (4 A + 4 AAAA + www CNAME) in Porkbun's
DNS panel.

**Cloudflare (cheapest, at-cost):** Cloudflare requires the domain to use
Cloudflare's nameservers *first*. So: (a) add the domain to Cloudflare as a
"Full" zone, recreate the GitHub Pages records there (set them to "DNS only" /
grey cloud), (b) change the nameservers at your current registrar to the
Cloudflare pair, (c) once the zone is active, go to Cloudflare → Registrar and
complete the transfer with the auth code. Requires: domain >60 days old, DNSSEC
off. A Cloudflare-registered domain can only use Cloudflare DNS.

### Step 3 — Attach the domain in GitHub
Same as Path 1, steps 3–4: Settings → Pages → Custom domain =
`yimingliuecon.com` → Save → Enforce HTTPS once the cert is ready.

---

## Timing & cautions (verified)

- **You have ~7 weeks** (expiry 2026-08-22) and a transfer takes ~5–10 days, so
  there's plenty of buffer — but **start now** if you choose Path 2; don't wait
  until August (transferring while near expiry is risky).
- **No need to pre-renew** at this distance from expiry; the transfer adds a year
  on top of your remaining time.
- The **60-day ICANN lock** still applies in 2026 (its removal was approved in
  2025 but isn't live yet) — so don't change registrant contact details before
  transferring.
- Request the **auth code early**; delivery can take anywhere from an hour to a
  few days depending on the backend.
- **Enforce HTTPS** can't be turned on until GitHub provisions the certificate;
  if the box stays greyed out, recheck your DNS records, wait, or Remove +
  re-add the custom domain in Settings → Pages to retry.
- If the auth code is rejected or the unlock option is missing (a known
  Weebly/Square quirk), call **Square support: 1-855-700-6000** (Mon–Fri,
  6am–6pm Pacific) to release the domain manually.

---

## What only you can do vs. what I can do

- **You:** create the repo, anything requiring your Square/Weebly or registrar
  login (DNS edits, unlock, auth code, transfer approval), and ticking the
  GitHub Pages settings (since the repo is under your account).
- **Me:** everything in the code/site, telling you the exact records to paste,
  and verifying with `dig` that your DNS is pointing correctly once you've made
  the change.

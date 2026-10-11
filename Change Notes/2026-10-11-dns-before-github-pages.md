# DNS records BEFORE switching to GitHub Pages (recorded 2026-10-11)

Where: Mweb Plesk > Websites & Domains > giantelevators.co.za > Hosting & DNS > DNS
(Login details are kept by Dene. They are deliberately not stored in this folder.)

## Original records (as they were)

| Host | Type | Value |
|---|---|---|
| giantelevators.co.za. | NS | wh-ns1.mweb.co.za. |
| giantelevators.co.za. | NS | wh-ns2.mweb.co.za. |
| _dmarc.giantelevators.co.za. | TXT | v=DMARC1; p=quarantine |
| www.giantelevators.co.za. | CNAME | giantelevators.co.za. |
| giantelevators.co.za. | MX (10) | mx10.mweb.co.za. |
| giantelevators.co.za. | TXT | v=spf1 v=spf1 include:spf1.mweb.co.za ~all |
| giantelevators.co.za. | A | 102.65.21.221 |
| ftp.giantelevators.co.za. | CNAME | giantelevators.co.za. |
| smtphop._domainkey.giantelevators.co.za. | CNAME | smtphop._domainkey.mweb.co.za. |

Old Mweb site: files in httpdocs, IP 102.65.21.221 (a one-page "Welcome to Giant Elevators" flyer). Still on the Mweb server, untouched.

## Changes planned

1. A record giantelevators.co.za: 102.65.21.221 -> 185.199.108.153
2. Add A records: 185.199.109.153, 185.199.110.153, 185.199.111.153
3. www CNAME: giantelevators.co.za. -> mnjbzgh6dw-debug.github.io
4. NOT touched: NS, MX, both TXT, smtphop._domainkey, ftp (email depends on these)

## How to revert

1. In the same DNS page, delete the three extra A records (185.199.109.153, .110.153, .111.153).
2. Edit the remaining A record back to 102.65.21.221.
3. Edit the www CNAME back to giantelevators.co.za.
4. Wait up to a few hours for DNS to settle. The old Mweb flyer site returns.
5. Optional: in GitHub repo Settings > Pages, remove the custom domain.

## Website code versions (git)

- dac06f1 = last version WITH the contact form (before the form was removed)
- 4c233e3 = form removed, Call / WhatsApp / Email cards under "Get started"

To go back to the form version: `git revert 4c233e3` then `git push`.
The form posted to a mailto: link, which browsers flag as "not secure".

## Edit screens captured before any change (screenshots saved in this folder)

- before-A-record-edit-screen.png
  Record type A, Domain name blank (the main domain), TTL blank, IP address 102.65.21.221
- before-www-CNAME-edit-screen.webp
  Record type CNAME, Domain name www, TTL blank, Canonical name giantelevators.co.za (trailing dot added by Plesk)

TTL was blank on both, meaning the Plesk default was in use. When reverting, leave TTL blank.

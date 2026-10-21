# Connect by Relco Digital: connect.raschident.com

Static site (plain HTML, CSS and JS) plus one serverless function, `api/contact.js`, that emails every contact form submission to **contact@raschident.com**.

## Deploy on Vercel

1. Put this folder in a Git repository (a new one, or a new branch) and import it in Vercel. Framework preset: **Other**. No build command, no output directory.
2. In **Project Settings > Environment Variables**, add the email settings (pick ONE option below).
3. Assign the domain `connect.raschident.com` to this project (your DNS already points at Vercel).
4. Redeploy, open `/contact.html`, send a test message.

> If `connect.raschident.com` currently serves your RELCO Media app from another Vercel project, deploy this as a separate project or branch first and check the preview URL before moving the domain, so nothing live is overwritten.

## Email settings

### Option A: Resend (recommended)
1. Create a free account at resend.com and add the domain `raschident.com` (Resend shows the DNS records; add them where your DNS is managed).
2. Create an API key.
3. Set in Vercel:

| Variable | Value |
|---|---|
| `RESEND_API_KEY` | your key |
| `MAIL_FROM` | `Connect Website <forms@raschident.com>` (any address on the verified domain) |

### Option B: SMTP with your own mailbox
| Variable | Value |
|---|---|
| `SMTP_HOST` | your mail server, e.g. `mail.raschident.com` |
| `SMTP_PORT` | `465` (SSL) or `587` |
| `SMTP_USER` | `contact@raschident.com` |
| `SMTP_PASS` | the mailbox password |
| `SMTP_FROM` | `Connect Website <contact@raschident.com>` |

### Optional
| Variable | Default | Purpose |
|---|---|---|
| `CONTACT_TO` | `contact@raschident.com` | where enquiries are delivered |
| `AUTO_REPLY` | on | set to `false` to stop the confirmation email to visitors |

## How the form works
- Visitor fills the form on `/contact.html` (also reachable as `?topic=audit|quote|order|team|general`).
- The browser posts JSON to `/api/contact`; the function validates it, blocks spam (hidden field, timing check, rate limit) and emails you.
- The email's **Reply-To** is the visitor's address, so you answer straight from your inbox.
- The visitor gets a short confirmation email.
- If delivery fails, the visitor sees a clear message with your email and WhatsApp.

## Files
- `*.html`: the pages. `assets/`: styles, script, favicon.
- `api/contact.js`: form handler. `vercel.json`: security headers. `sitemap.xml`, `robots.txt`.

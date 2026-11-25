# PulseFeed — Publishing Business Starter

A deployable Node.js RSS publishing site with:
- Responsive public homepage, category filters, search and headline-based trending topics.
- RSS/Atom ingestion and caching (refreshes every 5 minutes when requested).
- Admin login, RSS source management, original article drafts and publishing.
- Optional Gemini-powered summaries (server-side API key; never exposed to browsers).
- SEO basics: page metadata, canonical-ready homepage, robots.txt, sitemap.xml, story routes.
- Ad placement placeholder and ads.txt endpoint.

## 1. Run locally

Requirements: Node.js 20+.

```bash
npm install
cp .env.example .env
```

Set a strong `SESSION_SECRET` and `ADMIN_PASSWORD` in `.env`. Then:

```bash
npm start
```

Open `http://localhost:3000`. Admin: `http://localhost:3000/admin.html`.

## 2. Enable AI summaries (optional)

Create a Gemini API key in Google AI Studio. Set `GEMINI_API_KEY` in the server environment. Keep it private; do not put it in frontend JavaScript. The admin assistant summarizes only the headline/excerpt you supply. Human fact-checking is required.

## 3. Deploy

Deploy this Node app to a Node-capable host (for example Render, Railway, Fly.io or a VPS). Configure:
- `NODE_ENV=production`
- `SITE_URL=https://yourdomain.com`
- `SESSION_SECRET` (long random value)
- `ADMIN_PASSWORD` (unique strong password)
- optional `GEMINI_API_KEY`, `GEMINI_MODEL`

**Persistence note:** this starter stores feeds and posts as JSON files in `data/`. Your host must provide a persistent disk mounted to the project data directory, or replace JSON storage with a database before scaling. Do not use ephemeral storage for production editorial content. Use HTTPS. For multiple server instances, use a persistent session store instead of Express MemoryStore.

## 4. Custom domain

1. Register a domain with a registrar.
2. Add it to your hosting provider's custom-domain settings.
3. Copy the exact DNS records supplied by that host into your registrar.
4. Wait for DNS/SSL provisioning, then set `SITE_URL` to the HTTPS domain and redeploy.
5. Verify `/robots.txt` and `/sitemap.xml` work on the live domain.
6. Replace placeholder contact details and policy text.

## 5. AdSense

AdSense is **not active by default**. Before applying:
- Publish useful original content consistently; do not simply republish RSS headlines or scraped articles.
- Add real About, Contact, Privacy and Editorial Policy pages with accurate operator details.
- Ensure navigation works, the site is useful, and content complies with publisher and AdSense policies.
- Apply through Google AdSense. Approval is Google's decision, not guaranteed.
- After approval, add the official AdSense script and ad unit code to `public/index.html` / `public/styles.css`.
- Set `ADSENSE_CLIENT` to your publisher ID. Verify `/ads.txt` after deployment.

Never insert ads on third-party content pages unless you have appropriate rights and the page adds substantial original value.

## 6. Editorial and copyright safeguards

- Treat RSS as a discovery and referral layer. Keep attribution and link readers to the original publisher.
- Review each feed's terms of use and publisher permissions. Publicly accessible RSS does not automatically grant a licence to republish full articles, images or substantial excerpts.
- Do not scrape article bodies or copy images without permission.
- Use PulseFeed's own reporting, explainers, interviews and analysis as the core publishing product.
- Verify every factual claim, especially AI-assisted summaries. Clearly label opinion and sponsored content.
- Provide a working correction/removal contact and respond to publisher requests.

## 7. Before a real launch

This is a working starter, not a fully hardened newsroom CMS. Add a managed database, persistent session store, backups, role-based accounts, CSRF protection, audit logs, editorial review workflow, image rights tracking, analytics consent controls, and a tested privacy policy before operating at scale.

## Finalized PulseFeed brand configuration

- Brand: PulseFeed — Stories in Motion
- Positioning: fast discovery of trending stories from the Philippines and around the world.
- Audience: Philippines + international readers.
- Languages: English / Filipino interface toggle. Editors should label each article's language clearly.
- Design: energetic viral-trending news portal with dark editorial styling and bright accents.
- Suggested editorial mix: 50% Philippines, 25% world, 15% technology/business, 10% entertainment/lifestyle. Adjust using real audience analytics.
- Voice: clear, energetic and factual. Avoid misleading or sensational headlines.

## Domain name ideas (availability not checked)

- pulsefeed.ph
- pulsefeednews.com
- thepulsefeed.com
- pulsefeed.today

Check availability, renewal price and registrar terms before purchasing.

## Deployment checklist

1. Create a GitHub repository and upload this project.
2. Choose a Node.js hosting provider that supports persistent storage/volumes.
3. Deploy as a Node web service with start command `npm start`.
4. Mount persistent storage to the project `data/` directory. Posts and feeds must survive restarts.
5. Set `NODE_ENV=production`, `SITE_URL`, a long random `SESSION_SECRET`, and a unique strong `ADMIN_PASSWORD`.
6. Optionally set `GEMINI_API_KEY` and `GEMINI_MODEL=gemini-2.5-flash`.
7. Register a domain after checking availability; add the DNS records supplied by your host; enable HTTPS.
8. Replace placeholder contact details and review the Privacy and Editorial Policy pages.
9. Add a production session store, CSRF protection, backups and a database before scaling. Express's default in-memory session store is not suitable for production.
10. Publish original, useful articles consistently; apply for AdSense only when the site is complete and compliant. Approval is not guaranteed.

## Editorial and monetization safeguards

RSS is a discovery/referral layer: show attribution and link to original publishers. Public RSS availability does not automatically grant rights to republish full articles or images. Build the business around original reporting, explainers, interviews and commentary. Fact-check AI-assisted summaries. Add AdSense only after approval and use the official publisher code supplied by Google.

# Ideato outage and the move off Vercel (14 Nov 2026)

## What broke

On 14 Nov 2026 at 20:43 IST, Vercel paused Ideato's free (Hobby) account: "fair use limits exceeded" for fluid CPU time. www.ideato.social returned `402 DEPLOYMENT_DISABLED`, and so did the AI connector. Vercel would only lift the pause on 14 Dec.

Vercel's own usage numbers showed the cause. Around 97% of function time went to requests that hung until Vercel's timeout: 125 to 636 of them a day over the two weeks before, against about 0.3 to 1.4 GB-hours of normal work a day.

The main suspect was the MCP endpoint (`/api/mcp`), which AI connectors call. It's stateless, but it answered `GET` by opening a server-to-client stream that never sends anything, so every connected Claude session held one open until Vercel killed it.

## The fix

`GET /api/mcp` now returns `405 Method Not Allowed`, which the MCP spec allows for servers without a standalone stream. Clients fall back to POST only. Code: kamal0808/ideato#175 (#212).

## Where Ideato runs now

- A production build on our own small server, behind a Cloudflare Tunnel (free), with DNS on Cloudflare.
- Auto-deploy: every 3 minutes the server checks `master`, builds any new commit in a separate folder, and switches the live site only if the build passes. A failed build leaves the site as it was (#214).
- Background jobs (Inngest) were re-pointed to the new address.

## Next home: Cloudflare

- We compared credit programmes for a bootstrapped startup: Cloudflare for Startups ($10k for one year, no funding needed), Google for Startups Start ($2k), AWS Activate Founders ($1k to $5k), Oracle Always Free, DigitalOcean Hatch (paused) and Microsoft for Startups (stuck in support). The full memo, every claim sourced: https://github.com/kamal0808/topc/blob/master/ecosystem/research/cloud-credits.md (topc-social/topc-tasks#286)
- We applied to Cloudflare for Startups on 14 Nov (topc-social/topc-tasks#111).
- Ideato builds and runs on Cloudflare Workers through OpenNext in a local test, at 6.2 MiB gzipped. Two fixes are needed before moving: Next.js 16.4.5 or later, and a User-Agent header on GitHub API calls, because Workers sends none and GitHub refuses requests without one (#213).

## Dead ends

- The free Cloudflare Workers plan can't run Ideato: it allows 10 ms of CPU per request, less than a server-rendered page needs.
- A frontend on Cloudflare with a backend elsewhere doesn't fit: Ideato renders its pages on the server, so splitting it would mean a rewrite.

## Tasks

- #212 Bring Ideato prod back (accepted)
- #213 Check Ideato on Cloudflare Workers (accepted)
- #214 Auto-deploy master to prod (closed)
- topc-social/topc-tasks#286 Cloud credits comparison (accepted)
- topc-social/topc-tasks#111 Cloudflare for Startups application (waiting on Cloudflare)

# Who would pay for Ideato?

Task: [#180](https://github.com/topc-social/ideato-tasks/issues/180). Done 2026-10-25 from read-only queries on Ideato's prod database (shared with Founderbot), GitHub activity across `topc-social`, and Kamal's notes on the people he's onboarded. Kamal's two accounts and the review test account are left out of "other people" counts. Founderbot users' chats are private, so they're described by kind of business only.

## Short answer

Nobody has paid for Ideato or Founderbot yet, and almost nobody besides Kamal uses Ideato. The data can't name a payer. It does show one group with a concrete, money-shaped need: **people running or starting a small business who need a specific person or job done**. That's the one to test first.

## What people actually did

| Who / group | What they did | What they asked for | Source |
|---|---|---|---|
| Everyone (54 profiles, Oct 2025 – Oct 2026) | 123 ideas, 32 comments, 19 projects | – | `profiles`, `ideas`, `comments`, `ideato_projects` |
| Kamal | 107 of 123 ideas, 31 of 32 comments, 17 of 19 projects, all 17 "want / have this problem / would pay" signals, all 9 joins on other people's ideas | – | `ideas`, `comments`, `idea_signals`, `idea_contributors` |
| 9 other people | 16 ideas between them (Satsidha 6, Shivang 3, one each from Pulkit, Rory, Aditya, Intesar, Himanshu, anshul, and one who goes by "Some") | Mostly consumer apps and civic causes (haircut app, ITR filing, women's safety, government accountability, commuting) | `ideas` |
| Same 9 | 1 comment, 0 joins on anyone else's idea, 0 signals | – | `comments`, `idea_contributors`, `idea_signals` |
| Satsidha | Started the only project not owned by Kamal (AccuGov) | – | `ideato_projects` |
| anshul (joined 2026-10-24) | Posted one idea | "We are working as a traditional business of produce distribution and looking for guidance from a person in this industry" ([idea](https://www.ideato.social/idea/283dab09-f4a1-4723-bf6e-d997c958dd38)) | `ideas` |
| Logged-out visitors | 34 idea views; 9 other signed-in people viewed 52 | – | `idea_views` |
| Invites | 14 sent on 2026-10-19 and 2026-10-24, 3 opened, 0 joined through the invite page | – | `invites` |
| Other people's work in the tasks repos | 0 issues, 0 comments by anyone but Kamal or the Ideato bot. Ledger rows for others: Inas (named Neki, 1,000), Intesar (named Gomitai, 1,000), Sayan (Apple developer account for Profiley, 792) | – | GitHub API, every `LEDGER.md` in `topc-social` |
| Inas, Intesar, Khushboo, Sayan | Friends and family Kamal brought in by hand on WhatsApp or in person. Khushboo took the GST task (topc-tasks#63) | Khushboo: "Ideato should explain itself", since she only got it because Kamal told her (ideato-tasks#164). Sayan: would co-found 50-50, not work for Neki | Kamal's notes; decisions log 2026-10-10 |
| Founderbot users (33 people besides Kamal, Dec 2025 – Sep 2026) | Most sent 1 or 2 messages. Deeper chats (14–48 messages) were about a health product, a voiceover-video product, a bag brand and a website review | Private ideas, mostly **small service businesses**: a visa service, SOX compliance services, moving actuarial Excel models to Python as a service, a hospital, a shilajit brand, an e-commerce store | `projects`, `project_chat_sessions`, `project_chat_messages` |
| Paying | 0 paid subscriptions ever (Kamal's own "pro" row has no payment attached). Pro waitlist: 1 entry, Kamal | – | `subscriptions`, `pro_waitlist` |

## What this says

- **Ideato has no outside usage to read a payer from yet.** Outside Kamal: 16 ideas, 1 comment, 0 joins, 0 accepted hand-ins from strangers. Some of those posters are friends trying it out (decisions log, Kamal's note 2026-10-07), so even the 16 aren't all demand.
- **Founderbot drew cold people, and they came with businesses, not hobby apps.** They wanted to talk their idea through in private, not build in public (Kamal, 2026-10-23). With a paid plan available, none of them paid.
- **The one cold Ideato post with a clear need asks for a person**, not a tool: someone who knows produce distribution. Whether anshul is a friend or a cold user isn't known; ask Kamal before counting it.
- **Every hand-in by someone else came from a personal ask** (WhatsApp, in person). Nobody has picked up a task from the board on their own.

## Candidate payers

**1. Small businesses that need a specific person or job.** They pay per match or per job; Ideato takes a cut.
- For: anshul's post; Founderbot's cold signups were mostly service businesses; "find someone who's done this" is something people already pay for (consultants, freelancers); fits "people find each other and agree how they'll work" (decisions 2026-10-15).
- Against: one post, not confirmed cold; Founderbot's paywall turned none of them into payers; Ideato would be up against Upwork, LinkedIn and plain WhatsApp referrals.

**2. Builders who want a team (subscription).** Founders pay to find co-builders and run a project in public.
- For: it's what Ideato is built for; Kamal and Sayan built the same thing alone without ever talking (2026-10-10).
- Against: the strongest data here. 0 joins on anyone else's idea, 0 invites converted, 0 paid Founderbot plans, and the one co-founder pair (Kamal and Sayan) set up by hand. These builders mostly have no money to spend (Kamal's own case included).

**3. Grants and programmes paying for Ideato as public good.** Not a customer, but money in, and first on Kamal's list (2026-10-25).
- For: no dilution; collaboration, jobs and skills are what many grants fund.
- Against: grant forms ask for traction and a customer, which is the gap this memo found. It needs a Pvt Ltd and DPIIT recognition first.

## Recommendation

Test candidate 1 first, by hand, before building anything.

Cheapest test: Kamal (or a `role:people` task) messages anshul and 5 of the Founderbot signups with a concrete business (they're Founderbot has their sign-in emails). Offer one thing: "I'll find you someone who has done this, from the people on Ideato, for ₹X if the intro is useful." Count how many say yes and how many pay. One payer is a signal; zero after 6 real asks means move on to the next candidate.

What this memo couldn't check: who among the posters is a friend; WhatsApp group activity (no read access; needs a chat export); PostHog traffic for ideato.social.

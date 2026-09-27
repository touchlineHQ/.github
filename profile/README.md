# touchlineHQ

**White-label websites and club tools for grassroots football.**

We build the digital stack a volunteer-run club actually needs: a site that looks like the club, fixtures that stay current, payments that treasurers can send from a phone, and publication rules that match the FA's U11 guidance rather than fighting it.

- Marketing site: [touchlinehq.co.uk](https://touchlinehq.co.uk)
- Club platform: [clubs.touchlinehq.co.uk](https://clubs.touchlinehq.co.uk)
- Fixture feeds & calendars: [fixtures.touchlinehq.co.uk](https://fixtures.touchlinehq.co.uk)

---

## What we ship

| Repo | What it is |
| --- | --- |
| [clubsPlatform](https://github.com/touchlineHQ/clubsPlatform) | White-label club websites. Single-club fork or multi-club platform on Cloudflare Pages + D1. Club colours, teams, news, registration, matchday info, admin panel, pitch bookings, and encrypted API secrets. |
| [touchlineHQ](https://github.com/touchlineHQ/touchlineHQ) | Marketing site for the platform, plus the Treasurer's Tool for GoCardless Direct Debit sign-up with player-specific payment references. |
| [fulltimeFeeds](https://github.com/touchlineHQ/fulltimeFeeds) | Daily FA Full-Time scrapes published as per-team `.ics` calendars and JSON feeds. Restricted U11-and-below data is redacted at source. |

---

## How the pieces fit

```text
FA Full-Time
     |
     v
fulltimeFeeds  -->  .ics calendars + JSON feeds
     |
     v
clubsPlatform / touchlineHQ  -->  club sites, fixtures, results, calendars
     |
     v
GoCardless  -->  Treasurer's Tool subscriptions
```

Youth football publication is treated as a product rule, not a display tweak. Results, opposition names, venues, and form are withheld for U11 and below. The match still appears as played — a blank season looks like a bug and tells a parent nothing.

---

## Stack

React, TypeScript, Vite, Mantine, Cloudflare Pages / Functions / D1, better-auth, GoCardless, PostHog.

---

## Working in this org

- Default branch is `main`.
- Typecheck and tests run on pull requests; they gate production on `clubsPlatform`.
- Do not commit secrets. GoCardless and encryption keys live in Cloudflare, not in the repo.
- Player identity stays a blind asset (`fanId`). Contact emails are direct PII — see `docs/DATA_PROTECTION.md` in `clubsPlatform`.
- Keep `website/src/utils/compliance.ts` (sites) and `scraper/compliance.py` (feeds) in step.

Questions or a club that needs a site: open an issue on the relevant repo, or start from [touchlinehq.co.uk](https://touchlinehq.co.uk).

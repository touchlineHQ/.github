# touchlineHQ

**Whitelabelled websites and club tools for grassroots football.**

We build the kit a volunteer-run club actually needs: a site that looks like the club, fixtures that stay current, payments a treasurer can send from a phone, and publication rules that follow the FA's U11 guidance rather than fight it.

- Marketing site: [touchlinehq.co.uk](https://touchlinehq.co.uk)
- Club platform: [clubs.touchlinehq.co.uk](https://clubs.touchlinehq.co.uk)
- Fixture feeds and calendars: [fixtures.touchlinehq.co.uk](https://fixtures.touchlinehq.co.uk)

---

## What we build

| Repository | What it is |
| --- | --- |
| [clubsPlatform](https://github.com/touchlineHQ/clubsPlatform) | Whitelabelled club websites. A single-club fork or a multi-club platform on Cloudflare Pages and D1. Club colours, teams, news, registration, matchday information, an admin panel, pitch bookings, and encrypted API secrets. |
| [touchlineHQ](https://github.com/touchlineHQ/touchlineHQ) | Marketing site for the platform, plus the Treasurer's Tool for GoCardless Direct Debit set-up with player-specific payment references. |
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

Youth football publication is treated as a product rule, not a display tweak. Results, opposition names, venues and form are withheld for U11 and below. The match still appears as played — a blank season looks like a bug and tells a parent nothing.

---

## Stack

React, TypeScript, Vite, Mantine, Cloudflare Pages / Functions / D1, better-auth, GoCardless, PostHog.

---

## Working in this organisation

- The default branch is `main`.
- Type-checking and tests run on pull requests; they must pass before production on `clubsPlatform`.
- Do not commit secrets. GoCardless and encryption keys live in Cloudflare, not in the repository.
- Player identity stays a blind asset (`fanId`). Contact emails are personal data — see `docs/DATA_PROTECTION.md` in `clubsPlatform`.
- Keep `website/src/utils/compliance.ts` (sites) and `scraper/compliance.py` (feeds) in step.

Questions, or a club that needs a site: open an issue on the relevant repository, or start from [touchlinehq.co.uk](https://touchlinehq.co.uk).

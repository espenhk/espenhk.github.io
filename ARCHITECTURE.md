# How the espenhk repos fit together

The single map of the personal repos. Each repo's CLAUDE.md / AGENTS.md
links here; keep this file current when a repo's role or its publishing changes.

## Repos

| Repo | What it is | Publishes to | Who writes to it |
|---|---|---|---|
| `espenhk.github.io` | Landing page: lists every public repo with Pages on (GitHub API, in the browser) | `espenhk.github.io/` (its own Pages) | you |
| `espenhk-portfolio` | Portfolio / CV (React, Lovable, Supabase CMS) | `espen.hk` via Lovable, not GitHub Pages | you, Lovable |
| `espenhk-hobby-projects` | Independent hobby projects, shared Poetry env | `espenhk.github.io/espenhk-hobby-projects/` from `docs/` | you; CI bot for `docs/football-scheduler/` until #130 below |
| `espenhk-skills` (private) | Claude skills; CI builds one ZIP per skill, installed by hand in the Claude app | nothing | you |
| `brann-away` | Encrypted output of the `brann-away-trip` skill: no code, no CI | `espenhk.github.io/brann-away/` from the repo root | **only** the `brann-away-trip` skill |

```
   espenhk.github.io ── lists ──►  every public repo with Pages on
          ▲                         ├─ espenhk.github.io/brann-away/
          │ linked from             └─ espenhk.github.io/espenhk-hobby-projects/
   espen.hk (portfolio)
     repo list marks repos with a live page

   espenhk-skills/brann-away-trip ── renders, encrypts, pushes ──► brann-away
   Claude Design systems ── synced one way ──► repos that use them
     Starfleet → portfolio (more consumers planned)
     Bortebane → brann-away-trip templates
```

## Rules

1. **Each repo deploys only itself.** No workflow commits into another repo.
   Generated output isn't committed: build it in CI and deploy with Actions.
   *Exception:* the hobby repo's football-scheduler report, until it moves out.
2. **One cross-repo writer, on purpose:** the `brann-away-trip` skill pushes
   to `brann-away`, a content-only repo. Nothing else writes there, and
   it's never edited by hand. Its pages embed their own trip data, so
   template changes reach them with a re-render (see the skill's
   `references/publish.md`), not by re-planning trips.
3. **Design systems live in Claude Design**, not in any repo. A repo that uses
   one commits a verbatim `tokens.json` plus generated `tokens.css`, with a test
   that fails on drift, and pulls updates itself. No repo reads tokens from
   another repo.
4. **Two sites, two jobs.** `espen.hk` presents all your work, most of which
   has no frontend. `espenhk.github.io` indexes only the repos that do. The
   portfolio marks repos with a live page and links to the index.
   A repo with the `unlisted` topic is hidden from both.

## Live URL rule

A repo's live page is its GitHub **Website** field if set, otherwise
`https://espenhk.github.io/<repo>/`. Both the index and the portfolio use
this rule, so they always agree.

## In progress

- Move `football-scheduler` into its own repo, deployed with Actions:
  [espenhk-hobby-projects#130](https://github.com/espenhk/espenhk-hobby-projects/issues/130).
- Shared `design-sync` skill for pulling Claude Design systems into the other repos:
  [espenhk-skills#34](https://github.com/espenhk/espenhk-skills/issues/34).
- Starfleet tokens in the portfolio:
  [espenhk-portfolio#4](https://github.com/espenhk/espenhk-portfolio/pull/4).

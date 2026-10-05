# Project instructions

## Project

Celestia 2 — an *Equestria at War* (EaW) total conversion for Victoria 2 /
Project Alice. Work is done region by region (see the region plan below).

- Working tree (git): `D:\celestia_2_dev`
- Engine / game: `E:\game\Project Alice`; the mod is synced to
  `E:\game\Project Alice\mod\celestia_2_dev`
- Build: `D:\mysql_temp\opencode\build_c2_scenario.ps1 -Out <name>`; the report
  is `%LOCALAPPDATA%\Project Alice\scenario_errors.txt` and its **Errors**
  section must be empty.
- Scenario start: 932.1.1 (timeline 932–1032).

## Work tracking

The living progress log is **`docs/C2_PROGRESS.md`** (local only, since `docs/`
is gitignored). Update it at the end of every session — status, completed-work
log, and open items — and mirror the key points here.

Roadmap docs (local): `docs/C2_REGION_REFINEMENT_PLAN.md` (region plan),
`docs/C2_OPENING_SETUP.md` (opening situation), `docs/C2_PLAYABILITY_PLAN.md`,
`docs/C2_AI_DIPLOMACY_INVESTIGATION.md` and
`docs/C2_AI_AGGRESSION_INVESTIGATION.md` (AI diplomacy / war proneness).

Region order: 1) Equus — Equestria + dependencies + Olenia + Changelings;
2) the Griffonian Empire sphere; 3) the Riverlands; 4) northern Zebrica +
thestrals.

**Current state:** region 1 is in progress. Equestria's southern content
(frontier decisions, the "Until the Southern Sea" war, the SPCAC decision) and
the Changeling unification (CHN as a formable pan-changeling tag, `union = CHN`)
are implemented and build clean, as is the CHN–Equestria "Acornage Boundary
Agreement"; they still need in-game verification. The `ASS` tag was corrected
from a donkey nation to a changeling hive. An AI war-proneness investigation is
done (`docs/C2_AI_AGGRESSION_INVESTIGATION.md`): PA has no per-nation
aggression and its declaration threshold (`best_difference = 2.0f`) is
hard-coded. Data-side tuning is partially applied (2026-10-05): truce 60
months incl. white peace, fabricated-CB validity 12 months, crisis chance 0,
and `EQS_southern_sea`/`free_peoples` are no longer fabricable; an engine patch
for a 4.0 threshold is pending a decision.

Key gotchas (full list in `docs/C2_PROGRESS.md` §6):

- `change_tag = TAG` preserves the former country's primary culture; the
  `= culture` form instead adopts the cultural union.
- The changeling culture group's real culture keys are `boreal`, `brackish`,
  `greneclyf`; the `*_changeling` names are race labels, not culture keys.
- In country-history files, accepted cultures use `culture = <c>`;
  `add_accepted_culture` is invalid there.
- Cultural unions are declared with `union = TAG` in `common/cultures.txt`.
- PA ignores the CB `is_triggered_only` flag (the AI can fabricate those CBs
  unless `constructing_cb = no` is set), and a white peace grants only
  `BASE_TRUCE_MONTHS` of truce (c2: 60 since 2026-10-05).
- Always build with 0 Errors and sync to the game dir before committing.

## Git commits

- Write all commit messages in English.
- Split unrelated work into separate commits; one topic per commit.
- Keep messages short: a concise subject, a short body only when needed, and a
  `Footer:` line of at most 50 words summarizing the key outcome.

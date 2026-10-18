# Huang Feng · Pixel Character Sheet

A single-page pixel character sheet built with static React + TypeScript + Vite. This is the redesigned sheet for Huang Feng.

A complete character companion for Huang Feng (黄蜂), a **level 9 Lightfoot Halfling Savant / Philosopher, Spy**. Exploration and combat share a persistent save. No game server, API key, analytics, external font request, or runtime network service is required. The GitHub Pages website is public. Your session saves stay in your browser; no character saves are uploaded to GitHub.

## Start locally

Use Node.js 22.12+ or 24 and pnpm 11.25.0. From this folder:

```sh
corepack enable
corepack prepare pnpm@11.25.0 --activate
pnpm install --frozen-lockfile
pnpm dev
```

Open the URL printed by Vite. For production:

```sh
pnpm test
pnpm build
pnpm preview
```

`dist/` is the complete production website. Serve it through HTTP/HTTPS; opening `index.html` directly with `file://` does not support module loading or PWA installation. The shipped build uses relative paths (`./`). This repository contains source and an example starting save. GitHub Actions creates and publishes the production build; generated output and local QA artifacts are ignored.

## Use at the table

Everything is on **one continuous character sheet**, with no page tabs or separate screens. Pixel fonts, stepped frames, block icons, dithered backgrounds, pixel dice and the supplied six-pose character art are bundled locally for offline use.

- **Identity & vitals:** name, class, race, background, AC, speed, PB, Intellect die, DC, HP/temp HP, Hit Dice, item resources and tattoo status.
- **Abilities, skills & saves:** six ability checks, six saving throws and all 18 skill checks are directly on the sheet. Situational Brave and extraplanar communication checkboxes are explicit.
- **Attacks, actions & reactions:** confirm hits before damage or ink. Choose Focus/other inside each attack. Enemy saves are resolved by the DM. Start My Turn/Next Round prepare two reactions. New creature’s turn refreshes only Studied Strike.
- **Compact popups:** Manage HP, attacks, abilities, rests, conditions, history, Focus and confirmations all dock in the lower-right on displays at least 768px wide and 540px high, without blocking the sheet. Phones, including short landscape displays, keep a modal dialog. Long popup contents scroll inside their own window, capped at620px tall. Optional Focus facts and notes expand inside the window; Cancel/Escape leaves the saved Focus unchanged.
- **Focus & effects:** persistent Focus facts, notes, Deduction, conditions and confirmed target effects stay on the same page. End Combat changes the mode without restoring or clearing resources.
- **Features, equipment & character bonds:** start collapsed; click or use Enter/Space on each heading to expand. Biography and contacts live under Character bonds. Session notes stay directly accessible on the sheet.
- **Phone quick controls:** Roll / Turn, Actions, Focus, Notes and Edit jump to the relevant sheet section or perform the labelled game action. They never swap pages.
- **Portraits:** all six supplied poses are selectable for exploration. Initiative uses the supplied fighting pose. Low HP and Frightened use the corresponding supplied poses. These choices do not alter game resources.
- **Edit & backup:** expands inline at the foot of the sheet. Ability edits, GM overrides, import preview, export, installation and offline status remain available. The schema-v1 character save is unchanged, so the redesign preserves existing character data.

## Rests, items and time

Every rest/dawn dialog shows the exact before/after resources and requires confirmation. Cancelling spends nothing and does not record preview dice.

| Command | Changes |
| --- | --- |
| Short Rest | Choose available Hit Dice; each rolls d8 + current CON. Heal to max; subtract dice spent. No item/tattoo recovery. |
| Long Rest | HP to max, up to 4 Hit Dice recovered (cap 9), Robes to 5, Deduction to 1; death-save counters reset. Standard temporary HP expire. |
| Dawn | Roll d4 ink recovery, cap 4. Nothing else recharges. |
| Start My Turn / Next Round | Two reactions and Studied Strike available; no healing or charge recovery. |
| End Combat | Exploration mode only. |

Longstrider is single-use, no concentration, and is blocked from casting while Focus is active. It remains consumed on rests and reloads. Its in-game minute counter changes only with the explicit Advance Time controls or a manual edit. Rest buttons intentionally do not infer elapsed spell/effect time; after an eight-hour rest, explicitly advance/expire any remaining one-hour Longstrider effect. Target effect durations and condition expiry are also manual, with recorded rules and confirmed removal flows. The rope has separate bonus-action release and target-action escape-check flows.

The ordinary 2014 temporary-HP rule is applied at long rest; a source-specific duration can be corrected in Settings. See [2014 Basic Rules: Combat](https://www.dndbeyond.com/sources/dnd/basic-rules-2014/combat#TemporaryHitPoints).

## Moving from the previous hosted URL

Before switching, open the old site and choose **Export Character Save**. On the GitHub Pages site, expand **Edit sheet, rules & backup**, import that JSON, inspect the preview, and confirm the overwrite. The URLs use separate browser storage, so your HP, charges and journal do not transfer automatically. Keep the backup until you have checked the new save.

## Save reliability and backups

- Versioned localStorage key: **`huang-feng-v1`**, schema version **1**. Every confirmed mutation is synchronously written, including rolls, resources, notes, Focus, effects, reactions, initiative and mode. There is no midnight or wall-clock resource reset.
- Each browser/device/origin has its own data. Safari, an installed home-screen app, another browser and another domain can have separate storage. Browser clearing, private browsing, storage eviction or device loss can remove local data.
- **Export Character Save** downloads readable JSON. Keep a copy outside the browser after each session. A reminder and quick export control are always available.
- **Import Save** validates structure, types, bounded resources, known schema, roll totals and override keys. It presents a preview and requires overwrite confirmation. Export the current character first if needed.
- `examples/huang-feng-canon-level-9.json` is a valid clean starting save, not a record of your campaign.
- Unknown/corrupt saves are never silently overwritten. A recovery banner offers the original raw data for download; explicitly import a valid backup or confirm using the in-memory character. Write failures are visible and advise export.
- Another tab changing the save produces a reload warning. Use one tab for live play and reload the latest save before editing in another.
- Migration supports this schema and a narrow pre-release v0 `{ schemaVersion: 0, hp, notes }` shape. Future unknown versions are refused rather than guessed. Upgrades that change the schema must add an explicit migration.
- Roll history retains the newest **500** entries. Clear History has confirmation.

## Dice engine

All rolls use `src/dice.ts`: typed roll kinds, die sizes, modes, labelled components, modifiers, raw rolls, kept/dropped dice, Lucky replacements, timestamps and final totals.

Web Crypto uses rejection sampling of 32-bit unsigned integers to avoid modulo bias. Only when Web Crypto is unavailable is `Math.random` used, visibly identified in roll history. Lucky applies once to each initial d20 showing 1 for attacks, checks, saves and initiative. It never cascades and never applies to damage or healing. It can be declined in settings. Advantage/disadvantage selects the kept d20 after any Lucky replacements.

Only an attack natural 20 produces a critical-hit indicator. Damage doubles the weapon and eligible Studied Strike dice, not fixed bonuses. Checks do not automatically succeed or fail; an optional DM natural-20/1 setting displays a ruling reminder while retaining the numeric total. Multiple Intellect Dice added to the same check apply only the highest; the canonical Words of Power damage is the sum of two d8s.

Dice use distinct pixel polyhedral silhouettes for d4, d6, d8, d10, d12 and d20, with a CSS tumble. The transient roll popup hides after five seconds; a new roll restarts that timer. Time in an open game dialog does not consume the popup timer, and dialog results stay visible for confirmation. Results remain in Recent roll and saved history.

Dice animate in CSS; exploration/combat swaps use the same supplied six-pose character reference, copied unchanged and clipped only at display time. Reduced-motion preferences disable the animation. Optional quiet synthesized dice sound is muted by default.

## Source precedence and attribution

1. `Huang_Feng_Level_0_to_10.txt`, compiled 18 October 2026: selected progression, current totals and explicit GM modifications. **Step 10 is equipment, not character level 10.**
2. Supplied laserllama **Savant v5.6.1** and **Savant: Expanded v5.6.1** PDFs for unchanged class rules: [Savant](https://www.gmbinder.com/share/-M0ZVK6ndhFyImQPF_aJ), [Expanded](https://www.gmbinder.com/share/-MzD8t8Wt2S232M_WBVC).
3. 2014 D&D rules / the specified Tasha’s options / official selected-item rules where unchanged.
4. Supplied `Huang_Feng_3_Pages.pdf` for visual reference only. The original portrait crops and app icon came from its embedded images. The redesigned sheet uses the additional six-pose image supplied in chat. None of the decorative sheets’ conflicting attack/item rules were imported into the UI.

Original PDF/TXT reference files were read without modification and are not bundled here. The supplied six-pose PNG is bundled unchanged as an app asset. All interactive rules and labels are selectable HTML text. Application code is separate from the supplied art and game rules; third-party packages retain their licenses.

## DM decisions and deliberate manual controls

- **Deduction + incapacitation:** default preserves Focus, following the selected TXT instruction. A clearly labelled setting can end Focus when an incapacitating condition is confirmed. Keen Awareness, Sharp Mind and reactions are suspended as appropriate. This is the remaining interaction to confirm with the DM.
- **Physical Thieves’ Tools / Dragonchess set:** proficiency is known; possession is not assumed. Inventory flags this for confirmation.
- **Quick Study:** choose one temporary skill or record a tool/language after one hour with an example. Only exact skill selections automatically add PB; for the custom entry, use the tool roller only when it really is a proficient tool, not a language.
- **Longstrider recipient:** the dedicated speed timer assumes self-casting. A different touched recipient should be recorded in notes and tracked manually.
- **Item loadout:** canonical three attunements are Robes, Rapier and Boots. If removed/changed by the DM, record it and adjust fixed totals/settings. Item caps remain the selected level-9 caps (Robes 5, ink 4).
- **Enemy stats and outcomes:** always supplied by the DM; no monster data, hidden save modifiers or adventure spoilers. Focus facts remain blank until recorded.
- **Combat economy:** no Extra Attack, level-10 damage support, free Flourish movement or Flourish counterattack. Reaction/resource limits and Studied Strike are tracked; general action/bonus-action legality, ammunition, distance, line of sight, hearing, concentration and effect expiry remain player/DM decisions.

## GitHub Pages

This copy is prepared for GitHub Pages. The included workflow builds and tests the app, then publishes the static `dist/` output on every push to `main`.

The included `.github/workflows/pages.yml` builds, runs unit tests and uploads `dist` to GitHub Pages. Push this project folder as the repository root on `main`, then select **Settings → Pages → Source: GitHub Actions**. The workflow selects `/REPOSITORY/` for project Pages and `/` for a `*.github.io` repository. No secrets or API keys are required.

Manual build for a project Pages URL:

```sh
VITE_BASE_PATH=/your-repository/ pnpm build
```

For a custom/root domain use `VITE_BASE_PATH=/`. Default `./` also supports serving the app from a directory. Navigation stays on one continuous sheet with no deep routes, so refreshing requires no server rewrite. Keep the trailing slash on a project URL. Serve `sw.js`, manifest, assets and `index.html` at the same configured base.

## iPhone installation and offline limits

1. Host `dist` on HTTPS (GitHub Pages is suitable).
2. Open the URL in Safari while online.
3. In Settings / Backup, wait for **Offline ready**. Failures are displayed, rather than claiming the install succeeded.
4. Use Safari **Share → Add to Home Screen → Open as Web App**, where offered.
5. Open the installed app online once and verify its own character save; import your JSON if this installation has separate storage.
6. Export after sessions.

The production service worker precaches the app shell, supplied pose reference, pixel fonts, portraits, icons and manifest. Updates wait; a visible Apply Update control activates the new version and reloads only when requested. Old caches are removed after activation. Updates never clear the character save. Offline use requires a successful prior cache; Safari can later evict website data. There is no background cloud sync. The Vite development server does not register the production worker.

## Validation actually performed

- TypeScript strict compilation and production build: passed.
- **32 automated unit tests:** passed.
- **19 end-to-end browser checks for the updated sheet:** passed in an isolated Chrome profile, using real rendered UI controls, downloads, fresh storage contexts and offline network emulation. Deterministic random inputs were injected by the test browser only; no test dice controls exist in the shipped app.
- Screens checked at **320×568, 390×844, 844×390 and 1440×1100**, including every section of the continuous sheet, inline editing, dialogs, quick controls and no horizontal document overflow.
- Production offline reload passed with saved resources, the new character poses and bundled pixel fonts. The preceding build also passed a separate `/silkwasp-companion/` deployment-path test; the redesigned build retains that base-path configuration.
- No browser JavaScript errors across the tested flows.

The original local checkout retains browser QA screenshots and results. This publishing copy includes `tests/core.test.ts`, the repeatable browser QA script, and `TESTS.md` with the requested 16-case mapping.

This is responsive browser testing, **not a physical iPhone/Safari installation test**. Actual home-screen installation, Safari storage eviction behaviour and weeks of real-world device usage have not been verified. Persistence was tested through reloads, preserved save timestamps, independent browser contexts, export/import and offline reopening. The Pages workflow is ready; deployment status is available in this repository’s Actions tab.

To repeat unit tests use `pnpm test`. Optional browser QA requires Playwright and a browser, plus a preview server:

```sh
pnpm exec vite build --base=/silkwasp-companion/ --outDir qa/subpath-dist
node scripts/build-sw.mjs qa/subpath-dist
pnpm preview
# Optional test dependency (not needed to use the app):
pnpm add --save-dev playwright
pnpm exec playwright install chromium
# In a second terminal:
node scripts/browser-qa.mjs
```

The script defaults to `http://127.0.0.1:4173/`. Set `QA_URL` to change that. `CHROME_PATH` can point to an installed Chrome executable; `PLAYWRIGHT_PATH` can point to a Playwright module outside this project. The subpath test launches a temporary local static server and closes it on completion.

## Pixel fonts

Locally bundled [VT323](https://github.com/google/fonts/tree/main/ofl/vt323), [Press Start 2P](https://github.com/google/fonts/tree/main/ofl/pressstart2p) and [DotGothic16](https://github.com/google/fonts/tree/main/ofl/dotgothic16) provide body, heading and Chinese-name pixels. Their Open Font License files are included in `public/assets/fonts/`, along with the Press Start 2P FONTLOG. No font CDN is contacted at runtime.

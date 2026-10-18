# Huang Feng · Pixel Character Sheet

[Open the character sheet](https://romanief.github.io/huang-feng-companion/)

A one-page, offline-capable D&D 5e companion for Huang Feng (黄蜂), a level 9 Lightfoot Halfling Savant / Philosopher with the Spy background. It includes pixel artwork, real dice rolls, combat and Focus tracking, compact desktop popups, item resources, rests, notes and JSON backups.

## Source and local development

The complete React + TypeScript + Vite source, supplied artwork, fonts, tests, example backup and detailed README are in **[source-project.zip](source-project.zip)**. The deployment workflow unpacks this archive in a temporary build folder; it has read-only access to repository contents.

After cloning or downloading this repository, extract `source-project.zip` into a folder. Open a terminal in that extracted folder and use Node.js 24 with pnpm 11.25.0:

```sh
corepack enable
corepack prepare pnpm@11.25.0 --activate
pnpm install --frozen-lockfile
pnpm dev
```

For checks and a production build:

```sh
pnpm test
pnpm build
pnpm preview
```

The detailed README and TESTS.md inside the archive document all rules, source precedence, DM questions, limitations, accessibility, save handling and the 16 requested validation cases. The local build and all 32 unit tests passed. The original app also passed 19 responsive browser scenarios; no physical iPhone installation test was performed.

## Publishing updates

`.github/workflows/pages.yml` runs on pushes to `main` and can also be started from Actions. It extracts `source-project.zip`, installs locked dependencies, runs tests, builds with the repository base path, and publishes only the static `dist/` output to Pages. To update the app, edit the extracted source and replace the source archive while preserving its root file structure. Changes to the root reference configuration files alone do not change the deployed app.

## Move your existing character save

1. Open your previous hosted sheet and choose **Export Character Save**.
2. Open the GitHub Pages sheet, expand **Edit sheet, rules & backup**, and import the JSON.
3. Check the preview and confirm the overwrite.

The two URLs have separate browser storage. HP, charges, Focus, notes and combat state do not transfer automatically. No browser save or session journal is uploaded to this repository.

## iPhone and offline use

Open the Pages URL in Safari while online. Wait for **Offline ready**, then use **Share → Add to Home Screen**. Export a backup after sessions. Browser data clearing, storage eviction or device loss can remove local saves; the app has no cloud sync.

## Attribution

Artwork supplied by the user. Savant and Savant: Expanded rules by laserllama; game rules and fonts retain their respective ownership and licenses. Font license files and source notes are included in the archive. Original reference PDFs and campaign saves are not included.

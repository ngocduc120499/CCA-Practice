# CCA Foundations Study Hub

Bilingual (English / Tiếng Việt) static study site for the **Claude Certified Architect — Foundations** exam:
exam format, domain weights, all 30 task statements, and an 88-question practice bank with explanations.

Content compiled from the community repo
[paullarionov/claude-certified-architect](https://github.com/paullarionov/claude-certified-architect).
Not an official Anthropic publication.

## Structure

```
public/index.html   # the whole site (self-contained, no build step)
vercel.json         # static config: serves /public, security headers
.github/workflows/  # optional CI deploy via Vercel CLI
```

## Deploy to Vercel

### Option A — Vercel CLI (fastest)

```bash
npm i -g vercel
cd cca-study-hub
vercel login          # once
vercel                # preview deploy; accept defaults
vercel --prod         # production deploy
```

### Option B — GitHub + Vercel Git integration (auto-deploy on push)

```bash
cd cca-study-hub
git init && git add . && git commit -m "CCA study hub"
gh repo create cca-study-hub --private --source . --push   # or create the repo in the GitHub UI
```

Then on vercel.com → **Add New… → Project** → import the repo.
Framework preset **Other**, leave build command empty; `vercel.json` sets the output to `public`.
Every push to `main` deploys to production, every PR gets a preview URL.
(If you use this, delete `.github/workflows/deploy-vercel.yml` to avoid double deploys.)

### Option C — GitHub Actions with the Vercel CLI

1. Run `vercel link` locally once; copy `orgId` and `projectId` from `.vercel/project.json`.
2. Create a token at vercel.com/account/tokens.
3. Add repo secrets `VERCEL_TOKEN`, `VERCEL_ORG_ID`, `VERCEL_PROJECT_ID`.
4. Push to `main` → production; PRs → preview.
   Disable the Git integration in the Vercel project settings to avoid double deploys.

## Local preview

```bash
npx serve public
```

## Notes

- Quiz progress, language and tab choice are stored in the visitor's browser (`localStorage`).
- Language: toggle in the header, or open `/#vi` / `/#en`.
- Fonts load from Google Fonts; everything else is inline.

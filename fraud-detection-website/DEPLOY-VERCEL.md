# Deploy Fraud Detection Website to Vercel

This project is a Next.js app inside a subfolder:

- App folder: `fraud-detection-website`
- Monorepo root: `Capstone-Project`

Use one of the two methods below.

## Method 1: Deploy with Vercel Dashboard (Recommended)

1. Push your latest code to GitHub.
2. Open https://vercel.com/new and import your repository.
3. In Project Settings, set:
   - Framework Preset: `Next.js`
   - Root Directory: `fraud-detection-website`
   - Build Command: `next build` (default is fine)
   - Install Command: `pnpm install` (preferred because `pnpm-lock.yaml` exists)
4. Click Deploy.
5. After deployment, open your Vercel URL and test:
   - `/`
   - `/dashboard`
   - `/api/analyze-fraud`
   - `/api/credit-score`

## Method 2: Deploy with Vercel CLI

Run these commands from your machine terminal:

```bash
cd fraud-detection-website
npm i -g vercel
vercel
```

During first setup, choose:

- Link to existing project? `No` (or `Yes` if already created)
- Project name: your choice (for example: `fraud-detection-website`)
- Directory: `.`
- Override settings? `No`

Then deploy to production:

```bash
vercel --prod
```

## Environment Variables

Current source code does not require custom environment variables (`process.env.*` not used in app source).

If you add secrets later:

1. Go to Vercel Project -> Settings -> Environment Variables
2. Add each key for Production (and Preview if needed)
3. Redeploy

## Domain Setup (Optional)

1. Vercel Project -> Settings -> Domains
2. Add your custom domain
3. Follow DNS records shown by Vercel

## Common Issues

### Wrong page deployed
Cause: Wrong root directory.
Fix: Set Root Directory to `fraud-detection-website`.

### Build uses wrong package manager
Cause: Auto-detection mismatch.
Fix: Set Install Command explicitly to `pnpm install`.

### Vercel chooses unexpected pnpm major version
Cause: `package.json` does not pin `packageManager`, so Vercel infers pnpm from project metadata.
Fix: Pin pnpm in `package.json`, for example:

```json
"packageManager": "pnpm@10.0.0"
```

If your lockfile was generated with pnpm 9 and you want to keep pnpm 9 on Vercel, pin it instead (example: `pnpm@9.15.4`) and redeploy.

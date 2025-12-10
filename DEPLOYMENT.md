# Deployment Guide for Newmanure.com

This document explains how the blog is deployed to GitHub Pages with a custom domain.

## Overview

- **Site**: https://newmanure.com
- **Platform**: GitHub Pages
- **Build Tool**: Astro
- **Deployment**: GitHub Actions (automated)

## How It Works

1. **Push to Main**: When you push changes to the `main` branch, GitHub Actions automatically triggers the deployment workflow
2. **Build Process**: The workflow installs dependencies, builds the Astro site, and generates static files in the `dist/` directory
3. **Deploy**: The built files are uploaded and deployed to GitHub Pages
4. **Custom Domain**: The `CNAME` file ensures your custom domain (newmanure.com) works correctly

## GitHub Actions Workflow

The deployment is handled by `.github/workflows/deploy.yml`:

```yaml
- Install pnpm (package manager)
- Install dependencies
- Build the Astro site
- Upload dist/ directory as artifact
- Deploy to GitHub Pages
```

## GitHub Pages Settings

To verify your GitHub Pages settings:

1. Go to your repository on GitHub: https://github.com/Newman5/newmanure
2. Click **Settings** → **Pages**
3. Ensure the following:
   - **Source**: GitHub Actions (not branch-based deployment)
   - **Custom domain**: newmanure.com

## Custom Domain (Cloudflare DNS)

Your domain is managed by Cloudflare. Ensure these DNS records are configured:

### For GitHub Pages:
- **A Record**: `185.199.108.153` (GitHub Pages IP)
- **A Record**: `185.199.109.153` (GitHub Pages IP)
- **A Record**: `185.199.110.153` (GitHub Pages IP)
- **A Record**: `185.199.111.153` (GitHub Pages IP)
- **CNAME Record** (www): `newman5.github.io`

### In Cloudflare:
1. Go to your domain's DNS settings in Cloudflare
2. Verify the above records exist
3. Ensure **Proxy status** is enabled (orange cloud icon) for performance and security

## Local Development

To test the site locally before deploying:

```bash
# Install dependencies
pnpm install

# Start development server
pnpm run dev

# Build for production
pnpm run build

# Preview production build
pnpm run preview
```

## Troubleshooting

### 404 Error on GitHub Pages
- **Cause**: Old workflow was uploading source code instead of built files
- **Fix**: New workflow (deploy.yml) builds Astro and uploads dist/ directory
- **Verify**: Check that GitHub Actions ran successfully in the "Actions" tab

### Custom Domain Not Working
- **Check CNAME file**: Ensure `public/CNAME` contains `newmanure.com`
- **Check DNS**: Verify Cloudflare DNS records point to GitHub Pages IPs
- **Check SSL**: GitHub Pages may take time to provision SSL certificate

### Build Failures
- **Check logs**: View workflow logs in the "Actions" tab
- **Local test**: Run `pnpm run build` locally to catch errors before pushing
- **Dependencies**: Ensure pnpm-lock.yaml is committed

## Vault CMS (Obsidian Integration)

This blog uses Vault CMS for writing content in Obsidian:

1. **Write**: Create/edit posts in Obsidian vault
2. **Commit**: Use Vault CMS plugin to commit changes
3. **Push**: Push to GitHub (manually or via plugin)
4. **Deploy**: GitHub Actions automatically builds and deploys

See the [Vault CMS Guide](https://github.com/davidvkimball/vault-cms) for setup instructions.

## File Structure

```
.
├── .github/workflows/
│   └── deploy.yml          # GitHub Actions deployment workflow
├── public/
│   └── CNAME               # Custom domain configuration
├── src/
│   ├── config.ts           # Site configuration
│   ├── content/            # Blog posts and pages
│   └── ...
└── dist/                   # Built site (generated, not committed)
```

## Site Configuration

Key settings in `src/config.ts`:

```typescript
site: "https://newmanure.com",
title: "Newmanure",
author: "Newman5",
deployment: {
  platform: "github-pages"
}
```

## Next Steps

1. **Verify Deployment**: Check https://newmanure.com after the next push to main
2. **GitHub Pages Settings**: Ensure GitHub Pages is using GitHub Actions as source
3. **Cloudflare DNS**: Verify DNS records point to GitHub Pages
4. **SSL Certificate**: GitHub Pages will automatically provision SSL (may take a few minutes)

## Support

For issues with:
- **Astro Modular Theme**: See [documentation](https://github.com/davidvkimball/astro-modular)
- **Vault CMS**: See [Vault CMS docs](https://github.com/davidvkimball/vault-cms)
- **GitHub Pages**: See [GitHub Pages docs](https://docs.github.com/en/pages)

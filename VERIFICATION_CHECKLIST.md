# Post-Merge Verification Checklist

After merging this PR, follow these steps to ensure everything is working correctly:

## 1. Verify GitHub Actions Workflow ✓

- [ ] Go to https://github.com/Newman5/newmanure/actions
- [ ] Look for a workflow run triggered by the merge to main
- [ ] Ensure the workflow completes successfully (green checkmark)
- [ ] Check the workflow took 2-3 minutes to complete
- [ ] Verify the "Deploy to GitHub Pages" step succeeded

**Expected Output:**
```
✓ Build with Astro
✓ Setup Pages
✓ Upload artifact
✓ Deploy to GitHub Pages
```

## 2. Verify GitHub Pages Settings ✓

- [ ] Go to https://github.com/Newman5/newmanure/settings/pages
- [ ] Confirm **Source** is set to "GitHub Actions" (not "Deploy from a branch")
- [ ] Confirm **Custom domain** shows "newmanure.com"
- [ ] Look for green checkmark and message: "Your site is live at https://newmanure.com"

**Important:** If you see "Deploy from a branch" instead of "GitHub Actions":
1. Click the dropdown under "Source"
2. Select "GitHub Actions"
3. Save the changes

## 3. Verify DNS Configuration in Cloudflare ✓

- [ ] Log into Cloudflare dashboard
- [ ] Select your domain: newmanure.com
- [ ] Go to DNS → Records
- [ ] Verify these A records exist:

| Type | Name | Content | Proxy Status |
|------|------|---------|--------------|
| A | @ | 185.199.108.153 | Proxied (orange cloud) |
| A | @ | 185.199.109.153 | Proxied (orange cloud) |
| A | @ | 185.199.110.153 | Proxied (orange cloud) |
| A | @ | 185.199.111.153 | Proxied (orange cloud) |
| CNAME | www | newman5.github.io | Proxied (orange cloud) |

**If Records are Missing:**
1. Click "Add record"
2. Add each A record pointing to GitHub Pages IPs
3. Add CNAME record for www subdomain
4. Ensure proxy status is enabled (orange cloud)

## 4. Wait for SSL Certificate ✓

- [ ] GitHub Pages automatically provisions SSL certificate
- [ ] This usually takes 5-10 minutes
- [ ] You'll see a certificate icon (🔒) in your browser when ready
- [ ] If it takes longer than 1 hour, check DNS configuration

**How to Check SSL Status:**
1. Go to GitHub Pages settings
2. Look for "HTTPS" section
3. Should show "Your site is published at https://newmanure.com"

## 5. Test Your Website ✓

- [ ] Visit https://newmanure.com
- [ ] You should see your blog homepage
- [ ] Verify the site title shows "Newmanure"
- [ ] Check that blog posts are visible
- [ ] Try clicking on a post to ensure routing works
- [ ] Try the command palette (Ctrl+K or Cmd+K)
- [ ] Test dark/light mode toggle
- [ ] Try navigating to different pages

**If You See 404:**
- Wait 5 minutes and refresh (deployment may still be in progress)
- Clear browser cache (Ctrl+Shift+R or Cmd+Shift+R)
- Try incognito/private browsing mode
- Check GitHub Actions to ensure workflow succeeded
- See Troubleshooting section in FIX_SUMMARY.md

## 6. Test Navigation and Features ✓

- [ ] Homepage loads correctly
- [ ] Blog posts page (/posts) works
- [ ] Individual post pages work
- [ ] Projects page (/projects) works
- [ ] Docs page (/docs) works
- [ ] About page (/about) works
- [ ] Contact page (/contact) works
- [ ] Command palette (Ctrl+K) opens and searches work
- [ ] Dark/light mode toggle works
- [ ] Graph view (if enabled) works

## 7. Verify SEO and Feeds ✓

- [ ] Visit https://newmanure.com/robots.txt
- [ ] Visit https://newmanure.com/sitemap.xml
- [ ] Visit https://newmanure.com/rss.xml
- [ ] Visit https://newmanure.com/feed.xml

All should load without 404 errors.

## 8. Test on Mobile Devices ✓

- [ ] Open https://newmanure.com on mobile phone
- [ ] Verify responsive design works
- [ ] Test mobile menu
- [ ] Check that images load correctly
- [ ] Verify text is readable

## 9. Check Analytics and Monitoring ✓

If you have analytics set up:
- [ ] Verify Google Analytics is tracking (if configured)
- [ ] Check Cloudflare analytics for traffic
- [ ] Monitor GitHub Actions for any failed deployments

## 10. Future Content Updates ✓

When adding new content:
- [ ] Create/edit posts in Obsidian using Vault CMS
- [ ] Commit changes via Vault CMS plugin or git
- [ ] Push to main branch
- [ ] GitHub Actions automatically builds and deploys
- [ ] Changes appear on site within 2-3 minutes

**Workflow:**
1. Write post in Obsidian
2. Save and commit via Vault CMS
3. Push to GitHub
4. Wait for GitHub Actions to complete
5. Visit newmanure.com to see changes

---

## Troubleshooting Common Issues

### Site Still Shows 404
1. Check GitHub Actions completed successfully
2. Verify GitHub Pages source is "GitHub Actions"
3. Clear browser cache and try incognito mode
4. Wait 10 minutes for deployment to propagate
5. Check DNS configuration in Cloudflare

### SSL Certificate Error
1. Wait 10-30 minutes for GitHub to provision certificate
2. Verify custom domain is set correctly in GitHub Pages
3. Verify DNS records point to GitHub Pages IPs
4. Try visiting http://newmanure.com (without https) temporarily

### Build Failures in GitHub Actions
1. View the workflow logs in Actions tab
2. Look for error messages in build output
3. Common causes:
   - External images in posts (mark as draft)
   - Syntax errors in markdown
   - Missing dependencies (run `pnpm install` locally to test)

### DNS Not Resolving
1. Use https://dnschecker.org to check DNS propagation
2. Verify A records in Cloudflare
3. Wait up to 24 hours for DNS changes to propagate globally
4. Try flushing DNS cache on your computer

### Changes Not Appearing
1. Hard refresh browser (Ctrl+Shift+R or Cmd+Shift+R)
2. Check GitHub Actions to ensure new deployment ran
3. Clear browser cache completely
4. Try different browser or incognito mode

---

## Success Criteria

Your deployment is successful when:
- ✅ GitHub Actions workflow runs without errors
- ✅ https://newmanure.com loads your blog
- ✅ SSL certificate is active (🔒 in browser)
- ✅ All pages and posts are accessible
- ✅ Navigation and features work correctly
- ✅ Site updates automatically when you push to main

---

## Need Help?

- **GitHub Actions Issues**: Check workflow logs in Actions tab
- **DNS Issues**: See Cloudflare documentation or support
- **Astro/Theme Issues**: See DEPLOYMENT.md and FIX_SUMMARY.md
- **Development Questions**: See .github/prompt.md for AI guidance

**Status**: Ready for verification! 🚀

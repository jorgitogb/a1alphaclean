# GitHub Pages Deployment Guide

This guide will help you deploy your A1 Alpha Clean website to GitHub Pages.

## Prerequisites

- A GitHub account
- Git installed on your computer
- Your project files ready to push

## Step 1: Create a GitHub Repository

1. Go to [GitHub](https://github.com) and sign in
2. Click the **+** icon in the top right and select **New repository**
3. Name your repository (e.g., `a1alphaclean`)
4. Choose **Public** (required for free GitHub Pages)
5. **Do NOT** initialize with README, .gitignore, or license (your project already has these)
6. Click **Create repository**

## Step 2: Configure Astro for GitHub Pages

### For a Project Site (username.github.io/repo-name)

If your site will be at `https://username.github.io/a1alphaclean/`, update `astro.config.mjs`:

```javascript
// @ts-check
import { defineConfig } from "astro/config";

export default defineConfig({
  site: "https://username.github.io",
  base: "/a1alphaclean",
  output: "static",
});
```

**Replace `username` with your actual GitHub username!**

### For a User/Organization Site (username.github.io)

If you named your repository `username.github.io`, update `astro.config.mjs`:

```javascript
// @ts-check
import { defineConfig } from "astro/config";

export default defineConfig({
  site: "https://username.github.io",
  output: "static",
});
```

### For a Custom Domain (a1alphaclean.com)

If you plan to use your custom domain, keep the current configuration:

```javascript
// @ts-check
import { defineConfig } from "astro/config";

export default defineConfig({
  site: "https://a1alphaclean.com",
  output: "static",
});
```

## Step 3: Push Your Code to GitHub

If you haven't initialized git yet:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/username/a1alphaclean.git
git push -u origin main
```

If you already have a git repository:

```bash
git remote add origin https://github.com/username/a1alphaclean.git
git branch -M main
git push -u origin main
```

**Replace `username` with your GitHub username!**

## Step 3.5: Disable Jekyll (CRITICAL)

GitHub Pages uses Jekyll by default, which will cause errors with Astro projects. A `.nojekyll` file has been created in your project root to disable this.

**Verify the file exists:**
- Check that `.nojekyll` file exists in your project root
- This file should be empty (it's just a marker file)
- It will be committed with your code

If you see errors like "Invalid YAML front matter in .astro files", this means Jekyll is still trying to process your files.

## Step 4: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** (top menu)
3. Click **Pages** (left sidebar)
4. Under **Source**, select **GitHub Actions**
5. The workflow will automatically run on your next push

## Step 5: Wait for Deployment

1. Go to the **Actions** tab in your repository
2. You should see a workflow run called "Deploy to GitHub Pages"
3. Wait for it to complete (usually 1-2 minutes)
4. Once complete, your site will be live!

## Step 6: Access Your Site

- **Project site**: `https://username.github.io/a1alphaclean/`
- **User site**: `https://username.github.io/`
- **Custom domain**: See below

## Custom Domain Setup (Optional)

To use `a1alphaclean.com` with GitHub Pages:

### 1. Add CNAME File

Create a file named `CNAME` in the `public` folder:

```
a1alphaclean.com
```

### 2. Configure DNS

In your domain registrar (where you bought a1alphaclean.com), add these DNS records:

**For apex domain (a1alphaclean.com):**
```
Type: A
Name: @
Value: 185.199.108.153

Type: A
Name: @
Value: 185.199.109.153

Type: A
Name: @
Value: 185.199.110.153

Type: A
Name: @
Value: 185.199.111.153
```

**For www subdomain (www.a1alphaclean.com):**
```
Type: CNAME
Name: www
Value: username.github.io
```

### 3. Enable Custom Domain in GitHub

1. Go to repository **Settings** → **Pages**
2. Under **Custom domain**, enter `a1alphaclean.com`
3. Click **Save**
4. Wait for DNS check to complete (can take up to 24 hours)
5. Once verified, check **Enforce HTTPS**

## Updating Your Site

After making changes to your site:

```bash
git add .
git commit -m "Description of changes"
git push
```

The GitHub Actions workflow will automatically rebuild and deploy your site.

## Troubleshooting

### Jekyll Error: "Invalid YAML front matter"

**Error message:**
```
ERROR: YOUR SITE COULD NOT BE BUILT:
Invalid YAML front matter in /github/workspace/src/pages/index.astro
```

**Solution:**
1. Ensure `.nojekyll` file exists in your project root (already created)
2. Make sure you've committed and pushed the `.nojekyll` file:
   ```bash
   git add .nojekyll
   git commit -m "Add .nojekyll to disable Jekyll"
   git push
   ```
3. In GitHub repository settings:
   - Go to **Settings** → **Pages**
   - Under **Source**, ensure it's set to **GitHub Actions** (NOT "Deploy from a branch")
4. Re-run the failed workflow from the Actions tab

**Why this happens:** GitHub Pages defaults to Jekyll builds. The `.nojekyll` file tells GitHub to skip Jekyll processing and use your custom workflow instead.

### Workflow Fails

- Check the **Actions** tab for error messages
- Ensure your `package.json` has the correct dependencies
- Verify `astro.config.mjs` is properly configured

### 404 Errors on Pages

- Make sure `base` is set correctly in `astro.config.mjs`
- For project sites, all links should include the base path

### Custom Domain Not Working

- Verify DNS records are correct
- Wait up to 24 hours for DNS propagation
- Check that CNAME file exists in the `public` folder
- Ensure custom domain is set in GitHub Pages settings

### Assets Not Loading

- Check that asset paths are relative or use Astro's built-in path helpers
- For project sites, ensure the `base` path is included in asset URLs

## Additional Resources

- [Astro Deployment Docs](https://docs.astro.build/en/guides/deploy/github/)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Custom Domain Setup](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)

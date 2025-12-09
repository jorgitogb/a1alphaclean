# Deploying A1 Alpha Clean to Hostgator

This guide explains how to deploy your Astro website to Hostgator hosting.

## Prerequisites

- Hostgator hosting account with cPanel access
- FTP/SFTP credentials or File Manager access
- Domain `a1alphaclean.com` configured in Hostgator

## Build the Website

1. **Build the production site:**
   ```bash
   npm run build
   ```

   This creates a `dist` folder with all static files ready for deployment.

2. **Preview the build locally (optional):**
   ```bash
   npm run preview
   ```

## Deploy to Hostgator

### Option 1: Using File Manager (Recommended for beginners)

1. Log in to your Hostgator cPanel
2. Navigate to **File Manager**
3. Go to the `public_html` directory (or your domain's root directory)
4. **Delete** all existing files in the directory (if starting fresh)
5. **Upload** all files from the `dist` folder to `public_html`
6. Ensure the `.htaccess` file is uploaded (it may be hidden)

### Option 2: Using FTP/SFTP

1. Connect to your Hostgator server using an FTP client (FileZilla, Cyberduck, etc.)
   - Host: Your domain or server IP
   - Username: Your cPanel username
   - Password: Your cPanel password
   - Port: 21 (FTP) or 22 (SFTP)

2. Navigate to the `public_html` directory

3. Upload all files from the `dist` folder to `public_html`

## Directory Structure on Hostgator

After deployment, your `public_html` should look like this:

```
public_html/
├── _astro/           # Astro's generated assets
├── favicon.svg
├── index.html
└── .htaccess         # Important for proper routing
```

## .htaccess Configuration

Create a `.htaccess` file in your `public_html` directory with the following content:

```apache
# Enable GZIP compression
<IfModule mod_deflate.c>
  AddOutputFilterByType DEFLATE text/html text/plain text/xml text/css text/javascript application/javascript application/json
</IfModule>

# Browser caching
<IfModule mod_expires.c>
  ExpiresActive On
  ExpiresByType image/jpg "access plus 1 year"
  ExpiresByType image/jpeg "access plus 1 year"
  ExpiresByType image/gif "access plus 1 year"
  ExpiresByType image/png "access plus 1 year"
  ExpiresByType image/svg+xml "access plus 1 year"
  ExpiresByType text/css "access plus 1 month"
  ExpiresByType application/javascript "access plus 1 month"
  ExpiresByType text/html "access plus 1 hour"
</IfModule>

# Security headers
<IfModule mod_headers.c>
  Header set X-Content-Type-Options "nosniff"
  Header set X-Frame-Options "SAMEORIGIN"
  Header set X-XSS-Protection "1; mode=block"
</IfModule>

# Error pages
ErrorDocument 404 /index.html
```

## Verify Deployment

1. Visit `https://a1alphaclean.com` in your browser
2. Check that all sections load correctly:
   - Hero section
   - Services section
   - Why Choose Us section
   - Contact form
   - Footer

3. Test responsive design on mobile devices

4. Verify all links work properly

## Updating the Website

To update the website after making changes:

1. Make your changes to the source files
2. Run `npm run build` to create a new production build
3. Upload the contents of the `dist` folder to Hostgator (overwrite existing files)
4. Clear your browser cache and verify changes

## Troubleshooting

### Styles not loading
- Ensure all files from `dist/_astro/` are uploaded
- Check that file permissions are correct (644 for files, 755 for directories)
- Clear browser cache

### 404 errors
- Verify `.htaccess` file is present and configured correctly
- Check that `index.html` is in the root directory

### Images not displaying
- Ensure all files from `dist/` are uploaded, including subdirectories
- Check file paths are correct (case-sensitive on Linux servers)

### Contact form not working
- The current form uses client-side JavaScript for demonstration
- For production, you'll need to implement server-side form handling or use a service like:
  - Formspree (https://formspree.io/)
  - Netlify Forms
  - EmailJS
  - Custom PHP script on Hostgator

## SSL Certificate

Ensure your domain has an SSL certificate installed:

1. In cPanel, go to **SSL/TLS Status**
2. Enable AutoSSL for your domain
3. Force HTTPS by adding to `.htaccess`:

```apache
# Force HTTPS
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

## Support

- Hostgator Support: https://www.hostgator.com/help
- Astro Documentation: https://docs.astro.build/

## Quick Reference Commands

```bash
# Development server
npm run dev

# Build for production
npm run build

# Preview production build locally
npm run preview
```

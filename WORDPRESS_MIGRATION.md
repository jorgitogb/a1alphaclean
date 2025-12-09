# Replacing WordPress with Your New Astro Site

## 🔍 The Problem

Your domain `a1alphaclean.com` previously had a WordPress site. WordPress has special configuration files that can interfere with a new site.

## ✅ Solution: Clean Up WordPress Files First

### Step 1: Log into Hostgator cPanel

1. Go to your Hostgator login page
2. Log in to cPanel
3. Open **File Manager**

### Step 2: Enable Hidden Files

1. In File Manager, click **"Settings"** (top right)
2. Check **"Show Hidden Files (dotfiles)"**
3. Click **"Save"**

### Step 3: Navigate to public_html

1. Click on **"public_html"** in the left sidebar
2. You should see WordPress files like:
   - `wp-admin` folder
   - `wp-content` folder
   - `wp-includes` folder
   - `.htaccess` file (WordPress version)
   - `index.php` file
   - `wp-config.php` file
   - Other WordPress files

### Step 4: Backup Old WordPress Site (IMPORTANT!)

Before deleting anything, create a backup:

1. **Select ALL files** in `public_html` (Ctrl + A or click checkbox at top)
2. Click **"Compress"** button at the top
3. Choose **"Zip Archive"**
4. Name it: `wordpress-backup-2024.zip`
5. Click **"Compress File(s)"**
6. Wait for compression to complete
7. **Download the backup** to your computer:
   - Right-click `wordpress-backup-2024.zip`
   - Select **"Download"**
   - Save it somewhere safe on your computer

### Step 5: Delete ALL WordPress Files

Now that you have a backup, delete everything:

1. **Deselect the backup** (uncheck `wordpress-backup-2024.zip`)
2. **Select ALL other files** in `public_html`:
   - All folders (`wp-admin`, `wp-content`, `wp-includes`, etc.)
   - All files (`.htaccess`, `index.php`, `wp-config.php`, etc.)
3. Click **"Delete"** button at the top
4. Confirm deletion
5. Wait for deletion to complete

Your `public_html` folder should now be **EMPTY** except for the backup zip file.

### Step 6: Upload Your New Astro Site

Now follow the upload steps from the main deployment guide:

#### Quick Upload Method:

1. **On your computer**, go to:
   ```
   C:\Users\brizuela\Documents\workspace\a1alphaclean\dist
   ```

2. **Select ALL files** (Ctrl + A):
   - `.htaccess`
   - `favicon.svg`
   - `index.html`
   - `_astro` folder

3. **Create a zip file**:
   - Right-click → "Send to" → "Compressed (zipped) folder"
   - Name it `new-site.zip`

4. **Upload to Hostgator**:
   - In File Manager (in `public_html`)
   - Click **"Upload"**
   - Select `new-site.zip`
   - Upload it

5. **Extract the zip**:
   - Right-click `new-site.zip` in File Manager
   - Select **"Extract"**
   - Click **"Extract File(s)"**

6. **Move files to root**:
   - You'll see a folder created (might be called `dist` or `new-site`)
   - Open that folder
   - Select ALL files inside (Ctrl + A)
   - Click **"Move"**
   - Type: `/public_html`
   - Click **"Move File(s)"**

7. **Clean up**:
   - Go back to `public_html`
   - Delete the empty folder
   - Delete `new-site.zip`
   - **KEEP** `wordpress-backup-2024.zip` (your backup)

### Step 7: Verify Files Are Correct

Your `public_html` should now have:

```
public_html/
├── .htaccess                      ← Your NEW .htaccess (not WordPress)
├── favicon.svg                    ← Your favicon
├── index.html                     ← Your homepage
├── _astro/                        ← Folder with CSS/JS
└── wordpress-backup-2024.zip      ← Your backup (safe to keep)
```

### Step 8: Clear WordPress Cache

WordPress might have caching that needs to be cleared:

1. In cPanel, find **"Select PHP Version"** or **"MultiPHP Manager"**
2. Make sure PHP is enabled (it should be)
3. In cPanel, find **"Optimize Website"** or **"Cache Manager"**
4. Clear all caches if available

### Step 9: Test Your Site

1. Open a **new incognito/private browser window** (Ctrl + Shift + N in Chrome)
2. Go to: `https://a1alphaclean.com`
3. You should now see your NEW Astro site!

If you still see WordPress or an error:
- Clear your browser cache completely
- Wait 5-10 minutes for server cache to clear
- Try accessing via: `https://a1alphaclean.com/index.html`

## 🔧 Troubleshooting

### Still Seeing WordPress?

**Check .htaccess file:**

1. In File Manager, right-click `.htaccess`
2. Select **"Edit"**
3. Make sure it's YOUR `.htaccess` (from the Astro project)
4. It should start with: `# A1 Alpha Clean - Apache Configuration`
5. If it has WordPress rules, delete it and re-upload your `.htaccess`

**WordPress .htaccess looks like this (DELETE THIS):**
```apache
# BEGIN WordPress
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteBase /
RewriteRule ^index\.php$ - [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.php [L]
</IfModule>
# END WordPress
```

**Your NEW .htaccess should look like this (KEEP THIS):**
```apache
# A1 Alpha Clean - Apache Configuration for Hostgator

# Enable GZIP compression
<IfModule mod_deflate.c>
  AddOutputFilterByType DEFLATE text/html text/plain text/xml text/css text/javascript application/javascript application/json
</IfModule>
```

### Still Getting "Site Can't Be Reached"?

This means DNS might not be configured:

1. Check your domain registrar (where you bought the domain)
2. Make sure nameservers point to Hostgator:
   - `ns1.hostgator.com`
   - `ns2.hostgator.com`
3. DNS changes can take 24-48 hours to propagate

### Files Are There But Site Not Loading?

Check file permissions:

1. In File Manager, right-click `index.html`
2. Select **"Change Permissions"**
3. Set to: `644` (or check: Owner Read+Write, Group Read, World Read)
4. Click **"Change Permissions"**

Do the same for folders:
1. Right-click `_astro` folder
2. Set to: `755`

## ✅ Success Checklist

After following these steps, you should have:

- [x] WordPress files backed up
- [x] Old WordPress files deleted
- [x] New Astro site files uploaded
- [x] Files in correct location (`public_html`)
- [x] `.htaccess` is the NEW one (not WordPress)
- [x] Site loads at https://a1alphaclean.com
- [x] All styles working
- [x] Favicon showing

## 📞 Need Help?

If you're still having issues:

1. **Check what's in public_html:**
   - Take a screenshot of File Manager showing all files
   - Make sure you see: `.htaccess`, `index.html`, `favicon.svg`, `_astro/`

2. **Check the .htaccess content:**
   - Open it and verify it's the Astro version, not WordPress

3. **Try direct access:**
   - Visit: `https://a1alphaclean.com/index.html`
   - If this works but the root doesn't, it's an `.htaccess` issue

4. **Contact Hostgator Support:**
   - They can verify DNS is pointing correctly
   - They can check if there are any server-level redirects
   - Available 24/7 via live chat in cPanel

# Reset Hostgator Configuration for a1alphaclean.com

## 🔄 Reset Hostgator to Fresh State

This will clear any old WordPress or configuration issues and start fresh.

## Step 1: Remove Domain (If It Exists)

### Check if Domain is Added:

1. **Log into Hostgator cPanel**
2. Search for **"Domains"** or **"Addon Domains"**
3. Look for `a1alphaclean.com` in the list

### If Domain is Listed as Addon Domain:

1. Find `a1alphaclean.com` in the list
2. Click **"Remove"** or the trash icon next to it
3. Confirm removal
4. Wait for it to be removed

### If It's Your Primary Domain:

- You can't remove it, but you can clean it up (continue to Step 2)

## Step 2: Clean Out public_html Completely

### Backup First (Important!):

1. **In File Manager**, go to `public_html`
2. Click **"Settings"** → Enable **"Show Hidden Files"**
3. **Select ALL files** in `public_html` (click checkbox at top)
4. Click **"Compress"**
5. Choose **"Zip Archive"**
6. Name: `backup-before-reset.zip`
7. Click **"Compress File(s)"**
8. **Download** `backup-before-reset.zip` to your computer (right-click → Download)

### Delete Everything:

1. **Deselect** the backup zip (uncheck `backup-before-reset.zip`)
2. **Select ALL other files and folders**:
   - All WordPress files (`wp-admin`, `wp-content`, `wp-includes`, etc.)
   - All `.htaccess` files
   - All `index.php`, `index.html` files
   - Everything except the backup zip
3. Click **"Delete"**
4. Confirm deletion
5. Wait for deletion to complete

**Result:** `public_html` should now be EMPTY except for `backup-before-reset.zip`

## Step 3: Reset .htaccess (If Needed)

If there's a `.htaccess` file that won't delete or keeps coming back:

1. **Right-click** `.htaccess`
2. Select **"Edit"**
3. **Delete ALL content** inside
4. Click **"Save Changes"**
5. Then delete the file

## Step 4: Clear PHP/Cache Settings

### Reset PHP Version:

1. In cPanel, find **"Select PHP Version"** or **"MultiPHP Manager"**
2. Select your domain
3. Set PHP version to **7.4** or **8.0** (recommended)
4. Click **"Apply"**

### Clear Caches:

1. In cPanel, search for **"Cache Manager"** or **"Optimize Website"**
2. If available, click **"Clear All Caches"**
3. Or select **"Compress All Content"**

## Step 5: Re-add Domain (If Removed)

If you removed the domain in Step 1, add it back:

1. In cPanel, go to **"Addon Domains"**
2. Click **"Create a New Domain"**
3. Enter:
   - **Domain:** `a1alphaclean.com`
   - **Subdomain:** Leave blank or auto-fill
   - **Document Root:** `public_html` (or `public_html/a1alphaclean.com`)
4. **Uncheck** "Create an FTP account" (not needed)
5. Click **"Add Domain"**
6. Wait for domain to be added

## Step 6: Verify DNS/Nameservers

Make sure domain points to Hostgator:

1. **In cPanel**, find **"Zone Editor"** or **"DNS Zone Editor"**
2. Find `a1alphaclean.com`
3. Verify there's an **A Record** pointing to your server IP

**OR check nameservers:**

1. Go to where you bought the domain (GoDaddy, Namecheap, etc.)
2. Find DNS/Nameserver settings
3. Make sure nameservers are:
   ```
   ns1.hostgator.com
   ns2.hostgator.com
   ```
4. If not, change them and wait 24-48 hours

## Step 7: Upload Your Fresh Site

Now that Hostgator is clean, upload your site:

### Create Upload Package:

1. **On your computer**, go to:
   ```
   C:\Users\brizuela\Documents\workspace\a1alphaclean\dist
   ```

2. **Select ALL files** (Ctrl+A):
   - `.htaccess`
   - `favicon.svg`
   - `index.html`
   - `_astro` folder

3. **Right-click** → "Send to" → "Compressed (zipped) folder"
4. Name it: `site-upload.zip`

### Upload to Hostgator:

1. **In File Manager**, make sure you're in `public_html`
2. Click **"Upload"**
3. Select `site-upload.zip`
4. Wait for upload to complete

### Extract Files:

1. **Right-click** `site-upload.zip` in File Manager
2. Select **"Extract"**
3. Click **"Extract File(s)"**
4. Wait for extraction

### Move to Correct Location:

If files extracted into a subfolder:

1. Open the extracted folder
2. Select ALL files inside (Ctrl+A)
3. Click **"Move"**
4. Type: `/public_html`
5. Click **"Move File(s)"**

### Clean Up:

1. Delete `site-upload.zip`
2. Delete any empty folders
3. Delete `backup-before-reset.zip` (if you don't need it)

## Step 8: Set Correct Permissions

### For Files:

1. **Select** `index.html`
2. Click **"Change Permissions"**
3. Set to: **644**
4. Click **"Change Permissions"**

Do the same for:
- `.htaccess` → 644
- `favicon.svg` → 644

### For Folders:

1. **Right-click** `_astro` folder
2. Select **"Change Permissions"**
3. Set to: **755**
4. **Check** "Recurse into subdirectories"
5. Click **"Change Permissions"**

## Step 9: Force HTTPS (Optional)

If you have SSL certificate:

1. In cPanel, find **"SSL/TLS Status"**
2. Enable AutoSSL for `a1alphaclean.com`
3. Wait a few minutes for certificate

Then edit `.htaccess`:

1. **Right-click** `.htaccess` in File Manager
2. Select **"Edit"**
3. Find the HTTPS section (around line 30)
4. **Uncomment** these lines (remove the `#`):
   ```apache
   RewriteEngine On
   RewriteCond %{HTTPS} off
   RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
   ```
5. Click **"Save Changes"**

## Step 10: Test Your Site

1. **Clear browser cache** (Ctrl+Shift+Delete)
2. **Visit:** `https://a1alphaclean.com`
3. **You should see:**
   - Blue gradient hero section
   - "Sparkling Clean Spaces, Every Single Time"
   - All styles loading correctly

## ✅ Final Verification

Your `public_html` should look like this:

```
public_html/
├── .htaccess          ← Your new .htaccess
├── favicon.svg        ← Your favicon
├── index.html         ← Your homepage
└── _astro/            ← Folder with CSS/JS
    └── [hashed files]
```

**NOT like this:**
```
public_html/
├── backup-before-reset.zip
├── site-upload.zip
└── dist/              ← Files should NOT be in a subfolder
    ├── index.html
    └── ...
```

## 🔧 If Still Not Working

### Check Server IP:

1. In cPanel → **"Server Information"**
2. Find **"Shared IP Address"**
3. Visit: `http://[your-ip]` in browser
4. If site loads → DNS issue (wait for propagation)
5. If doesn't load → Contact Hostgator support

### Contact Hostgator Support:

1. In cPanel, click **"Support"** or **"Live Chat"**
2. Tell them:
   - "I uploaded a static HTML site to public_html"
   - "Domain is a1alphaclean.com"
   - "Site not loading, can you check DNS and server configuration?"

They can verify:
- Domain is properly added
- DNS is correct
- No server-level blocks
- Files are in correct location

## 📞 Support Resources

- **Hostgator Live Chat:** Available 24/7 in cPanel
- **Hostgator Phone:** Check your welcome email
- **Hostgator Help:** https://www.hostgator.com/help

---

## ✅ Summary

After this reset, you'll have:
- ✅ Clean Hostgator configuration
- ✅ No WordPress remnants
- ✅ Fresh upload of your Astro site
- ✅ Correct file permissions
- ✅ Proper DNS configuration

Your site should load at `https://a1alphaclean.com`!

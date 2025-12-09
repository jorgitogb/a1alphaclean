# Step-by-Step Deployment Guide for A1 Alpha Clean

## ✅ Pre-Deployment Checklist

Before uploading to Hostgator, verify you have:

- [x] Production build completed (`npm run build`)
- [x] `dist` folder exists with all files
- [x] Hostgator hosting account with cPanel access
- [x] Domain `a1alphaclean.com` added to your Hostgator account
- [ ] Hostgator login credentials ready

## 📁 What's in Your `dist` Folder

Your `dist` folder should contain these files:

```
dist/
├── .htaccess          (1.3 KB - HIDDEN FILE, very important!)
├── favicon.svg        (870 bytes)
├── index.html         (12.7 KB)
└── _astro/            (folder with CSS and JS files)
    └── [hashed files].css
```

**IMPORTANT:** The `.htaccess` file is hidden by default. Make sure you can see it before uploading!

### How to See Hidden Files in Windows

1. Open the `dist` folder in File Explorer
2. Click the **View** tab at the top
3. Check **"Hidden items"** in the Show/hide section
4. You should now see `.htaccess` file

---

## 🚀 Method 1: Upload via Hostgator File Manager (Recommended)

### Step 1: Log into cPanel

1. Go to your Hostgator login page (usually `https://yourdomain.com/cpanel` or through the Hostgator portal)
2. Enter your cPanel username and password
3. You should see the cPanel dashboard

### Step 2: Enable Hidden Files in File Manager

1. In cPanel, find and click **"File Manager"** (usually in the "Files" section)
2. Once File Manager opens, click **"Settings"** in the top-right corner
3. In the Preferences dialog:
   - ✅ Check **"Show Hidden Files (dotfiles)"**
   - Click **"Save"**
4. Now you'll be able to see `.htaccess` files

### Step 3: Navigate to public_html

1. In the left sidebar, click on **"public_html"** folder
2. This is where your website files go
3. **IMPORTANT:** If you see existing files (like a default index.html), you may need to:
   - Back them up first (select and click "Compress" to create a backup.zip)
   - Then delete them to make room for your new site

### Step 4: Upload Your Files

**The Simple Way (Recommended):**

1. **On your computer**, open File Explorer and go to:
   ```
   C:\Users\brizuela\Documents\workspace\a1alphaclean\dist
   ```

2. **Select ALL files** in the `dist` folder:
   - Press `Ctrl + A` to select everything
   - You should see: `.htaccess`, `favicon.svg`, `index.html`, and `_astro` folder highlighted

3. **Right-click** on the selected files and choose **"Send to"** → **"Compressed (zipped) folder"**
   - This creates a file called `dist.zip` (or similar)
   - This zip file contains everything you need

4. **In Hostgator File Manager** (in your browser):
   - Make sure you're in the `public_html` folder
   - Click the **"Upload"** button at the top
   - Click **"Select File"**
   - Find and select the `dist.zip` file you just created
   - Click **"Open"** to upload it
   - Wait for the upload to finish (you'll see "Upload Complete")

5. **Extract the zip file**:
   - Back in File Manager, you should now see `dist.zip` in `public_html`
   - **Right-click** on `dist.zip`
   - Select **"Extract"**
   - A dialog appears - just click **"Extract File(s)"**
   - Wait for extraction to complete

6. **Move files to the correct location**:
   - After extraction, you'll see a `dist` folder in `public_html`
   - **Open** the `dist` folder (double-click it)
   - **Select ALL files** inside (Ctrl + A):
     - `.htaccess`
     - `favicon.svg`
     - `index.html`
     - `_astro` folder
   - Click **"Move"** button at the top
   - In the "Move to" dialog, type: `/public_html`
   - Click **"Move File(s)"**

7. **Clean up**:
   - Go back to `public_html` (click it in the left sidebar)
   - Delete the empty `dist` folder (select it, click "Delete")
   - Delete the `dist.zip` file (select it, click "Delete")

### Step 5: Verify All Files Are Uploaded

In File Manager, your `public_html` should now show:

```
public_html/
├── .htaccess          ← Must be visible (if not, check Settings)
├── favicon.svg
├── index.html
└── _astro/            ← Folder with CSS/JS files inside
```

**Double-check:**
- ✅ `.htaccess` file is present (enable "Show Hidden Files" if you don't see it)
- ✅ `_astro` folder exists and contains CSS files
- ✅ `index.html` is in the root of public_html
- ✅ `favicon.svg` is present

---

## 🚀 Method 2: Upload via FTP (Alternative)

### Step 1: Get Your FTP Credentials

1. In cPanel, search for **"FTP Accounts"**
2. Your main FTP account credentials are usually:
   - **Host:** `ftp.a1alphaclean.com` or your server IP
   - **Username:** Your cPanel username
   - **Password:** Your cPanel password
   - **Port:** 21 (FTP) or 22 (SFTP)

### Step 2: Download an FTP Client

If you don't have one, download **FileZilla** (free):
- Go to: https://filezilla-project.org/
- Download and install FileZilla Client

### Step 3: Connect to Your Server

1. Open FileZilla
2. Enter your FTP credentials at the top:
   - Host: `ftp.a1alphaclean.com`
   - Username: [your cPanel username]
   - Password: [your cPanel password]
   - Port: 21
3. Click **"Quickconnect"**
4. If prompted about unknown certificate, click **"OK"**

### Step 4: Navigate to public_html

1. In the **"Remote site"** panel (right side), navigate to `/public_html`
2. In the **"Local site"** panel (left side), navigate to:
   `C:\Users\brizuela\Documents\workspace\a1alphaclean\dist`

### Step 5: Upload Files

1. In the left panel (local), select ALL files in the `dist` folder:
   - `.htaccess` (if you don't see it, enable "Show hidden files" in FileZilla settings)
   - `favicon.svg`
   - `index.html`
   - `_astro` folder
2. Right-click and select **"Upload"**
3. Or simply drag and drop from left to right panel
4. Wait for all files to upload (watch the transfer queue at the bottom)

### Step 6: Verify Upload

Check the right panel (remote site) to ensure all files are on the server:
- `.htaccess`
- `favicon.svg`
- `index.html`
- `_astro/` folder with files inside

---

## 🔒 Step 7: Enable SSL Certificate (HTTPS)

### Enable Free SSL in cPanel

1. In cPanel, find **"SSL/TLS Status"** (in Security section)
2. Find `a1alphaclean.com` in the list
3. Click **"Run AutoSSL"** or enable it
4. Wait a few minutes for the certificate to be issued
5. Your site will now be accessible via `https://a1alphaclean.com`

### Force HTTPS Redirect

Once SSL is active, edit the `.htaccess` file to force HTTPS:

1. In File Manager, right-click `.htaccess`
2. Select **"Edit"**
3. Find these lines (around line 30):

```apache
# Force HTTPS (uncomment after SSL is set up)
# RewriteEngine On
# RewriteCond %{HTTPS} off
# RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

4. Remove the `#` symbols to uncomment:

```apache
# Force HTTPS
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

5. Click **"Save Changes"**
6. Now all HTTP traffic will redirect to HTTPS

---

## ✅ Step 8: Test Your Live Website

### Visit Your Website

1. Open a web browser
2. Go to: **https://a1alphaclean.com**
3. You should see your website with:
   - ✅ Blue gradient hero section
   - ✅ "Sparkling Clean Spaces, Every Single Time" heading
   - ✅ Styled buttons and cards
   - ✅ Custom favicon in the browser tab
   - ✅ All sections: Services, Why Choose Us, Contact Form, Footer

### Test Checklist

- [ ] Website loads at https://a1alphaclean.com
- [ ] All styles are applied (gradients, colors, fonts)
- [ ] Favicon appears in browser tab
- [ ] Hero section has blue gradient background
- [ ] Buttons are styled and clickable
- [ ] Service cards have shadows and hover effects
- [ ] Contact form is visible
- [ ] Footer displays correctly
- [ ] Mobile responsive (test on phone or resize browser)
- [ ] No 404 errors in browser console (press F12 to check)

### If Styles Don't Load

1. **Clear your browser cache:**
   - Press `Ctrl + Shift + Delete`
   - Clear cached images and files
   - Reload the page

2. **Check File Manager:**
   - Verify `_astro` folder exists in public_html
   - Verify it contains CSS files (they have long hashed names)

3. **Check browser console:**
   - Press F12
   - Look for any 404 errors
   - All files should load successfully

---

## 🔧 Troubleshooting Common Issues

### Issue: "This site can't be reached"

**Causes:**
- Domain DNS hasn't propagated yet
- Domain not pointing to Hostgator nameservers

**Solutions:**
1. Check domain nameservers in your domain registrar
2. They should point to Hostgator's nameservers (usually `ns1.hostgator.com` and `ns2.hostgator.com`)
3. DNS propagation can take 24-48 hours
4. Test with your server's IP address instead: `http://[your-server-ip]`

### Issue: Styles Not Loading (Plain HTML)

**Causes:**
- `_astro` folder not uploaded
- `.htaccess` file missing
- Files in wrong directory

**Solutions:**
1. Verify `_astro` folder is in `public_html`
2. Check that `.htaccess` is present (enable "Show Hidden Files")
3. Ensure files are in `public_html`, not a subdirectory
4. Clear browser cache and reload

### Issue: 404 Error on Page

**Causes:**
- `index.html` not in the root of public_html
- File permissions incorrect

**Solutions:**
1. Move `index.html` to the root of `public_html`
2. Right-click `index.html` → Permissions → Set to `644`
3. Set folder permissions to `755`

### Issue: .htaccess Not Visible

**Solutions:**
1. In File Manager, click **Settings**
2. Enable **"Show Hidden Files (dotfiles)"**
3. Click **Save**
4. Refresh File Manager

### Issue: Contact Form Not Working

**Note:** The current form uses JavaScript for demonstration. For production:

**Options:**
1. **Formspree** (easiest): https://formspree.io/
   - Free tier available
   - Add your email to receive form submissions

2. **EmailJS**: https://www.emailjs.com/
   - Send emails directly from JavaScript

3. **Custom PHP Script** (requires PHP knowledge)
   - Create a `contact.php` file to handle form submissions

---

## 📊 Post-Deployment Steps

### 1. Set Up Google Analytics (Optional)

1. Go to https://analytics.google.com/
2. Create a new property for `a1alphaclean.com`
3. Get your tracking code
4. Add it to `src/layouts/Layout.astro` in the `<head>` section
5. Rebuild and redeploy

### 2. Submit to Google Search Console

1. Go to https://search.google.com/search-console
2. Add property: `https://a1alphaclean.com`
3. Verify ownership (via HTML file upload or DNS)
4. Submit your sitemap (you may need to generate one)

### 3. Set Up Google Business Profile

1. Go to https://www.google.com/business/
2. Create a profile for A1 Alpha Clean
3. Add your website URL
4. Verify your business
5. Add photos and business information

### 4. Update Contact Information

Remember to update the placeholder contact info in the website:

**Current placeholders:**
- Phone: (702) 555-1234
- Email: info@a1alphaclean.com

**To update:**
1. Edit `src/pages/index.astro`
2. Find the contact section (around line 180)
3. Replace with your real contact information
4. Run `npm run build`
5. Re-upload the new `dist/index.html` to Hostgator

---

## 🔄 How to Update Your Website

When you make changes to your website:

1. **Edit source files** in `src/` folder
2. **Test locally:** Run `npm run dev` and check `http://localhost:4321`
3. **Build:** Run `npm run build`
4. **Upload:** Upload the new files from `dist/` to Hostgator
   - You can upload just the changed files
   - Or upload everything to be safe
5. **Clear cache:** Clear your browser cache to see changes

---

## 📞 Support Resources

- **Hostgator Support:** https://www.hostgator.com/help
- **Hostgator Live Chat:** Available 24/7 in cPanel
- **Astro Documentation:** https://docs.astro.build/
- **This Project:** `C:\Users\brizuela\Documents\workspace\a1alphaclean`

---

## ✅ Deployment Complete!

Once you've followed these steps, your website should be live at:

🌐 **https://a1alphaclean.com**

Congratulations! Your A1 Alpha Clean website is now live and ready to attract customers! 🎉

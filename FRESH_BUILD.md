# Fresh Build & Upload Guide

## ✅ Your Configuration is Correct

Your `astro.config.mjs` is already properly configured:
- ✅ Site URL: `https://a1alphaclean.com`
- ✅ Output: `static` (perfect for Hostgator)

## 🔄 Fresh Build Steps

Let's create a clean build and upload it:

### Step 1: Clean Build

Run these commands in order:

```bash
# Stop any running dev servers first (Ctrl+C if needed)

# Remove old build
Remove-Item -Recurse -Force dist

# Create fresh build
npm run build
```

### Step 2: Verify Build

Check that `dist` folder was created:

```bash
# List contents of dist folder
Get-ChildItem dist -Force
```

You should see:
- `.htaccess` (hidden file)
- `favicon.svg`
- `index.html`
- `_astro` folder

### Step 3: Create Upload Package

Create a single zip file with everything:

**In PowerShell:**

```powershell
# Go to your project folder
cd C:\Users\brizuela\Documents\workspace\a1alphaclean

# Create zip of dist folder contents
Compress-Archive -Path "dist\*" -DestinationPath "a1alphaclean-upload.zip" -Force
```

**Or manually:**
1. Open `C:\Users\brizuela\Documents\workspace\a1alphaclean\dist`
2. Press `Ctrl + A` to select all files
3. Right-click → "Send to" → "Compressed (zipped) folder"
4. Name it: `a1alphaclean-upload.zip`

### Step 4: Upload to Hostgator

1. **Log into Hostgator cPanel**
   - Go to your Hostgator login page
   - Enter your credentials

2. **Open File Manager**
   - Click "File Manager" in cPanel

3. **Enable Hidden Files**
   - Click "Settings" (top right)
   - Check "Show Hidden Files (dotfiles)"
   - Click "Save"

4. **Go to public_html**
   - Click "public_html" in left sidebar

5. **Clear public_html (if needed)**
   - If there are old files, select them all
   - Click "Delete"
   - Confirm deletion

6. **Upload Your Zip**
   - Click "Upload" button
   - Click "Select File"
   - Choose `a1alphaclean-upload.zip` from your computer
   - Wait for upload to complete

7. **Extract the Zip**
   - Back in File Manager, you should see `a1alphaclean-upload.zip`
   - Right-click on it
   - Select "Extract"
   - Click "Extract File(s)"
   - Wait for extraction

8. **Verify Files**
   - You should now see in `public_html`:
     - `.htaccess`
     - `favicon.svg`
     - `index.html`
     - `_astro` folder

9. **Clean Up**
   - Delete `a1alphaclean-upload.zip` (you don't need it anymore)

### Step 5: Test Your Site

1. **Clear your browser cache:**
   - Press `Ctrl + Shift + Delete`
   - Select "Cached images and files"
   - Click "Clear data"

2. **Visit your site:**
   - Go to: `https://a1alphaclean.com`
   - Or try: `http://a1alphaclean.com`

3. **What you should see:**
   - Blue gradient hero section
   - "Sparkling Clean Spaces, Every Single Time"
   - Styled buttons and cards
   - All sections loading correctly

## 🔧 If Site Still Doesn't Load

### Check 1: Files in Correct Location

In File Manager, verify `public_html` contains:
```
public_html/
├── .htaccess          ← Must be here (not in a subfolder)
├── favicon.svg        ← Must be here
├── index.html         ← Must be here
└── _astro/            ← Must be here
    └── [CSS files]
```

**NOT like this:**
```
public_html/
└── dist/              ← WRONG! Files are nested
    ├── .htaccess
    ├── index.html
    └── ...
```

If files are in a `dist` subfolder:
1. Open the `dist` folder
2. Select all files inside (Ctrl+A)
3. Click "Move"
4. Type: `/public_html`
5. Click "Move File(s)"
6. Delete the empty `dist` folder

### Check 2: DNS Configuration

Your domain must point to Hostgator:

1. **Find where you registered the domain** (GoDaddy, Namecheap, etc.)
2. **Log into that account**
3. **Find DNS or Nameserver settings**
4. **Verify nameservers are:**
   ```
   ns1.hostgator.com
   ns2.hostgator.com
   ```

If they're different, change them and wait 24-48 hours.

### Check 3: Test with IP Address

While waiting for DNS:

1. In cPanel, find "Server Information"
2. Look for "Shared IP Address"
3. Copy the IP (e.g., `123.45.67.89`)
4. Visit: `http://[your-ip-address]` in browser
5. If site loads → DNS issue, wait for propagation
6. If site doesn't load → File location issue

### Check 4: File Permissions

Make sure files have correct permissions:

1. In File Manager, right-click `index.html`
2. Select "Change Permissions"
3. Set to: `644`
4. Click "Change Permissions"

For the `_astro` folder:
1. Right-click `_astro`
2. Select "Change Permissions"
3. Set to: `755`
4. Check "Recurse into subdirectories"
5. Click "Change Permissions"

## ✅ Final Checklist

Before asking for help, verify:

- [ ] Ran `npm run build` successfully
- [ ] `dist` folder exists on your computer
- [ ] Created zip file of dist contents
- [ ] Uploaded zip to Hostgator
- [ ] Extracted zip in File Manager
- [ ] Files are in `public_html` root (not in subfolder)
- [ ] `.htaccess` file is visible (hidden files enabled)
- [ ] `_astro` folder contains CSS files
- [ ] Cleared browser cache
- [ ] Tried both http:// and https://
- [ ] Checked DNS nameservers

## 📞 Still Need Help?

If you've completed all steps and site still doesn't load, provide:

1. **Screenshot of File Manager** showing `public_html` contents
2. **Where you bought the domain** (registrar name)
3. **What you see** when visiting the site (error message, blank page, etc.)
4. **Result of IP address test** (does it load via IP?)

This will help diagnose the exact issue!

# How to Deploy OpenSecureAI.org to GitHub Pages

This guide provides step-by-step instructions to deploy the OpenSecureAI landing page to GitHub Pages and serve it at `https://opensecureai.org`.

## 📋 Prerequisites

Before starting, ensure you have:
- A GitHub account
- The OpenSecureAI.org files ready (index.html, styles.css, script.js)
- Access to DNS settings for your domain (opensecureai.org)
- Basic familiarity with Git and GitHub

## 🚀 Deployment Options

### Option 1: Deploy to GitHub Pages with Custom Domain (Recommended)

#### Step 1: Create GitHub Repository

1. **Log in to GitHub** at [github.com](https://github.com)
2. **Create a new repository** named `opensecureai.org`
   - Click the "+" icon in the top right → "New repository"
   - Repository name: `opensecureai.org`
   - Description: "OpenSecureAI landing page - Securing AI for Humanity"
   - Set to **Public** (required for GitHub Pages)
   - **DO NOT** initialize with README (we'll add our own)
   - Click "Create repository"

#### Step 2: Upload Files to Repository

**Method A: Upload via GitHub Web Interface (Easiest)**

1. **Upload files** to your new repository:
   - Click "uploading an existing file" link on the repository page
   - Drag and drop these files:
     - `index.html`
     - `styles.css`
     - `script.js`
     - `README.md`
     - `.gitignore`
   - Add commit message: "Initial OpenSecureAI landing page"
   - Click "Commit changes"

**Method B: Upload via Git Command Line**

```bash
# Clone your repository (replace YOUR_USERNAME)
git clone https://github.com/YOUR_USERNAME/opensecureai.org.git
cd opensecureai.org

# Copy your files to the repository
cp /path/to/your/files/* .

# Add and commit files
git add .
git commit -m "Initial OpenSecureAI landing page"
git push origin main
```

#### Step 3: Enable GitHub Pages

1. **Navigate to Settings** in your repository
2. **Go to Pages** in the left sidebar
3. **Configure GitHub Pages**:
   - Source: "Deploy from a branch"
   - Branch: `main` (or `master`)
   - Folder: `/ (root)`
   - Click "Save"

4. **Wait for deployment** (usually 1-2 minutes)
5. **Your site will be available at**: `https://YOUR_USERNAME.github.io/opensecureai.org`

#### Step 4: Configure Custom Domain (opensecureai.org)

**Step 4.1: Add CNAME file to repository**

1. **Create CNAME file** in your repository root:
   - Click "Create new file" in your repository
   - Name the file exactly `CNAME` (no extension)
   - Content: `opensecureai.org`
   - Commit message: "Add custom domain configuration"
   - Click "Commit new file"

**Step 4.2: Configure DNS Settings**

**For opensecureai.org domain, configure DNS with your domain provider:**

**Option A: Using A Records (Recommended)**
- Add these A records to your DNS:
  ```
  185.199.108.153
  185.199.109.153
  185.199.110.153
  185.199.111.153
  ```

**Option B: Using CNAME Record**
- Add CNAME record:
  - Name: `www` (or `@` for root)
  - Value: `YOUR_USERNAME.github.io`

**Step 4.3: Enable HTTPS**

1. **Wait for DNS propagation** (5-30 minutes)
2. **Check GitHub Pages settings**:
   - Go to repository Settings → Pages
   - Under "Custom domain", you should see "Your site is published at https://opensecureai.org"
   - Enable "Enforce HTTPS" checkbox

### Option 2: Deploy to GitHub Pages without Custom Domain

If you don't have a custom domain, you can still deploy to GitHub Pages:

1. **Follow Steps 1-3** from Option 1
2. **Your site will be available at**: `https://YOUR_USERNAME.github.io/opensecureai.org`

## 🔧 Verification Steps

### 1. Check GitHub Pages Status
- Go to your repository Settings → Pages
- Look for green checkmark: "Your site is published at..."
- If you see any errors, check the troubleshooting section below

### 2. Test Your Site
- Visit `https://opensecureai.org` (or your GitHub Pages URL)
- Test on different devices and browsers
- Check all links and navigation
- Verify contact forms work (if applicable)

### 3. Test HTTPS
- Ensure your site loads with `https://`
- Check for mixed content warnings in browser console

## 🛠️ Troubleshooting

### Common Issues and Solutions

#### Issue: Site not loading at custom domain
**Solutions:**
1. **Check DNS propagation**:
   ```bash
   nslookup opensecureai.org
   dig opensecureai.org
   ```
2. **Verify CNAME file** exists in repository root
3. **Check DNS configuration** with your domain provider
4. **Wait longer** - DNS changes can take up to 48 hours

#### Issue: HTTPS not working
**Solutions:**
1. **Wait for certificate generation** (can take up to 1 hour)
2. **Check custom domain settings** in GitHub Pages
3. **Ensure DNS is properly configured**
4. **Try accessing via HTTP first**, then HTTPS

#### Issue: CSS/JS not loading
**Solutions:**
1. **Check file paths** in index.html
2. **Verify files are uploaded** to repository
3. **Check browser console** for 404 errors
4. **Ensure case sensitivity** (GitHub Pages is case-sensitive)

#### Issue: 404 errors
**Solutions:**
1. **Check file names** match exactly (index.html, styles.css, script.js)
2. **Verify repository is public**
3. **Check branch settings** in GitHub Pages

### Debug Commands

```bash
# Check if your site is accessible
curl -I https://opensecureai.org

# Check DNS resolution
nslookup opensecureai.org
dig opensecureai.org

# Check SSL certificate
curl -v https://opensecureai.org
```

## 🔄 Updating Your Site

### Making Changes

1. **Edit files locally** or directly on GitHub
2. **Commit changes** to the main branch
3. **GitHub Pages will automatically redeploy** (usually within 1-2 minutes)

### Quick Update Process

**Via GitHub Web:**
1. Go to your repository
2. Click on file to edit
3. Make changes
4. Add commit message
5. Click "Commit changes"

**Via Git Command Line:**
```bash
# Pull latest changes
git pull origin main

# Make your changes
# Edit files...

# Commit and push
git add .
git commit -m "Update landing page content"
git push origin main
```

## 📊 Monitoring and Analytics

### GitHub Pages Analytics
- Go to repository Insights → Traffic
- View page views, unique visitors, and referrers

### Adding Google Analytics
1. **Get Google Analytics tracking ID**
2. **Add to index.html** before closing `</head>` tag:
   ```html
   <!-- Google tag (gtag.js) -->
   <script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
   <script>
     window.dataLayer = window.dataLayer || [];
     function gtag(){dataLayer.push(arguments);}
     gtag('js', new Date());
     gtag('config', 'GA_MEASUREMENT_ID');
   </script>
   ```

## 🚀 Advanced Configuration

### Custom 404 Page
Create `404.html` in repository root for custom error page:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Page Not Found - OpenSecureAI</title>
    <meta http-equiv="refresh" content="5;url=/">
</head>
<body>
    <h1>Page Not Found</h1>
    <p>Redirecting to homepage...</p>
</body>
</html>
```

### Adding Subdirectories
For additional pages:
1. Create folders like `/about/`, `/contact/`
2. Add `index.html` files in each folder
3. Update navigation links accordingly

## 🎯 Next Steps

After successful deployment:

1. **Update README.md** with your actual GitHub repository URL
2. **Add real project links** to replace placeholder GitHub links
3. **Set up contact forms** (consider Netlify Forms or Formspree)
4. **Add team member information**
5. **Implement blog functionality** (consider Jekyll for GitHub Pages)
6. **Set up continuous deployment** with GitHub Actions

## 📞 Support

If you encounter issues:

1. **Check GitHub Pages documentation**: https://docs.github.com/en/pages
2. **Review GitHub Community discussions**
3. **Contact your domain provider** for DNS issues
4. **Open an issue** in your repository for code-related problems

## 🎉 Success Checklist

- [ ] Repository created with all files
- [ ] GitHub Pages enabled
- [ ] Custom domain configured (if applicable)
- [ ] HTTPS enabled
- [ ] Site tested on multiple devices
- [ ] All links working
- [ ] Contact information updated
- [ ] Analytics configured (optional)

Your OpenSecureAI.org landing page is now live and ready to serve the global AI security community!
# Quick Deployment Setup

You have 3 HTML versions:
- **index.html** - Original with Mailchimp
- **index2.html** - Alternative design
- **index3.html** - Latest design with Formspree (RECOMMENDED)

## Step-by-Step Deployment

### Step 1: Choose Your Main Page

**Recommended:** Use index3.html as your main page

Run these commands in your terminal:

```bash
# Navigate to project
cd "c:\Users\saiga\Desktop\tutor\Edutech-sample2"

# Backup current index.html
move index.html index-mailchimp-backup.html

# Make index3.html your main page
copy index3.html index.html

# Check status
git status
```

### Step 2: Set Up Formspree

1. Go to [https://formspree.io/register](https://formspree.io/register)
2. Sign up with: hemaprasanthnaidu@gmail.com
3. Create a new form called "NyTutorr Contact"
4. Copy your form ID (looks like: `abc123xyz`)
5. Open `index.html` in a text editor
6. Find this line:
   ```html
   <form action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
   ```
7. Replace `YOUR_FORM_ID` with your actual ID:
   ```html
   <form action="https://formspree.io/f/abc123xyz" method="POST">
   ```
8. Save the file

### Step 3: Commit Changes

```bash
# Add all changes
git add .

# Commit with message
git commit -m "Setup website for deployment with Formspree contact form"

# Push to GitHub
git push origin main
```

### Step 4: Enable GitHub Pages

1. Go to: https://github.com/saiganesh-d/Edutech-sample2/settings/pages
2. Under "Source":
   - Branch: **main**
   - Folder: **/ (root)**
3. Click **Save**
4. Wait 2-3 minutes
5. Your site will be live at: `https://saiganesh-d.github.io/Edutech-sample2/`

### Step 5: Add Custom Domain (mytutorr.com)

**On GitHub:**
1. Go to: https://github.com/saiganesh-d/Edutech-sample2/settings/pages
2. Under "Custom domain", enter: `mytutorr.com`
3. Click **Save**
4. Wait for DNS check...

**On GoDaddy:**
1. Login to [GoDaddy](https://dcc.godaddy.com/control/portfolio/mytutorr.com/settings?tab=dns)
2. Go to **DNS Settings** for mytutorr.com
3. Delete any existing A or CNAME records for @ and www
4. Add these NEW records:

   **A Records (for root domain):**
   - Type: A, Name: @, Value: `185.199.108.153`, TTL: 600
   - Type: A, Name: @, Value: `185.199.109.153`, TTL: 600
   - Type: A, Name: @, Value: `185.199.110.153`, TTL: 600
   - Type: A, Name: @, Value: `185.199.111.153`, TTL: 600

   **CNAME Record (for www):**
   - Type: CNAME, Name: www, Value: `saiganesh-d.github.io`, TTL: 600

5. Click **Save**
6. **Wait 4-24 hours** for DNS to propagate worldwide

### Step 6: Enable HTTPS

After DNS propagates (4-24 hours):
1. Go back to GitHub Pages settings
2. Check the box: **Enforce HTTPS**
3. Done!

## Testing

**Local Test:**
1. Open `index.html` in your browser
2. Test the contact form
3. Check if you receive email from Formspree

**After Deployment:**
1. Visit: `https://saiganesh-d.github.io/Edutech-sample2/`
2. Test all links and navigation
3. Submit a test form entry
4. Check your email for the submission

**After Custom Domain:**
1. Visit: `https://mytutorr.com`
2. Verify it loads correctly
3. Test form again
4. Check HTTPS is working (green padlock in browser)

## Troubleshooting

**Form submissions not working?**
- Make sure you replaced `YOUR_FORM_ID` with your actual Formspree form ID
- Check Formspree dashboard for submissions

**GitHub Pages not deploying?**
- Check GitHub Actions tab for deployment status
- Make sure `index.html` exists in the root of main branch

**Custom domain not working?**
- DNS can take 4-24 hours to propagate
- Check DNS records in GoDaddy are correct
- Use [DNS Checker](https://dnschecker.org/) to verify: `mytutorr.com`

**HTTPS not available?**
- Wait for DNS to fully propagate first
- Then enable "Enforce HTTPS" in GitHub Pages settings

## Quick Commands Reference

```bash
# Check current status
git status

# Add changes
git add .

# Commit changes
git commit -m "Your message here"

# Push to GitHub
git push origin main

# View git log
git log --oneline -5
```

## Need Help?

Refer to the complete guide: [DEPLOYMENT-GUIDE.md](./DEPLOYMENT-GUIDE.md)

---

**Estimated Timeline:**
- Formspree setup: 5 minutes
- GitHub Pages deployment: 5 minutes
- DNS propagation: 4-24 hours
- **Total: ~24 hours for full deployment**

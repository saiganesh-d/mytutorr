# Netlify Deployment Guide for mytutorr.com

Complete guide to deploy your website on Netlify with custom domain and contact form.

---

## Why Netlify?

- **Free tier with great features**
- **Built-in form handling** (100 submissions/month free)
- **Automatic HTTPS** with custom domain
- **Continuous deployment** from GitHub
- **Better performance** than GitHub Pages
- **No configuration needed** - forms work automatically

---

## Step 1: Push to GitHub (Already Done ✓)

Your repository: https://github.com/saiganesh-d/mytutorr

---

## Step 2: Deploy to Netlify (10 minutes)

### 2.1 Sign Up for Netlify

1. Go to: [https://app.netlify.com/signup](https://app.netlify.com/signup)
2. Click **"Sign up with GitHub"**
3. Authorize Netlify to access your GitHub account

### 2.2 Import Your Repository

1. After signing in, click **"Add new site"** → **"Import an existing project"**
2. Click **"Deploy with GitHub"**
3. Authorize Netlify if prompted
4. Search for and select: **`mytutorr`**

### 2.3 Configure Build Settings

On the deploy settings page:

- **Branch to deploy:** `main`
- **Build command:** (leave empty)
- **Publish directory:** `.` (or leave empty)
- Click **"Deploy site"**

### 2.4 Wait for Deployment

- Netlify will deploy your site (takes 1-2 minutes)
- You'll get a random URL like: `https://random-name-123.netlify.app`
- Test this URL to make sure your site works

---

## Step 3: Set Up Custom Domain (10 minutes)

### 3.1 Add Domain in Netlify

1. In your site dashboard, go to **"Domain settings"**
2. Click **"Add custom domain"**
3. Enter: `mytutorr.com`
4. Click **"Verify"**
5. Netlify will show you need to configure DNS

### 3.2 Configure GoDaddy DNS

1. Login to GoDaddy: [https://dcc.godaddy.com/](https://dcc.godaddy.com/)
2. Go to **My Products** → **mytutorr.com** → **DNS**

3. **Delete ALL existing A and CNAME records**

4. **Add these NEW records:**

   **For Netlify (using their Load Balancer):**

   | Type | Name | Value | TTL |
   |------|------|-------|-----|
   | A | @ | `75.2.60.5` | 600 |
   | CNAME | www | `random-name-123.netlify.app` | 600 |

   **Important:** Replace `random-name-123.netlify.app` with YOUR actual Netlify subdomain!

   **OR use Netlify DNS Nameservers (Recommended):**

   Netlify will show you custom nameservers like:
   - `dns1.p03.nsone.net`
   - `dns2.p03.nsone.net`
   - `dns3.p03.nsone.net`
   - `dns4.p03.nsone.net`

   In GoDaddy:
   - Go to **Domain Settings** → **Nameservers**
   - Click **"Change Nameservers"**
   - Select **"Enter my own nameservers"**
   - Add all 4 Netlify nameservers
   - Click **"Save"**

5. **Save DNS changes**

### 3.3 Wait for DNS Propagation

- **Time:** 4-24 hours (usually 2-6 hours with nameservers)
- Check status: [https://dnschecker.org/](https://dnschecker.org/)
- Enter: `mytutorr.com`

### 3.4 Enable HTTPS in Netlify

1. After DNS propagates, go back to Netlify → **"Domain settings"**
2. Scroll to **"HTTPS"**
3. Click **"Verify DNS configuration"**
4. Netlify will automatically provision SSL certificate
5. **"Force HTTPS"** will be enabled automatically
6. Done! Your site is now secure with HTTPS

---

## Step 4: Configure Contact Form Notifications (5 minutes)

### 4.1 Set Up Email Notifications

1. In Netlify dashboard, go to **"Forms"**
2. Click **"Settings & notifications"**
3. Under **"Form notifications"**, click **"Add notification"**
4. Select **"Email notification"**
5. Configure:
   - **Event to listen for:** New form submission
   - **Email to notify:** `hemaprasanthnaidu@gmail.com`
6. Click **"Save"**

### 4.2 Test the Form

1. Visit your website: `https://mytutorr.com`
2. Fill out the contact form with test data
3. Submit the form
4. Check your email (hemaprasanthnaidu@gmail.com)
5. Also check Netlify dashboard → **"Forms"** to see submission

---

## Form Submission Details

**What happens when someone submits:**
1. User fills form on your website
2. Netlify captures the submission
3. You receive email notification
4. Submission is stored in Netlify dashboard
5. User sees success message

**Form Features:**
- ✅ Spam protection (honeypot + Netlify filters)
- ✅ 100 submissions/month (free tier)
- ✅ Email notifications
- ✅ Export to CSV
- ✅ Zapier/webhook integrations
- ✅ Custom success page (optional)

**Form Fields:**
- Name (required)
- Email (required)
- Phone (required)
- Course Interest (dropdown)
- Message (optional)

---

## Step 5: Configure Continuous Deployment

Already set up! When you push to GitHub, Netlify auto-deploys.

**To update your website:**
```bash
# Make changes to files
git add .
git commit -m "Your update message"
git push origin main
```

Netlify will automatically:
1. Detect the push
2. Build and deploy (1-2 minutes)
3. Your site is updated!

---

## Netlify Dashboard Features

### Site Overview
- **Site URL:** Your live website
- **Deploy status:** See build history
- **Analytics:** Traffic stats (requires upgrade)

### Forms
- View all form submissions
- Export to CSV
- Set up integrations
- Configure notifications

### Domain Settings
- Manage custom domains
- SSL/TLS certificate
- DNS settings
- Redirects

### Deploy Settings
- Auto-publishing
- Deploy previews
- Build hooks
- Environment variables

---

## Free Tier Limits

| Feature | Free Tier |
|---------|-----------|
| Bandwidth | 100 GB/month |
| Build minutes | 300 minutes/month |
| Form submissions | 100/month |
| Concurrent builds | 1 |
| Team members | 1 |
| Sites | Unlimited |

**For most small sites, free tier is plenty!**

---

## Upgrading (Optional)

If you need more:
- **Pro:** $19/month
  - 400 GB bandwidth
  - 1,000 form submissions
  - Analytics
  - Background functions

- **Business:** $99/month
  - Unlimited bandwidth
  - 2,500 form submissions
  - Team collaboration

---

## Custom Success Page (Optional)

Create a custom thank you page after form submission:

1. Create `thank-you.html`:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Thank You - mytutorr</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1E3A8A 0%, #3B82F6 100%);
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            margin: 0;
            text-align: center;
            padding: 20px;
        }
        .container {
            max-width: 600px;
        }
        h1 { font-size: 3rem; margin-bottom: 1rem; }
        p { font-size: 1.2rem; margin-bottom: 2rem; }
        a {
            background: white;
            color: #1E3A8A;
            padding: 12px 30px;
            border-radius: 8px;
            text-decoration: none;
            font-weight: 600;
            display: inline-block;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Thank You! 🎉</h1>
        <p>We've received your message and will get back to you within 24 hours.</p>
        <p>Check your email for confirmation.</p>
        <a href="/">Back to Home</a>
    </div>
</body>
</html>
```

2. Update form in `index.html`:
```html
<form name="contact" method="POST" data-netlify="true" action="/thank-you.html">
```

3. Commit and push:
```bash
git add .
git commit -m "Add custom thank you page"
git push origin main
```

---

## Troubleshooting

### Form not working?
- Check Netlify dashboard → Forms
- Make sure `data-netlify="true"` is in form tag
- Check for `name="contact"` attribute
- Verify honeypot field is present

### Domain not connecting?
- Wait at least 4 hours for DNS propagation
- Verify DNS records in GoDaddy match Netlify instructions
- Use dnschecker.org to verify
- Try using Netlify nameservers instead of A/CNAME

### SSL certificate not provisioning?
- DNS must fully propagate first
- Remove and re-add custom domain
- Wait 10-15 minutes and try again
- Check DNS configuration is correct

### Site not updating after push?
- Check Netlify dashboard → Deploys
- Look for build errors
- Make sure push went to `main` branch
- Try manual deploy from Netlify dashboard

---

## Timeline Summary

| Step | Time |
|------|------|
| Push to GitHub | Done ✓ |
| Deploy to Netlify | 10 min |
| Configure domain | 10 min |
| DNS propagation | 4-24 hours |
| Enable HTTPS | Automatic |
| Configure forms | 5 min |
| **Total** | **~6-24 hours** |

---

## Your Website URLs

- **Repository:** https://github.com/saiganesh-d/mytutorr
- **Netlify URL:** https://your-site.netlify.app (after deployment)
- **Custom Domain:** https://mytutorr.com (after DNS setup)

---

## Support Resources

- **Netlify Docs:** https://docs.netlify.com/
- **Netlify Forms:** https://docs.netlify.com/forms/setup/
- **GoDaddy DNS:** https://www.godaddy.com/help/dns-management-6
- **Netlify Support:** https://answers.netlify.com/

---

## Next Steps After Deployment

- [ ] Test form submissions
- [ ] Set up email notifications
- [ ] Add Google Analytics (optional)
- [ ] Add favicon
- [ ] Submit to Google Search Console
- [ ] Test on mobile devices
- [ ] Share your website!

---

**Your website will be live at https://mytutorr.com after DNS propagation!** 🚀

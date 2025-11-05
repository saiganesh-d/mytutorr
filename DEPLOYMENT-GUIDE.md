# NyTutorr Website Deployment Guide

Complete guide to deploying your website with contact form functionality and custom domain.

---

## Part 1: Contact Form Setup

Your contact form needs a backend to store submissions. Here are 3 options:

### **Option 1: Formspree (RECOMMENDED - Easiest)**

**Pros:** No coding, free tier (50 submissions/month), sends to email
**Cons:** Limited free tier

**Setup Steps:**

1. Go to [https://formspree.io/](https://formspree.io/)
2. Sign up with your email (hemaprasanthnaidu@gmail.com)
3. Click "New Form"
4. Name it "NyTutorr Contact Form"
5. You'll get a form ID like `xyzabc123`
6. In `index3.html`, replace:
   ```html
   <form action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
   ```
   With:
   ```html
   <form action="https://formspree.io/f/xyzabc123" method="POST">
   ```
7. Save and deploy - done!

**How it works:** When someone submits the form, you'll receive an email at hemaprasanthnaidu@gmail.com

---

### **Option 2: Google Sheets (FREE - Unlimited)**

**Pros:** Free, unlimited, data stored in spreadsheet
**Cons:** Requires some setup

**Setup Steps:**

1. Go to [Google Sheets](https://sheets.google.com)
2. Create a new spreadsheet called "NyTutorr Contacts"
3. Add headers: `Name | Email | Course | Message | Timestamp`
4. Click **Extensions** > **Apps Script**
5. Delete existing code and paste:

```javascript
function doPost(e) {
  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    var timestamp = new Date();

    var name = e.parameter.name || '';
    var email = e.parameter.email || '';
    var course = e.parameter.course || '';
    var message = e.parameter.message || '';

    sheet.appendRow([name, email, course, message, timestamp]);

    return ContentService.createTextOutput(JSON.stringify({
      'status': 'success',
      'message': 'Form submitted successfully'
    })).setMimeType(ContentService.MimeType.JSON);

  } catch(error) {
    return ContentService.createTextOutput(JSON.stringify({
      'status': 'error',
      'message': error.toString()
    })).setMimeType(ContentService.MimeType.JSON);
  }
}
```

6. Click **Deploy** > **New deployment**
7. Choose **Web app**
8. Settings:
   - Execute as: **Me**
   - Who has access: **Anyone**
9. Click **Deploy**
10. Copy the Web App URL (looks like: `https://script.google.com/macros/s/ABC123.../exec`)
11. In `index3.html`, replace the form section with the version in `google-sheets-form.html` (see below)

---

### **Option 3: Netlify Forms (FREE - Best Features)**

**Pros:** 100 submissions/month, spam filtering, export to CSV/JSON
**Cons:** Must host on Netlify (not GitHub Pages)

**Setup Steps:**

1. In `index3.html`, just add `data-netlify="true"` to the form:
   ```html
   <form data-netlify="true" name="contact" method="POST">
   ```
2. Deploy to Netlify (see Part 2, Option B)
3. Done! View submissions at Netlify dashboard

---

## Part 2: Hosting Options

### **Option A: GitHub Pages with Custom Domain**

**Pros:** Free, easy, version control
**Cons:** Static only, no server-side processing

**Steps:**

1. **Enable GitHub Pages:**
   ```bash
   # Make sure you're on main branch
   git checkout main

   # Rename index3.html to index.html (your main page)
   git mv index3.html index.html

   # Commit changes
   git add .
   git commit -m "Setup for GitHub Pages deployment"
   git push origin main
   ```

2. **Enable GitHub Pages on Repository:**
   - Go to: https://github.com/saiganesh-d/Edutech-sample2
   - Click **Settings** > **Pages**
   - Source: **Deploy from branch**
   - Branch: **main** / **root**
   - Click **Save**

3. **Wait 2-3 minutes** then visit: `https://saiganesh-d.github.io/Edutech-sample2/`

4. **Add Custom Domain (mytutorr.com):**

   **In GitHub:**
   - Go to **Settings** > **Pages**
   - Custom domain: `mytutorr.com`
   - Click **Save**
   - Check "Enforce HTTPS" (after DNS propagates)

   **In GoDaddy:**
   - Login to [GoDaddy](https://www.godaddy.com)
   - Go to **My Products** > **DNS** for mytutorr.com
   - Add these DNS records:

   | Type  | Name | Value                     | TTL  |
   |-------|------|---------------------------|------|
   | A     | @    | 185.199.108.153          | 600  |
   | A     | @    | 185.199.109.153          | 600  |
   | A     | @    | 185.199.110.153          | 600  |
   | A     | @    | 185.199.111.153          | 600  |
   | CNAME | www  | saiganesh-d.github.io    | 600  |

5. **Wait 24-48 hours** for DNS propagation
6. Visit `https://mytutorr.com` - Done!

---

### **Option B: Netlify (RECOMMENDED for better features)**

**Pros:** Better performance, form handling, auto SSL, custom domain
**Cons:** Different platform than GitHub

**Steps:**

1. **Deploy to Netlify:**
   - Go to [https://app.netlify.com/](https://app.netlify.com/)
   - Sign up with GitHub
   - Click **Add new site** > **Import existing project**
   - Choose **GitHub** > Select `Edutech-sample2`
   - Build settings:
     - Build command: (leave empty)
     - Publish directory: `/`
   - Click **Deploy**

2. **Custom Domain:**
   - In Netlify: **Domain settings** > **Add custom domain**
   - Enter: `mytutorr.com`
   - In GoDaddy DNS, add:

   | Type  | Name | Value                        | TTL  |
   |-------|------|------------------------------|------|
   | CNAME | @    | your-site.netlify.app       | 600  |
   | CNAME | www  | your-site.netlify.app       | 600  |

3. **Enable HTTPS** (automatic in Netlify)

---

## Part 3: Which Option Should You Choose?

### For Contact Form:
- **Easiest:** Formspree (just sign up and get form ID)
- **Most features:** Netlify Forms (but must use Netlify hosting)
- **Free unlimited:** Google Sheets (requires setup)

### For Hosting:
- **Easiest:** GitHub Pages (you're already using GitHub)
- **Best features:** Netlify (better performance + forms)

---

## Recommended Setup

**For beginners:** GitHub Pages + Formspree
**For best experience:** Netlify + Netlify Forms

---

## Quick Start Commands

```bash
# 1. Make index3.html your main page
cd "c:\Users\saiga\Desktop\tutor\Edutech-sample2"
git checkout main

# 2. Rename index3 to index
move index.html index-mailchimp.html
move index3.html index.html

# 3. Commit and push
git add .
git commit -m "Setup for deployment with Formspree contact form"
git push origin main
```

---

## Testing Before Deployment

1. Open `index.html` in your browser locally
2. Fill out the contact form with test data
3. Check if you receive the submission (email for Formspree, spreadsheet for Google Sheets)

---

## Troubleshooting

**Issue:** Form not working
**Fix:** Make sure you replaced `YOUR_FORM_ID` with actual Formspree ID

**Issue:** Custom domain not working
**Fix:** Wait 24-48 hours for DNS propagation, check DNS records in GoDaddy

**Issue:** GitHub Pages not deploying
**Fix:** Check Settings > Pages, make sure main branch is selected

---

## Support

Need help? Contact:
- **Formspree:** https://help.formspree.io/
- **GitHub Pages:** https://docs.github.com/pages
- **Netlify:** https://docs.netlify.com/
- **GoDaddy DNS:** https://www.godaddy.com/help/dns-management-6

---

## Next Steps After Deployment

1. Test the contact form thoroughly
2. Set up Google Analytics (optional)
3. Add favicon (optional)
4. Submit to search engines (Google Search Console)
5. Test on mobile devices
6. Monitor form submissions regularly

---

**Your website will be live at:** `https://mytutorr.com` after DNS propagation!

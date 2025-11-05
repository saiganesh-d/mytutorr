# Exact DNS Records for GoDaddy - mytutorr.com

Your Netlify site: **https://starlit-parfait-9a136b.netlify.app/**

---

## Option 1: Use GoDaddy DNS (Simple A + CNAME)

### Step 1: Login to GoDaddy

Go to: [https://dcc.godaddy.com/](https://dcc.godaddy.com/)

### Step 2: Access DNS for mytutorr.com

1. Click **"My Products"**
2. Find **mytutorr.com**
3. Click **"DNS"** button

### Step 3: Delete Old Records

**Delete these if they exist:**
- Any A records for `@`
- Any CNAME records for `@` or `www`
- Any records pointing to old hosting

### Step 4: Add These EXACT Records

#### Record 1: Root Domain (A Record)

```
Type:  A
Name:  @
Value: 75.2.60.5
TTL:   600 (or 1 Hour)
```

**Click "Add" or "Save"**

#### Record 2: WWW Subdomain (CNAME)

```
Type:  CNAME
Name:  www
Value: starlit-parfait-9a136b.netlify.app
TTL:   600 (or 1 Hour)
```

**Important:**
- ❌ DO NOT include `https://`
- ❌ DO NOT include trailing `/`
- ✅ Just: `starlit-parfait-9a136b.netlify.app`

**Click "Add" or "Save"**

### Step 5: Verify in GoDaddy

Your DNS records should look like this:

```
Type     Name    Value                              TTL
─────────────────────────────────────────────────────────
A        @       75.2.60.5                          600
CNAME    www     starlit-parfait-9a136b.netlify.app 600
```

---

## Option 2: Use Netlify DNS (Recommended - Better Performance)

### Why Netlify DNS is Better:
- ✅ Full CDN optimization on both www and root domain
- ✅ Faster DNS updates
- ✅ No manual record management
- ✅ Better global performance

### How to Switch to Netlify DNS:

#### In Netlify:

1. Go to: [https://app.netlify.com/sites/starlit-parfait-9a136b/settings/domain](https://app.netlify.com/sites/starlit-parfait-9a136b/settings/domain)
2. Scroll to **"Netlify DNS"**
3. Click **"Set up Netlify DNS"** or **"Use Netlify DNS"**
4. Follow the wizard - it will show you 4 nameservers like:
   ```
   dns1.p03.nsone.net
   dns2.p03.nsone.net
   dns3.p03.nsone.net
   dns4.p03.nsone.net
   ```
   (Your actual nameservers may be different - copy them!)

#### In GoDaddy:

1. Go to **Domain Settings** for mytutorr.com
2. Scroll to **"Nameservers"** section
3. Click **"Change"**
4. Select **"Enter my own nameservers (advanced)"**
5. Add all 4 Netlify nameservers (from step above)
6. Remove any existing nameservers
7. Click **"Save"**

#### Wait for Propagation:
- Time: 4-24 hours (usually 6-12 hours)
- After this, Netlify manages ALL DNS automatically

---

## Which Option Should You Choose?

### Choose Option 1 (GoDaddy DNS) if:
- You want to keep DNS management in GoDaddy
- You don't mind slightly less CDN optimization for root domain
- You want quick setup (records take effect in 2-4 hours)

### Choose Option 2 (Netlify DNS) if:
- You want best performance
- You want Netlify to handle everything automatically
- You don't need other DNS records (email, etc.) in GoDaddy
- You're okay with 6-24 hour nameserver propagation

---

## My Recommendation

**Use Option 2 (Netlify DNS)** for best performance and ease of use!

But if you need to keep email or other services in GoDaddy DNS, use Option 1.

---

## Verification

### Check DNS Propagation

After adding records, check propagation:

1. Go to: [https://dnschecker.org/](https://dnschecker.org/)
2. Enter: `mytutorr.com`
3. Select: **A**
4. Click **Search**
5. Should show: `75.2.60.5` worldwide (may take 2-24 hours)

Also check:
- Domain: `www.mytutorr.com`
- Type: **CNAME**
- Should show: `starlit-parfait-9a136b.netlify.app`

### Check in Netlify

1. Go to: [https://app.netlify.com/sites/starlit-parfait-9a136b/settings/domain](https://app.netlify.com/sites/starlit-parfait-9a136b/settings/domain)
2. You should see:
   - ✅ `mytutorr.com` - Awaiting external DNS (then will turn green)
   - ✅ `www.mytutorr.com` - Awaiting external DNS (then will turn green)

### After DNS Propagates

Netlify will automatically:
- ✅ Provision SSL/HTTPS certificate
- ✅ Enable secure connections
- ✅ Redirect HTTP to HTTPS
- ✅ Your site will be live at https://mytutorr.com

---

## Timeline

| Action | Time |
|--------|------|
| Add DNS records in GoDaddy | Now (5 min) |
| DNS starts propagating | Immediate |
| Partial propagation | 2-4 hours |
| Full global propagation | 6-24 hours |
| Netlify detects DNS | After propagation |
| HTTPS certificate issued | Automatic (5-10 min after DNS) |
| Site fully live | 6-24 hours total |

---

## Setting Primary Domain (After DNS Works)

Once DNS is propagated, decide which URL you prefer:

### Option A: Use www.mytutorr.com as primary (Recommended)

In Netlify:
1. Go to Domain settings
2. Find `www.mytutorr.com`
3. Click **"Options"** → **"Set as primary domain"**

Result:
- ✅ https://www.mytutorr.com (primary, full CDN)
- ↪️ https://mytutorr.com (redirects to www)

### Option B: Use mytutorr.com as primary (Current)

Keep as-is. Both URLs work, but root domain has slightly less CDN optimization with A record.

---

## Quick Copy-Paste for GoDaddy

**A Record:**
```
Type: A
Name: @
Value: 75.2.60.5
TTL: 600
```

**CNAME Record:**
```
Type: CNAME
Name: www
Value: starlit-parfait-9a136b.netlify.app
TTL: 600
```

---

## Troubleshooting

### "Domain already registered" error in Netlify
- Domain is already added, you're good! Just configure DNS.

### DNS not propagating after 24 hours
- Double-check records in GoDaddy match exactly
- Make sure there are no conflicting records
- Try removing and re-adding domain in Netlify

### HTTPS not working
- Wait for DNS to fully propagate first
- In Netlify, click "Verify DNS configuration"
- SSL will provision automatically (takes 5-10 min after DNS)

### Form not working after deployment
- Forms should work automatically with `data-netlify="true"`
- Submit a test form
- Check Netlify dashboard → Forms for submissions

---

## Test Your Site

Once DNS propagates:

1. ✅ Visit: https://mytutorr.com
2. ✅ Visit: https://www.mytutorr.com
3. ✅ Check HTTPS is working (green padlock)
4. ✅ Test contact form
5. ✅ Check email for form submission
6. ✅ Test all navigation links

---

## Current Status

- ✅ Repository: https://github.com/saiganesh-d/mytutorr
- ✅ Netlify Site: https://starlit-parfait-9a136b.netlify.app/
- ⏳ Custom Domain: https://mytutorr.com (waiting for DNS)
- ⏳ Form Notifications: Configure after DNS setup

---

## Next: Add Form Email Notifications

After DNS is set up and site is live:

1. Go to: [https://app.netlify.com/sites/starlit-parfait-9a136b/settings/forms](https://app.netlify.com/sites/starlit-parfait-9a136b/settings/forms)
2. Click **"Form notifications"**
3. Click **"Add notification"** → **"Email notification"**
4. Email: `hemaprasanthnaidu@gmail.com`
5. Event: **New form submission**
6. Click **"Save"**

Test the form and check your email!

---

**Your site is live at: https://starlit-parfait-9a136b.netlify.app**

**Just add the DNS records above to make it work at: https://mytutorr.com** 🚀

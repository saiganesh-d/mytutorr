# GoDaddy DNS Setup for Netlify - mytutorr.com

## Best Practice Setup (Recommended)

Since GoDaddy doesn't support ALIAS records, we'll use:
- **Primary domain:** `www.mytutorr.com` (gets full CDN benefits)
- **Root domain:** `mytutorr.com` (redirects to www)

This gives you the best performance and CDN advantages.

---

## Step-by-Step: GoDaddy DNS Configuration

### 1. Login to GoDaddy

Go to: [https://dcc.godaddy.com/](https://dcc.godaddy.com/)

### 2. Access DNS Management

1. Click **"My Products"**
2. Find **mytutorr.com**
3. Click **"DNS"** or **"Manage DNS"**

### 3. Delete Existing Records

**Delete these if they exist:**
- Any A records for `@` (root)
- Any CNAME records for `@`
- Any CNAME records for `www`
- Any other records pointing to old hosting

### 4. Add New DNS Records

Add these **TWO records**:

#### Record 1: Root Domain (A Record)
| Field | Value |
|-------|-------|
| Type | `A` |
| Name | `@` |
| Value | `75.2.60.5` |
| TTL | `600` (or 1 hour) |

**Click "Save"**

#### Record 2: WWW Subdomain (CNAME)
| Field | Value |
|-------|-------|
| Type | `CNAME` |
| Name | `www` |
| Value | `YOUR-SITE-NAME.netlify.app` |
| TTL | `600` (or 1 hour) |

**Important:** Replace `YOUR-SITE-NAME` with your actual Netlify subdomain!
- Example: If your Netlify URL is `https://happy-panda-123.netlify.app`
- Then enter: `happy-panda-123.netlify.app`

**Click "Save"**

---

## Step 5: Configure in Netlify

### Option A: Set WWW as Primary (Recommended)

1. Go to Netlify → **Domain settings**
2. Find **"Primary domain"**
3. If it shows `mytutorr.com`, click **"Options"** → **"Set as primary domain"** on `www.mytutorr.com`
4. This makes `www.mytutorr.com` the primary, and `mytutorr.com` will redirect to it

**Result:**
- ✅ `https://www.mytutorr.com` - Primary (full CDN)
- ↪️ `https://mytutorr.com` - Redirects to www

### Option B: Keep Root as Primary (Current Setup)

If you prefer `mytutorr.com` without www:
1. Keep current setup in Netlify
2. Users can visit both URLs
3. Slightly less CDN optimization (but still works fine)

**Result:**
- ✅ `https://mytutorr.com` - Primary
- ✅ `https://www.mytutorr.com` - Also works

---

## Visual Guide: GoDaddy DNS Records

After setup, your DNS records should look like this:

```
Type    Name    Value                           TTL
────────────────────────────────────────────────────
A       @       75.2.60.5                       600
CNAME   www     your-site.netlify.app           600
```

**Example:**
```
Type    Name    Value                           TTL
────────────────────────────────────────────────────
A       @       75.2.60.5                       600
CNAME   www     happy-panda-123.netlify.app     600
```

---

## Timeline

| Action | Time |
|--------|------|
| Add DNS records in GoDaddy | 5 minutes |
| DNS propagation starts | Immediate |
| Partial propagation | 2-4 hours |
| Full propagation | 6-24 hours |
| HTTPS certificate issued | Automatic (after DNS) |

---

## Verification

### Check DNS Propagation

1. Go to: [https://dnschecker.org/](https://dnschecker.org/)
2. Enter: `mytutorr.com`
3. Check A record shows: `75.2.60.5` globally

Also check:
- Domain: `www.mytutorr.com`
- Type: CNAME
- Should show: `your-site.netlify.app`

### Check in Netlify

1. Go to Netlify → **Domain settings**
2. You should see:
   - ✅ `mytutorr.com` - Netlify DNS verification passed
   - ✅ `www.mytutorr.com` - Netlify DNS verification passed
   - 🔒 **HTTPS** - Provisioning (then will show as active)

---

## Common Issues

### Issue 1: "DNS verification pending"

**Solution:** Wait for DNS propagation (4-24 hours)

### Issue 2: "CNAME not working"

**Solution:**
- Make sure CNAME value is JUST the subdomain: `your-site.netlify.app`
- NOT: `https://your-site.netlify.app` (no https://)
- NOT: `your-site.netlify.app.` (no trailing dot)

### Issue 3: HTTPS not provisioning

**Solution:**
- Wait for DNS to fully propagate first
- In Netlify, click "Verify DNS configuration"
- Remove and re-add custom domain if still not working

---

## Alternative: Use Netlify DNS (Easier!)

If you want to avoid GoDaddy DNS issues, transfer DNS management to Netlify:

### Benefits:
- ✅ Full CDN optimization
- ✅ Faster DNS updates
- ✅ Better performance
- ✅ Automatic configuration

### Steps:

1. In Netlify → **Domain settings** → **Use Netlify DNS**
2. Netlify will show you 4 nameservers like:
   ```
   dns1.p03.nsone.net
   dns2.p03.nsone.net
   dns3.p03.nsone.net
   dns4.p03.nsone.net
   ```

3. In GoDaddy → **Domain Settings** → **Nameservers**
4. Click **"Change"** → **"Enter my own nameservers"**
5. Add all 4 Netlify nameservers
6. Click **"Save"**

7. Wait 4-24 hours for nameserver propagation

**After this:** All DNS is managed in Netlify (much easier!)

---

## What's Your Netlify Subdomain?

To complete the CNAME setup, I need to know your Netlify subdomain.

After deploying to Netlify, you'll see a URL like:
- `https://happy-panda-123.netlify.app`
- `https://magical-unicorn-456.netlify.app`
- `https://mytutorr.netlify.app`

**Use that in the CNAME record!**

---

## Quick Reference Card

**For GoDaddy DNS:**

```
Record 1:
  Type:  A
  Name:  @
  Value: 75.2.60.5
  TTL:   600

Record 2:
  Type:  CNAME
  Name:  www
  Value: [YOUR-NETLIFY-SUBDOMAIN].netlify.app
  TTL:   600
```

**Then wait 4-24 hours for DNS propagation.**

---

## My Recommendation

**Use Netlify DNS (nameservers)** instead of GoDaddy DNS:
- ✅ Easier setup
- ✅ Better performance
- ✅ Full CDN benefits
- ✅ No A record limitations

**OR** if you prefer GoDaddy DNS:
- Set `www.mytutorr.com` as primary in Netlify
- This gives you full CDN benefits even with A record

---

## Need Help?

Share your Netlify subdomain URL and I can give you the exact DNS records to add!

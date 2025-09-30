# DNS Configuration Guide for castnlines.com
## Squarespace + Netlify Setup

### 🎯 Goal: Point castnlines.com to Netlify (where your affiliate site is hosted)

## Step 1: Netlify Site Setup

### A) Deploy Your Site to Netlify First
1. **Go to Netlify.com** and sign in to your personal account
2. **Drag and drop** your `C:\CASTNLINES\castnlines.com\` folder to Netlify
3. **Note your site URL**: Something like `https://amazing-salmon-123456.netlify.app`
4. **Go to Site Settings** → Domain Management
5. **Add custom domain**: castnlines.com

### B) Get Your Netlify DNS Targets
After adding the domain, Netlify will show you:
```
Primary Domain: castnlines.com
DNS Configuration Required:
- A Record: @ → 75.2.60.5
- CNAME Record: www → [your-site-name].netlify.app
```

## Step 2: Squarespace DNS Settings

### A) Access Squarespace DNS Settings
1. **Log into Squarespace** (where you registered castnlines.com)
2. **Go to Settings** → Domains
3. **Click on castnlines.com**
4. **Click "Use External DNS"** (if not already selected)
5. **Go to DNS Settings** or "Advanced DNS"

### B) Required DNS Records in Squarespace

**DELETE any existing A or CNAME records for @ and www first!**

Then ADD these records:

```
Type: A
Host: @
Value: 75.2.60.5
TTL: 3600

Type: CNAME  
Host: www
Value: [your-netlify-site-name].netlify.app
TTL: 3600
```

### C) Example Configuration
If your Netlify site is `castnlines-fishing.netlify.app`, then:

```
A Record:
- Host: @ (or blank)
- Points to: 75.2.60.5

CNAME Record:
- Host: www
- Points to: castnlines-fishing.netlify.app
```

## Step 3: Verification Steps

### A) Check DNS Propagation (takes 24-48 hours)
Use these tools to verify:
- **DNS Checker**: https://dnschecker.org
- **What's My DNS**: https://www.whatsmydns.net
- **Command Line**: `nslookup castnlines.com`

### B) Test Your Site
1. **Wait 30 minutes** after DNS changes
2. **Try both URLs**:
   - https://castnlines.com
   - https://www.castnlines.com
3. **Both should show your fishing lines affiliate site**

## Step 4: Netlify HTTPS Setup

Once DNS is working:
1. **Go back to Netlify** → Site Settings → Domain Management
2. **Enable HTTPS** (Let's Encrypt SSL certificate)
3. **Force HTTPS redirect** (recommended)

## 🔧 Troubleshooting Common Issues

### Issue 1: "Site can't be reached"
**Cause**: DNS not propagated yet
**Solution**: Wait 24-48 hours, check DNS propagation tools

### Issue 2: Shows Squarespace page instead of Netlify
**Cause**: DNS still pointing to Squarespace
**Solution**: Verify A record points to 75.2.60.5, not Squarespace IPs

### Issue 3: SSL certificate error
**Cause**: HTTPS not enabled or DNS not fully propagated
**Solution**: Wait for DNS propagation, then enable SSL in Netlify

### Issue 4: www subdomain not working
**Cause**: Missing or incorrect CNAME record
**Solution**: Ensure CNAME points to your-site.netlify.app (not the custom domain)

## 📋 Quick Checklist

- [ ] Netlify site deployed with working-version.html
- [ ] Custom domain added in Netlify: castnlines.com
- [ ] A record in Squarespace: @ → 75.2.60.5
- [ ] CNAME record in Squarespace: www → [your-site].netlify.app
- [ ] DNS propagation checked (24-48 hours)
- [ ] HTTPS enabled in Netlify
- [ ] Both castnlines.com and www.castnlines.com working

## 🎯 Current Status Check

**To find your exact Netlify site name:**
1. Go to your Netlify dashboard
2. Look at your site URL (something like: `https://peaceful-unicorn-123456.netlify.app`)
3. Use that name (without https://) in your CNAME record

**Your DNS should look like:**
```
castnlines.com A 75.2.60.5
www.castnlines.com CNAME peaceful-unicorn-123456.netlify.app
```

## 💡 Pro Tips

1. **Use Netlify's DNS**: Consider using Netlify DNS instead of Squarespace for easier management
2. **CDN Benefits**: Netlify provides global CDN for faster loading
3. **Deploy previews**: Every code change gets a preview URL
4. **Form handling**: Netlify can handle contact forms without backend code

## Need Help?

**Check these first:**
1. What's your current Netlify site URL?
2. What DNS records currently exist in Squarespace?
3. How long ago did you make the DNS changes?

**Common Commands to Check:**
```powershell
nslookup castnlines.com
nslookup www.castnlines.com
```

Both should eventually point to Netlify's servers (75.2.60.5 or similar).
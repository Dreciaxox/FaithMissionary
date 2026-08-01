# TinaCMS & Vercel Deployment Setup Guide

## Step 1: Local Development Setup (Your Computer)

### 1.1 Install Dependencies
Open your terminal/PowerShell in the project folder and run:
```bash
npm install
```

### 1.2 Start Local CMS
```bash
npm run cms
```

You should see output like:
```
✓ TinaCMS started
✓ Next.js dev server running at http://localhost:3000
```

**Keep this terminal window open** — don't close it.

### 1.3 Access the CMS Editor
Open your browser and go to:
```
http://localhost:3000/admin/
```

You should see a **TinaCMS login screen**. You can now:
- ✅ Edit church info, sermons, events, staff
- ✅ Test the editor before going live
- ✅ Add content without needing TinaCloud credentials

---

## Step 2: Real TinaCloud Setup (Get Live Credentials)

### 2.1 Create a TinaCloud Account
1. Go to https://app.tina.io/
2. Click **"Sign Up"**
3. Sign in with your GitHub account (same one as FaithMissionary repo)
4. Authorize TinaCloud to access your GitHub repos

### 2.2 Create a Project
1. Click **"Create Project"**
2. Search for and select: **`Dreciaxox/FaithMissionary`**
3. Click **"Create"**

TinaCloud will initialize your repo (this takes 1-2 minutes).

### 2.3 Get Your Credentials
Once the project loads:
1. Go to **Settings** (gear icon, top right)
2. Click **"API Tokens"** or **"Client ID"**
3. You'll see two values:
   - **Client ID** (looks like: `abc123def456`)
   - **API Token** (looks like: `xyz789abc123...`)
4. **Copy both** (you'll need these next)

### 2.4 Update Your `.env.local` File
In your project folder, open `.env.local` and replace with:

```
NEXT_PUBLIC_TINA_CLIENT_ID=YOUR_CLIENT_ID_HERE
TINA_TOKEN=YOUR_API_TOKEN_HERE
RESEND_API_KEY=re_test_key_placeholder
```

Example (with fake values):
```
NEXT_PUBLIC_TINA_CLIENT_ID=abc123def456
TINA_TOKEN=xyz789abc123xyz789abc123xyz789
RESEND_API_KEY=re_test_key_placeholder
```

### 2.5 Test with Real Credentials
1. **Stop** the current `npm run cms` (Ctrl+C in terminal)
2. **Start it again:**
   ```bash
   npm run cms
   ```
3. Visit `http://localhost:3000/admin/`
4. Try logging in with Google
5. You should now have full access to edit everything

---

## Step 3: Deploy to Vercel (Go Live)

### 3.1 Create a Vercel Account
1. Go to https://vercel.com
2. Click **"Sign Up"**
3. Choose **"Continue with GitHub"**
4. Authorize Vercel to access your GitHub repos

### 3.2 Import Your Repository
1. Click **"Add New"** → **"Project"**
2. Under "Import Git Repository," find **`Dreciaxox/FaithMissionary`**
3. Click **"Import"**

### 3.3 Add Environment Variables
Before deploying, Vercel needs your TinaCloud credentials:

1. In the import dialog, scroll down to **"Environment Variables"**
2. Add these three variables:

   | Name | Value |
   |------|-------|
   | `NEXT_PUBLIC_TINA_CLIENT_ID` | Your Client ID from Step 2.3 |
   | `TINA_TOKEN` | Your API Token from Step 2.3 |
   | `RESEND_API_KEY` | `re_test_key_placeholder` (or real Resend key if you want email forms) |

3. Click **"Deploy"**

Vercel will now build and deploy your site. This takes 2-5 minutes.

### 3.4 Your Live Site URL
Once deployed, you'll see:
```
✓ Production: https://faithmissionary.vercel.app
```

**Your church website is now live!** 🎉

Visit: https://faithmissionary.vercel.app

### 3.5 Connect Your Custom Domain (Optional)
If you want to use `fmbc.church` instead of `faithmissionary.vercel.app`:

1. In Vercel project settings, go to **"Domains"**
2. Click **"Add"**
3. Enter your domain: `fmbc.church`
4. Vercel will give you DNS records to add to your domain registrar
5. Follow their instructions to connect

---

## Step 4: Auto-Deployment (Automatic from Now On)

After deployment, **every time you:**
- 🖱️ Push changes to GitHub (`main` branch)
- 📝 Edit content in TinaCMS at `/admin/`
- 🖼️ Upload photos

**Your live site automatically updates within 1-2 minutes!**

No manual deployment needed.

---

## Troubleshooting

### "Could not connect to server" (local)
- Make sure `.env.local` exists with `NEXT_PUBLIC_TINA_CLIENT_ID` and `TINA_TOKEN`
- Restart `npm run cms`

### CMS login not working
- Make sure you're logged into GitHub in your browser
- Try incognito/private mode
- Clear browser cache

### Vercel deployment fails
- Check that environment variables are set correctly
- Go to Vercel → Project Settings → Environment Variables
- Verify `NEXT_PUBLIC_TINA_CLIENT_ID` and `TINA_TOKEN` are exact matches

### Site is live but content not showing
- TinaCMS may still be indexing (wait 2-3 minutes)
- Try rebuilding: Vercel → Deployments → Redeploy

---

## Quick Reference: Common Commands

```bash
npm run cms          # Start local editor + preview
npm run start        # Start preview only (no editor)
npm run build        # Build for production
npm run doctor       # Check for issues
npm run setup        # Reconfigure church info
```

---

## Next Steps After Deployment

1. **Add your church logo** → TinaCMS `/admin/` → Site settings
2. **Add staff members** → TinaCMS → Staff collection
3. **Upload sermons** → TinaCMS → Sermons collection
4. **Invite staff to edit** → Share `/admin/` link; they log in with Google
5. **Set up email forms** (optional) → Get Resend API key and add to `.env.local`

---

## Need Help?

- **Local issues?** Run `npm run doctor` to diagnose
- **Deployment issues?** Check Vercel build logs (Deployments tab)
- **CMS not showing data?** Wait 2-3 min for TinaCMS to reindex

**You're all set! Your church site is ready to customize.** 🙏

# Creator Space — Hybrid Hosting Starter

## What this package contains
- `index.html`: small public GitHub Pages entry page.
- `pages/terms.html`: Terms of Service draft.
- `pages/privacy.html`: Privacy Policy draft.

The existing Apps Script project remains the application/backend and Google Sheets remains the database. The public GitHub Pages site provides a stable public website and legal pages for TikTok URL-property verification. This starter does not pretend to contain TikTok's generated verification signature file.

## Before publishing
1. Replace `[NAMA CREATOR / PEMILIK]` and contact email placeholders in both legal pages.
2. In `index.html`, replace `REPLACE_WITH_APPS_SCRIPT_EXEC_URL` with the deployed Apps Script web app URL ending in `/exec`.
3. Create a **public** GitHub repository named `creator-space` (or another name you choose).
4. Upload `index.html` and the `pages` folder to the repository root, commit to `main`.
5. GitHub: Settings → Pages → Deploy from a branch → `main` → `/ (root)` → Save.
6. Wait for GitHub Pages to publish, then open the home, terms, and privacy URLs in an incognito/private browser window to confirm they are public.

## TikTok URL verification
1. In TikTok for Developers, open the app's URL properties / Verify properties section in **Production**.
2. Verify each required URL property (Web/Desktop, Terms of Service, Privacy Policy). TikTok may allow domain or URL-prefix verification.
3. For URL-prefix verification, download the exact signature file TikTok generates for the selected URL prefix.
4. Upload that file to the exact path and filename TikTok specifies. Do not rename it, edit its contents, or create a substitute file.
5. Commit/push it to GitHub Pages. Open the exact verification URL in a browser and ensure it returns the file directly (not a 404, HTML page, or redirect).
6. Return to TikTok and click Verify.

If TikTok provides separate signature files for separate URL prefixes, upload each file to its corresponding exact path. Keep the file contents unchanged.

## Apps Script configuration
The Apps Script deployment should be configured as a Web app:
- Execute as: Me
- Who has access: Anyone (only if the public website needs anonymous access to public data and forms)

Set Script Properties:
- `TIKTOK_CLIENT_KEY`
- `TIKTOK_CLIENT_SECRET`
- `APP_URL` = exact deployed Apps Script `/exec` URL

In TikTok Login Kit → Web, register that exact `/exec` URL as the Redirect URI. TikTok's web redirect URI must be absolute HTTPS, static, and match exactly. Test the redirect URI with the developer console before treating the OAuth integration as production-ready.

## Important integration note
The current starter's UI is served by Apps Script HTML Service. GitHub Pages in this package hosts the public entry/legal pages and TikTok verification file; the Open Creator Space link routes visitors to the Apps Script app. This is the low-risk first hybrid deployment. Moving the full interactive UI onto GitHub Pages and calling Apps Script as a cross-origin API is a separate integration step and must be tested for CORS, request handling, and OAuth callback behavior before switching production traffic.

## Security / policy review before launch
- Replace all legal placeholders with real owner/contact details.
- Confirm the actual data collected matches the Privacy Policy.
- Add spam/rate limiting and moderation for anonymous notes and submissions.
- Do not expose TikTok client secret or session-signing secret in frontend code or GitHub.
- Review local legal requirements and TikTok's current app review rules before submitting.

# Shorts Lab

A single-page tool for pulling your YouTube channel's video performance data into one place, analyzing it, and exporting it - no server, no install, runs entirely in your browser.

Built for creators who want to see retention, engagement, and growth metrics across every video side-by-side, sort by any metric to spot top/bottom performers, and fill in gaps (like swipe-away rate) that YouTube doesn't expose via API.

## Features

- **One-click pull** of every public video on your channel: title, description, publish date, views, retention %, average view duration, like rate, comment rate, subscriber rate, and shares
- **Only public/live videos** - scheduled, private, and unlisted videos are automatically excluded
- **Sortable columns** - click any header to sort ascending/descending, so you can instantly see your best and worst performers by any metric
- **Relative heatmap coloring** - each metric column is color-coded against your own videos (green = strong, red = weak relative to your channel), so patterns jump out visually
- **Manual editing** - click into any cell to correct or fill in data, including metrics YouTube doesn't expose via API (like swipe-away/scroll rate)
- **CSV export** - save your data anytime as a clean CSV
- **CSV import** - reload a previously exported CSV to keep working on it later, with no API calls needed
- **Runs 100% client-side** - your data and Google sign-in token stay in your browser; nothing is sent to any server other than Google's own APIs

## What it can't get automatically

YouTube doesn't expose **swipe-away/scroll rate** through any public or private API - it's only visible in YouTube Studio's per-video analytics graph. The tool leaves this column blank for you to fill in manually for the videos you care about most (usually your top and bottom performers, once you've sorted).

## Setup (one-time, ~10 minutes)

You'll need a free Google Cloud project to get an OAuth Client ID. This is what lets the tool sign in as you and read your channel's data - it does **not** cost anything and does not require using your YouTube channel's Google account specifically (they can be different accounts).

1. Go to [console.cloud.google.com](https://console.cloud.google.com/projectcreate) and create a free project.
2. Go to **APIs & Services → Library**, enable:
   - `YouTube Data API v3`
   - `YouTube Analytics API`
3. Go to **APIs & Services → OAuth consent screen**. Choose **External**, fill in the basic fields (app name, support email, developer email).
4. Under **Test users** (or **Audience**), add the Google account that owns your YouTube channel — this is required while the app is unverified, which is normal for personal-use tools.
5. Go to **APIs & Services → Credentials → Create Credentials → OAuth Client ID**. Choose **Web application**.
6. Under **Authorized JavaScript origins**, add the exact URL where you're hosting this file (e.g. `https://yourusername.github.io` if using GitHub Pages).
7. Copy the **Client ID** (ends in `.apps.googleusercontent.com`) — this is not a secret and is safe to paste into the tool.

## Hosting it with GitHub Pages

1. Push `shorts-lab.html` to a GitHub repo.
2. Go to **Settings → Pages**.
3. Under **Source**, choose **Deploy from a branch**, select your main branch and `/ (root)`, then **Save**.
4. After a minute or two, your live URL will appear, e.g.:
   `https://yourusername.github.io/your-repo-name/shorts-lab.html`
5. Register that origin (just `https://yourusername.github.io`, no path) in your OAuth Client's Authorized JavaScript origins.

## Using it

1. Open the hosted page.
2. Paste your OAuth Client ID and click **Connect to YouTube**.
3. Sign in with the Google account that owns your channel. You'll likely see an "unverified app" warning — click **Advanced → Go to Shorts Lab (unsafe)** to proceed. This is expected for personal-use tools that haven't gone through Google's public verification process.
4. Click **Fetch all my videos**.
5. Click any column header to sort, click any cell to edit it, and use **Export CSV** to save your results.

## Privacy

All data processing happens locally in your browser. Your Google sign-in token and video data are never sent to any third-party server — only to Google's own APIs, directly from your browser.

## Limitations

- YouTube's free API quota (10,000 units/day by default) applies, but this tool is designed to use very few calls regardless of channel size — it batches video lookups and pulls all analytics data in a single query rather than looping per video.
- Swipe-away/scroll rate must be added manually per video (see above).
- Requires a one-time Google Cloud setup; there's no way around this since it's what authorizes the tool to read your channel's private analytics.

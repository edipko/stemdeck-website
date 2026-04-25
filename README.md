# StemDeck — marketing site

Static site that ships:
- Product landing page (hero, features, pricing, comparison, CTA)
- Privacy policy (`/privacy`)
- Terms of use (`/terms`)

Hosted on Firebase Hosting alongside the other Edipko sites. No build step — just plain HTML + Tailwind via CDN. Edit, save, deploy.

## Layout

```
public/
├── index.html         landing page
├── privacy.html       privacy policy (linked from app + Mac App Store listing)
├── terms.html         terms of use
├── style.css          minor extras Tailwind utilities can't express
└── images/            screenshots, app icon, OG images (drop in here)
firebase.json          Firebase Hosting config
.firebaserc            Firebase project alias — set this to your project ID
```

## Update `.firebaserc`

`.firebaserc` currently aliases `default` to `stemdeck-site`. Replace with whatever
your Firebase project is actually called:

```json
{ "projects": { "default": "<your-firebase-project-id>" } }
```

## Local preview

Easiest:

```sh
cd public && python3 -m http.server 8000
```

Open http://localhost:8000.

Or with the Firebase CLI (gives you the same routing rules as production):

```sh
firebase emulators:start --only hosting
```

## Deploy

```sh
firebase login              # one time
firebase deploy --only hosting
```

That's it. Pages publish in 30–60 seconds.

## Where this site connects to the rest of the project

- The Mac app's **App Store listing** points its **support URL** and **marketing URL**
  at `/privacy` and `/` respectively (or wherever you'd like — pushed via the App Store
  Connect API in `STEMDECK/scripts` once we move them out of `/tmp`).
- The Mac app's in-app **paywall** links to `/terms` and `/privacy` for the
  Apple-required disclosures.

## Editing checklist

When you change the listing URL or any legal text:

- [ ] Update `Last updated:` date at the top of the policy/terms.
- [ ] Re-deploy.
- [ ] If pricing or subscription terms changed in the app, update both the **app's**
      App Store listing description AND the website's pricing section so they match —
      Apple cross-checks during review.

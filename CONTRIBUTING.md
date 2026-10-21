# Contributing to Homekeep

Thanks for helping. Homekeep is a single-file web app (`index.html`), so there is no build step.

## Run it locally

```bash
git clone https://github.com/<your-username>/homekeep.git
cd homekeep
python3 -m http.server 8080
```

Open http://localhost:8080. Manual entry, dates, renewal links and browser storage all work locally. Bill scanning and account sync only work inside Claude (see the README).

## Good first contributions

- **Add a brand.** Edit the `DEVS` list (devices) or `SUBS` list (subscriptions) near the top of the script in `index.html`. Each entry is `['keyword', 'https://official-support-or-account-page']`.
- Only link to the company's own domain. Open the page and confirm the address bar shows the real brand domain before you submit.
- Prefer the page where a customer manages billing or books service, not the home page.
- Report a wrong or dead link with the "Broken official link" issue template.

## Pull requests

1. Fork and create a branch.
2. Keep the change small and focused.
3. Test in a light and a dark theme and at phone width (about 400px).
4. Describe what changed and why.

## Code style

- Plain JavaScript, no frameworks, no build tools.
- Colors come from CSS variables defined at the top of the file. Do not add literal colors in components.
- Never put user data in the repo. Example entries in the app are clearly marked and invented.

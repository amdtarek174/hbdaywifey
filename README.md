# Happy Birthday, Nada

A single-page countdown to **30 September 2026**, with a new love note revealed every day.

Live page: `https://amdtarek174.github.io/hbdaywifey/`

## What it does

- Live countdown in days, hours, minutes and seconds.
- One message per day, revealed in order, so the final teasers land right before the birthday.
- A special birthday message that takes over automatically at midnight on 30 September.
- An expandable list of every note revealed so far.
- Floating hearts, script display font, rose and gold theme.

Everything lives in `index.html`. No build step, no dependencies, no tracking.

## Run it locally

Just open `index.html` in a browser. That's it.

If you prefer a local server:

```bash
python -m http.server 8000
# then open http://localhost:8000
```

## How to change things

Open `index.html` and look inside the `<script>` block near the bottom.

| What | Where |
| --- | --- |
| The date | `var TARGET = new Date(2026, 8, 30, 0, 0, 0, 0);` — months are 0-based, so `8` is September |
| The daily messages | the `MESSAGES` array, one string per day, in order |
| The birthday message | `BIRTHDAY_MESSAGE` |
| The signature | search for `always yours` in the HTML |
| Colours and fonts | the `:root` variables at the top of the `<style>` block |

The message shown each day is picked by how many days are left, so the **last** item in
`MESSAGES` is the one that shows the night before the birthday. Add more messages to the
front of the list if you want the countdown notes to start earlier.

## Deployment

Pushing to `main` triggers `.github/workflows/deploy.yml`, which publishes the repo root
to GitHub Pages.

One-time setup in the repo:

1. Go to **Settings → Pages**.
2. Under **Build and deployment → Source**, choose **GitHub Actions**.
3. Push to `main` (or run the workflow manually from the **Actions** tab).

The workflow uses GitHub's first-party actions pinned to major version tags. For stricter
supply-chain hygiene you can pin each `uses:` line to a full commit SHA instead.

## Accessibility notes

- The countdown numbers are hidden from screen readers (they change every second) and a
  calmer summary is announced once a minute instead.
- All animation is disabled when the reader has `prefers-reduced-motion` set.
- The page still reads well if the Google Fonts request is blocked; local fallback fonts
  are declared.

# theskcreative — portfolio site

A single-file, fully responsive rebuild of theskcreative.com, set up for GitHub Pages and built to double as a job-search + freelance landing page.

## What's here
- `index.html` — the entire site (HTML + CSS + JS in one file, no build step, no dependencies to install)
- `assets/img/logo.svg` — your SK mark, used as the nav logo, favicon, hero watermark, and the custom cursor
- `assets/` — put your resume PDF and any other local images here (see "Before you launch" below)

## New interactive additions
- **Custom rotating cursor** — a magenta dot plus a ring built from your SK logo that spins continuously and trails the mouse. It scales up and shows a contextual label ("View", "Open", "Download"...) on hover. Automatically disabled on touch devices and when the visitor has "reduce motion" turned on, so it never gets in the way.
- **Magnetic buttons** — the hero buttons pull gently toward the cursor as you approach them.
- **Tilted project cards** — the work grid tilts in 3D toward the cursor on hover.
- **Staggered hero entrance** — headline, tagline and buttons fade/slide in one after another on load.
- **Count-up stat** — "20+ projects shipped" counts up when it scrolls into view.
- **Rotating logo watermark** — a large, faint version of your SK mark slowly spins in the hero background.
- **Your photo in About** — currently pulling the illustrated portrait from your existing About page, with a duotone (lime/magenta) hover treatment that matches the work grid.
- **Self-contained project lightbox** — clicking a work card no longer sends people to a `theskcreative.com/?portfolio=...` WordPress page. It opens a modal right on this page, with the image, title and category. Nothing about the work grid depends on WordPress being online anymore.

## ⚠️ One thing still tied to WordPress: the images themselves
Removing the links fixed where the *clicks* go, but the actual image files (`src="..."`) for the work grid and the About photo are still pulled live from `theskcreative.com/wp-content/uploads/...`. That's your WordPress media library — if you shut down WordPress hosting entirely, those images will stop loading even though the links no longer point there.
**Before you shut WordPress down:** download every image used in the site (12 work thumbnails + the About portrait — full list below) and put them in `assets/img/`, then update each `src="..."` in `index.html` to `assets/img/filename.jpg`. Do this first, confirm the site still looks right with WordPress switched off, then cancel hosting.

## Before you launch — 4 things to swap in
1. **Email** — replace `hello@theskcreative.com` (appears twice) with your real inbox.
2. **Resume PDF** — add your CV as `assets/Siddharth-Kansara-Resume.pdf`, or update the two `href="assets/Siddharth-Kansara-Resume.pdf"` links to wherever you host it.
3. **Contact form** — the form currently posts to a placeholder Formspree endpoint (`action="https://formspree.io/f/your-form-id"`). GitHub Pages can't run server code, so you need a free form backend:
   - Go to [formspree.io](https://formspree.io), create a free form, copy the ID it gives you (looks like `xzbqjkvn`).
   - Replace `your-form-id` in `index.html` with that ID.
   - Alternative: skip the form entirely and just keep the `mailto:` link — delete the `<form>` block if you'd rather keep it simple.
4. **Download the images before you cancel WordPress hosting** — these are the exact files currently hotlinked (right-click → Save Image As, or download from your WordPress media library):
   - `wp-content/uploads/2025/03/Siddharth_Kansara_-with_blur_dessert-scaled.jpg` — Dessert Photography
   - `wp-content/uploads/2025/03/b2b1e8ea-e1e7-42bf-a02c-153778ba56aa-1024x768.jpg` — Desi Nibbles Chips
   - `wp-content/uploads/2025/03/logo_playmax-1024x1024.jpg` — Playmax Gaming
   - `wp-content/uploads/2025/03/1024_Icon.png` — Word Search UI
   - `wp-content/uploads/2025/03/1024_Wood_block_puzzles.png` — Wood Block UI
   - `wp-content/uploads/2025/03/Portraits-1024x576.jpg` — Portraits
   - `wp-content/uploads/2025/03/video1-1024x576.jpg` — Gatsby Studio
   - `wp-content/uploads/2025/03/CAP-946x1024.jpg` — Capette Fashion Booklet
   - `wp-content/uploads/2024/12/packaging11-1024x801.jpg` — Pinook
   - `wp-content/uploads/2024/12/logoxploture-1024x1024.jpg` — Xplotur Logo
   - `wp-content/uploads/2024/12/Screenshot-2024-12-12-224645-1024x460.png` — Electrowave
   - `wp-content/uploads/2024/12/1b612c62-616b-4faf-9358-991a28a31dc5-1024x682.jpg` — Tajin Ads Campaign
   - `wp-content/uploads/2025/02/Vector-Smart-Object-938x1024.png` — About portrait

   Save them into `assets/img/`, then in `index.html` replace each matching `src="https://theskcreative.com/wp-content/uploads/..."` with `src="assets/img/filename"`. There are two `src` attributes per work item (one in the visible thumbnail, one in `data-img` for the lightbox) — update both.
5. **Project count** — the hero stat is hardcoded to "20+ projects shipped" (`data-count="20"` on the `<span class="count-up">`). Update the number as your portfolio grows.

## Publishing to GitHub Pages
1. Create a new repository on GitHub — name it `theskcreative` (or anything you like).
2. Upload `index.html` (and your `assets/` folder) to the repo — either drag-and-drop on github.com, or:
   ```bash
   git init
   git add .
   git commit -m "Launch portfolio site"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/theskcreative.git
   git push -u origin main
   ```
3. In the repo, go to **Settings → Pages**.
4. Under **Build and deployment**, set **Source** to `Deploy from a branch`, branch `main`, folder `/ (root)`. Save.
5. GitHub gives you a live URL like `https://YOUR-USERNAME.github.io/theskcreative/` within a minute or two.

## Pointing theskcreative.com at GitHub instead of GoDaddy
You can keep your existing domain and just change where it points:
1. In the GitHub repo **Settings → Pages → Custom domain**, enter `theskcreative.com` and save — this creates a `CNAME` file in your repo automatically.
2. In your GoDaddy DNS settings, update the records:
   - Add an **A record** for `@` pointing to GitHub's Pages IPs: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - Add a **CNAME record** for `www` pointing to `YOUR-USERNAME.github.io`
3. Back in GitHub Pages settings, tick **Enforce HTTPS** once the DNS change has propagated (can take a few hours).
4. You can cancel/downgrade the GoDaddy website builder once the new site is live — just keep the domain registration itself if you're happy with it.

## Notes on the design
- CMY(K) accent colours (cyan / magenta / yellow) and the registration-mark crosshair motif are a nod to print production — your own craft (packaging, branding proofs) — rather than a generic template palette.
- Fully responsive: single-column mobile layout, hamburger nav, fluid type sizing.
- No frameworks — plain HTML/CSS/JS, so it's easy to edit by hand or hand off to any developer later.
- Work grid has category filtering (Branding / Packaging / UI-UX / Photography / Video) driven by `data-cat` attributes on each card — add new projects by copying a `<a class="card">` block and setting its category + link.

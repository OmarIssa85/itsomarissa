# itsomarissa — AI Creative portfolio

A single-page portfolio site. **No build step** — it runs anywhere.

- `index.html` — the design + code (rendering engine).
- `content.json` — all your editable content (text, projects, images, links).
- `.pages.yml` — config for the visual editor (Pages CMS).
- `images/`, `videos/` — your media files.

---

## 1. Editing your content — two ways

### A) Visual editor (easiest — drag & drop)
Go to **https://app.pagescms.org**, sign in with GitHub, and open the **`itsomarissa`** repo.
You get forms for every section: drag-drop image uploads, add/remove/reorder items, edit text,
then **Save** — it publishes to your live site automatically. Nothing to install.

### B) By hand
All content lives in **`content.json`**. Open it (on GitHub or locally), edit the text between
the quotes, or add/remove an item by copying a `{ ... }` block. Commit, and the site updates.
You never need to touch `index.html` — that's the design/code, kept separate on purpose so
editing content can never break the layout.

### Common edits (by hand, in `content.json`)
| I want to… | Do this |
|---|---|
| Change the headline | Edit `hero.headlineHTML`. Wrap a word in `<span class="serif">word</span>` to make it an italic accent. |
| Add a project | Copy a `{ ... }` block inside `work`. Set `type` to `"video"`, `"image"`, or `"both"`, and `span` to `"c-4"` / `"c-6"` / `"c-8"` (tile width). |
| Add a video or still | Copy a block inside `videos` or `images`. |
| Use a real photo instead of a gradient | Add `"img": "images/photo.jpg"` to any project/video/image block. |
| Update your email | Edit `contact.email`. |

### Common edits
| I want to… | Do this |
|---|---|
| Change the headline | Edit `hero.headlineHTML`. Wrap a word in `<span class="serif">word</span>` to make it an italic clay accent. |
| Add a project | Copy a line inside `work: [ ... ]`. Set `type` to `"video"`, `"image"`, or `"both"`, and `span` to `"c-4"` / `"c-6"` / `"c-8"` (tile width). |
| Add a video or still | Copy a line inside `videos: [ ... ]` or `images: [ ... ]`. |
| Use a real photo instead of a gradient | Add `img: "https://…/photo.jpg"` to any project/video/image line. |
| Update your email | Edit `contact.email`. |
| Add social links | Fill in the URLs under `contact.socials`. Leave a value as `""` to hide that icon. |
| Change bio / stats | Edit the `about` block. |

Save, refresh the page in your browser, and you'll see the change. To preview locally,
just double-click `index.html` (or run `python3 -m http.server` in this folder and open
http://localhost:8000).

---

## 2. Hosting it (GitHub Pages + your domain)

This is the recommended path: free, Git-based, and it auto-publishes every change.

### One-time setup
1. Create a **free GitHub account** if you don't have one, and create a new **empty repository** (e.g. `portfolio`).
2. In this folder, connect it and push (replace the URL with your repo's):
   ```bash
   git remote add origin https://github.com/YOUR-USERNAME/portfolio.git
   git branch -M main
   git push -u origin main
   ```
3. On GitHub: **Settings → Pages → Build and deployment → Source: Deploy from a branch**,
   pick **main / (root)**, Save. Your site goes live at `https://YOUR-USERNAME.github.io/portfolio/`.

### Connect your domain
1. GitHub → **Settings → Pages → Custom domain** → type your domain (e.g. `itsomarissa.com`) → Save.
   This creates a `CNAME` file in the repo — keep it.
2. At your **domain registrar's DNS settings**, add:
   - Four `A` records for the root domain pointing to GitHub's IPs:
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - One `CNAME` record for `www` pointing to `YOUR-USERNAME.github.io`
3. Back in GitHub Pages, tick **Enforce HTTPS** once it's available (can take a few minutes to an hour).

> Prefer Cloudflare Pages or Netlify instead? Both also connect to this same repo,
> auto-deploy on push, and support custom domains — pick whichever you like. The repo
> works with all of them unchanged.

---

## 3. Updating after it's live

Because it's a Git repo, every version is saved and nothing is ever lost.

- **You edit content:** change `CONTENT` in `index.html`, then:
  ```bash
  git add index.html
  git commit -m "Update projects"
  git push
  ```
  The live site updates automatically within a minute or two.

- **Claude edits the design/code for you:** point Claude at this folder (or paste the
  current `index.html`). Claude changes only the code below the `██ ENGINE ██` line and
  leaves your `CONTENT` block untouched, so your content is never lost. Then commit & push
  the same way.

If something ever looks wrong, `git log` shows every version and you can roll back.

---

## Files
- `index.html` — the entire site (content + design + code).
- `README.md` — this guide.
- `.gitignore` — housekeeping (ignores OS junk files).

# PHYS 5211 Course Site

Static course website for **PHYS 5211: Introduction to Scientific Computing in the Era of AI**, Northeastern University, Fall 2026.

## Structure

```
index.html          Home page (hero, philosophy, schedule, resources)
syllabus.html        Full syllabus
css/style.css        All styling — one shared stylesheet
data/lectures.json   The lecture schedule data. Edit this each week.
notes/template.html  Copy this to create a new lecture note page
notes/lecture-01.html, lecture-02.html   Example / real lecture notes
assets/              Photos and images go here
```

## Math rendering (KaTeX)

Lecture note pages render math automatically via [KaTeX](https://katex.org),
loaded from a CDN — no local font files or build step needed. Write inline
math as `$x^2$` and display equations as `$$x^2$$` directly in your HTML;
the script at the bottom of `template.html` finds and renders them after
the page loads. Don't remove the three KaTeX `<link>`/`<script>` tags when
duplicating the template.

## Adding a new lecture's notes (weekly workflow)

1. Copy the template:
   ```
   cp notes/template.html notes/lecture-03.html
   ```
2. Open `notes/lecture-03.html` and replace the bracketed placeholders
   (title, date, topic area, objectives, content). Fix the "Previous
   lecture" / "Next lecture" links at the bottom to point at the
   adjacent lecture files.
3. Also fix the **previous** lecture's "Next lecture" link so it now
   points at your new page instead of the template.
4. Open `data/lectures.json` and either add a new entry or update an
   existing `"upcoming"` / `"tba"` entry to `"posted"` with the correct
   `notesUrl`. Example:
   ```json
   {
     "session": 3,
     "date": "Wed, Sep 9",
     "title": "Error Analysis, Conditioning & Stability",
     "topic": "Foundations",
     "status": "posted",
     "notesUrl": "notes/lecture-03.html"
   }
   ```
5. Commit and push (see below). The home page schedule table reads
   this JSON file automatically — no other file needs to change.

## Publishing with GitHub Pages

**One-time setup:**

1. Create a new repository on GitHub (e.g. `phys5211-fall2026`). Public
   repos get free Pages hosting; a private repo needs GitHub Pro/Team/Enterprise
   to publish a Pages site from it.
2. From inside this folder on your computer, initialize git and push:
   ```bash
   git init
   git add .
   git commit -m "Initial course site"
   git branch -M main
   git remote add origin https://github.com/<your-username>/phys5211-fall2026.git
   git push -u origin main
   ```
3. On GitHub, go to the repo's **Settings → Pages**.
4. Under "Build and deployment," set **Source** to "Deploy from a branch."
5. Set **Branch** to `main` and folder to `/ (root)`, then **Save**.
6. GitHub will give you a URL, usually:
   ```
   https://<your-username>.github.io/phys5211-fall2026/
   ```
   It can take a minute or two to go live the first time.

**Every week after that**, updating the site is just:
```bash
git add .
git commit -m "Add lecture 3 notes"
git push
```
GitHub Pages redeploys automatically within a minute of the push — no
extra steps needed.

## Adding your own photos

Drop image files into `assets/` and reference them with a relative
path, e.g. `<img src="../assets/room-207.jpg" alt="...">` from a page
inside `notes/`, or `<img src="assets/room-207.jpg" alt="...">` from
`index.html`.

## Customizing colors and fonts

Everything visual lives in `css/style.css` as CSS variables at the top
of the file (`--navy`, `--gold`, `--teal`, `--rust`, `--serif`,
`--sans`). Change a value there and it updates across every page.

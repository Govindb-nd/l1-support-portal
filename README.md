# L1 Support Portal

A single-page triage console for Netradyne CS Technical Support: a categorized
troubleshooting questionnaire (all questions in a branch surface at once, not
one at a time) plus a Best Practices & Updates feed. No backend — it's a
static page that reads its content from three JSON files in this repo.

## Structure

```
l1-support-portal/
  index.html          the whole app (markup, styles, logic)
  data/
    categories.json    the 5 issue categories shown as tiles
    nodes.json          every question / resolution / escalation node
    posts.json          Best Practices & Updates feed items
```

## Preview it locally before pushing

Opening `index.html` directly by double-clicking it will NOT work — browsers
block `fetch()` of local files under `file://`. Serve it over a tiny local
web server instead, from inside this folder:

```
cd l1-support-portal
python3 -m http.server 8000
```

Then open `http://localhost:8000` in your browser. Ctrl+C to stop the server
when you're done.

## Push this to GitHub

From inside this folder:

```
git init
git add .
git commit -m "Initial L1 support portal"
git branch -M main
git remote add origin https://github.com/<your-account>/l1-support-portal.git
git push -u origin main
```

(Replace `<your-account>` with wherever you created the repo — your personal
account for now, or the `netradyne` org later if that access clears up.)

If you'd rather not use the command line: create the repo on github.com first
(Public visibility, no README/gitignore/license so it stays empty), then use
the "uploading an existing file" link on the empty repo's page to drag-and-drop
this whole folder's contents in through the browser instead of running git
commands.

## Turn on GitHub Pages

1. On the repo's GitHub page, go to **Settings → Pages**.
2. Under "Build and deployment", set **Source** to "Deploy from a branch".
3. Set **Branch** to `main` and folder to `/ (root)`, then Save.
4. GitHub will show your live URL (usually
   `https://<your-account>.github.io/l1-support-portal/`) within a minute or
   two.

## Publishing a content edit (no-code, for SMEs/managers)

1. Open the live site, switch the top-right toggle to **Edit preview**.
2. Make your changes — add/edit categories, insert or edit questions, publish
   or edit Best Practices & Updates posts. Changes update the page
   immediately, but only in your own browser.
3. Click **Download updated data**. Three files land in your Downloads
   folder: `categories.json`, `nodes.json`, `posts.json`.
4. On the repo's GitHub page, open the `data` folder, click into each file,
   click the pencil (edit) icon, and paste in the corresponding downloaded
   file's contents — or use "Add file → Upload files" and drag all three in
   at once to replace them, then commit.
5. GitHub Pages redeploys automatically. Refresh the live site in ~30–60
   seconds to see the change.

Note: the Reader / Edit preview toggle is a UI convenience, not real access
control — anyone visiting the public page can switch to Edit preview and see
the forms. It doesn't let them change what's actually published; only
someone who can commit to this repo can do that. Keep that in mind if this
ever needs enforced per-person permissions (that would mean adding real
sign-in, e.g. Microsoft Entra ID via MSAL.js, as a later step — not required
for this POC).

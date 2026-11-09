# IFDAR companion website

This public repository maintains <https://ifdar-book.org/> and the reader
datasets and scripts for *Introduction to Forestry Data Analysis with R*.
The full online book is hosted separately at
<https://www.finley-lab.com/ifdar/>.

The manuscript, build inputs, and development history are maintained in the
private `finleya/IFDAR-source` repository. This repository contains the public
website and reader resources only.

## Files to maintain

- `docs/index.html`: landing-page text, links, styling, and theme toggle.
- `docs/cover.png`: book cover displayed on the landing page.
- `docs/CNAME`: the custom domain, `ifdar-book.org`.
- `releases/IFDAR_book.zip`: downloadable reader datasets and R scripts.

Keep the website branch named `master`: the existing download URL includes
that branch name:

<https://github.com/finleya/IFDAR/raw/master/releases/IFDAR_book.zip>

## Edit and publish

Clone this repository on a new machine:

```sh
git clone --branch master git@github.com:finleya/IFDAR.git
cd IFDAR
```

On Andrew's current machine, the existing website checkout is
`/home/andy/projects/FD20-book/FD25-git/www/ifdar`.

From the website checkout, pull the latest changes before editing:

```sh
git status --short --branch
git pull --ff-only origin master
```

Edit `docs/index.html`. This is a static HTML page; no book compilation is
needed. To preview it locally:

```sh
python3 -m http.server 8000 --bind 127.0.0.1 --directory docs
```

Open <http://127.0.0.1:8000/> in your browser, then press Ctrl+C in the terminal
to stop the preview server. The dataset link uses GitHub, so it downloads the
published archive rather than a local replacement.

Review, commit, and push the intended changes:

```sh
git diff
git add docs/index.html
git commit -m "Update book website"
git push --no-follow-tags origin refs/heads/master:refs/heads/master
```

Stage `docs/cover.png` or `releases/IFDAR_book.zip` explicitly when updating those
files. Keep private manuscript branches and tags in `IFDAR-source`.

## GitHub Pages configuration

In this repository's **Settings → Pages**, configure:

- **Source:** Deploy from a branch.
- **Branch:** `master`.
- **Folder:** `/docs`.
- **Custom domain:** `ifdar-book.org`.
- **Enforce HTTPS:** enable once the certificate is available.

When restoring this site after the repository split, remove the custom domain
from the renamed `IFDAR-source` repository's Pages settings before assigning it
here, if it is still assigned there. The `CNAME` file alone does not configure
the new repository's Pages settings.

With Pages configured, pushes to `master` publish the website. Check deployment
status in GitHub's **Actions** tab, and verify both the site and the ZIP link in
a signed-out browser. The public site does not require readers to sign in.

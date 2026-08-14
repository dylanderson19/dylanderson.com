# dylanderson.com — wireframe

A static portfolio wireframe modeled on baker.studio. No build step, no
dependencies — plain HTML/CSS/JS that works on any host, including GoDaddy.

## Structure

```
index.html            Homepage — full-bleed hero carousel (4s per slide,
                      0.5s crossfade); each slide links to its project subpage
work.html             Work index — grid of project cards
work/
  project-01.html …   One subpage per project
journal.html          Journal index — dated list of posts
journal/
  post-01.html …      One subpage per post
about.html            Portrait + biography
contact.html          Big email link + socials
css/style.css         ALL styling lives here (one file, shared by every page)
assets/               Your images go here (see below)
```

The header on every page has hover dropdowns under **Work** and **Journal**
listing the subpages (same font, lighter value). The top-level links still go
to the index pages, so navigation works on touch devices too.

## Populating with assets

Every gray crosshatched box is a placeholder. Its label tells you the suggested
file path and size. Drop your images into `assets/`:

```
assets/
  signature.png   ← your name/signature logo in the header (all pages).
                    A placeholder is included; overwrite it with your own —
                    transparent background, any width, displays 26px tall
                    (export ~52px+ tall for retina)
  project-01/  hero.jpg (2400×1350)  detail-1.jpg  detail-2.jpg
  project-02/  hero.jpg              detail-1.jpg  detail-2.jpg
  project-03/  hero.jpg              detail-1.jpg  detail-2.jpg
  project-04/  hero.jpg              detail-1.jpg  detail-2.jpg
  about/       portrait.jpg (1200×1600)
  journal/     post images (any size)
```

Then replace a placeholder like this:

```html
<!-- before -->
<div class="ph hero"><span>Hero — …</span></div>

<!-- after -->
<div class="ph hero"><img src="assets/project-01/hero.jpg" alt="Project Title 01"
     style="width:100%;height:100%;object-fit:cover"></div>
```

**Important:** pages inside `work/` and `journal/` are one folder deep, so their
image paths start with `../` (e.g. `../assets/project-01/hero.jpg`). Each
subpage has a comment at the top showing the exact snippet. On the homepage
carousel the img also needs `position:absolute;inset:0;`.

Also update: project titles/categories, the lorem ipsum text, the About bio,
and the social links on Contact.

## Adding a project (or journal post)

1. Duplicate a subpage — e.g. copy `work/project-04.html` → `work/project-05.html`
   and edit its title, meta, text, and asset paths.
2. Add a card for it on `work.html` (copy an existing `<a class="card">` block).
3. Homepage: copy a `<a class="slide">` block in `index.html` and update the
   `/ 04` total in the counter.
4. Add one line to the Work dropdown in the header of **every** page (it's the
   same `<div class="dropdown">` block everywhere — find & replace across files
   works well).

Journal posts are the same minus step 3.

## Styling

Everything visual lives in `css/style.css`, including:

- Carousel crossfade duration → the `transition:opacity .5s` on `.slide`
  (the 4-second slide interval is in the script at the bottom of `index.html`)
- Dropdown color/spacing → the `.dropdown` rules
- Placeholder look → the `.ph` rules

## Publishing to dylanderson.com (GoDaddy)

Upload the contents of this folder (keeping the folder structure) to your
hosting's web root (often `public_html`) via GoDaddy's file manager or FTP. If
you don't have a hosting plan attached to the domain, alternatives like GitHub
Pages, Netlify, or Vercel are free for static sites — you'd point the domain's
DNS at them from GoDaddy.

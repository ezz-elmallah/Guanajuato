GUANAJUATO MEXICAN RESTAURANT — STATIC SITE
3907 Avenue H, Rosenberg, TX 77471 · (281) 633-9042

This folder is the whole website as plain HTML, CSS and JavaScript. There is no
Node process, no build step and no server code — it will run on any static host.


WHAT IS IN HERE
---------------
index.html              the site (one page, all seven sections)
404.html                the not-found page
_next/static/chunks/    the JavaScript, and the single compiled stylesheet
                        (....css — every design token and utility the site uses)
_next/static/media/     the two typefaces, self-hosted as .woff2, plus the icon
images/dishes/          30 dish photographs, cut out of the restaurant's menus
images/drinks/          5 bar photographs
icon.svg                the favicon
robots.txt, sitemap.xml
__next.*.txt            React payload files Next writes alongside the HTML;
                        harmless to keep, and small


HOW TO LOOK AT IT
-----------------
Opening index.html straight off the disk with file:// will not work — the page
loads its JavaScript and fonts by absolute path. Serve the folder instead:

    python3 -m http.server 8000        # then open http://localhost:8000
    # or
    npx serve .

To publish, upload the entire contents of this folder to any static host —
Netlify, Vercel, Cloudflare Pages, GitHub Pages, S3, or ordinary shared hosting.
Keep the folder structure exactly as it is.


BEFORE IT GOES LIVE
-------------------
The canonical URL, Open Graph tags, sitemap and structured data are all built
from one value — `siteUrl` in src/config/restaurant.ts of the source project,
currently https://gto-mex.com. If the real domain differs, change it there and
re-export (`npm run export`) rather than editing the HTML by hand.

Two things the static build gives up, because it has no server:

  · Image optimisation. The Node build resizes and re-encodes the photographs to
    AVIF/WebP per device; here the PNGs ship as authored (~24 MB total, lazily
    loaded below the fold). Everything above the fold is one image.
  · Redirects. /menu, /lunch, /contact, /directions and /hours redirect to the
    right section on the Node build. Configure those as redirect rules on your
    host if you want them, or drop them — nothing on the site links to them.


A NOTE ON THE CONTENT
---------------------
Every dish, price, portion and condition is transcribed from the restaurant's
own 2025 menu PDFs, and every photograph is the restaurant's own, taken from
those same PDFs. Prices are as printed in 2025 and have not been independently
confirmed as current; the site says so in the menu header, in each dish detail
and in the footer.

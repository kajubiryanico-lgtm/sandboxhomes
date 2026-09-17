# Answer key

Replace `YOUR-SITE` with your netlify address.

## Task 1: robots.txt and sitemap

robots.txt
```
User-agent: *
Allow: /
Sitemap: https://YOUR-SITE.netlify.app/sitemap.xml
```

sitemap.xml (list only pages you want indexed; not 404.html)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url><loc>https://YOUR-SITE.netlify.app/</loc></url>
  <url><loc>https://YOUR-SITE.netlify.app/services/extensions.html</loc></url>
  <url><loc>https://YOUR-SITE.netlify.app/locations/</loc></url>
  <url><loc>https://YOUR-SITE.netlify.app/locations/glen-waverley.html</loc></url>
  <url><loc>https://YOUR-SITE.netlify.app/projects/cypress.html</loc></url>
  <url><loc>https://YOUR-SITE.netlify.app/blog/extend-or-move.html</loc></url>
  <url><loc>https://YOUR-SITE.netlify.app/contact.html</loc></url>
</urlset>
```
Key idea: robots.txt controls **crawling**. A page blocked by robots.txt can't be read,
so Google can't see its content (or even a noindex tag on it).

## Task 2: noindex
Delete from services/extensions.html:
```html
<meta name="robots" content="noindex, nofollow">
```
Key idea: meta robots controls **indexing**. The page was crawlable but excluded from results.
On WordPress + Rank Math this lives in the page's Rank Math > Advanced tab, and
site-wide under Settings > Reading > "Discourage search engines".

## Task 3: homepage title + description
```html
<title>Custom Home Builders Melbourne | Sandbox Builders</title>
<meta name="description" content="Custom homes, extensions and knockdown rebuilds across Melbourne's eastern suburbs. Fixed-price agreements. Book a free 15-minute consultation.">
```

## Task 4: headings and alt text
Keep one H1 ("Expert builders for custom homes, extensions and renovations in Melbourne").
```html
<img src="..." alt="Double-storey custom home with rendered facade in Melbourne's east">
<img src="..." alt="Cypress French Provincial custom home in Glen Waverley, front elevation">
```

## Task 5: cannibalisation
Location page owns the local keyword:
```html
<title>Custom Home Builder Glen Waverley | Sandbox Builders</title>
```
Project page becomes a case study with its own angle:
```html
<title>Cypress: French Provincial Custom Home Case Study | Sandbox Builders</title>
<meta name="description" content="How we designed and built a 62-square French Provincial home in Glen Waverley: the brief, the build and the result.">
```
Location page: unique suburb copy + a two-line summary + link:
```html
<p>See how we handled a sloping Glen Waverley block in our
<a href="/projects/cypress.html">Cypress custom home case study</a>.</p>
```

## Task 6: internal links (examples)
On extensions.html:
```html
<p>Not sure whether to renovate or sell? Read our
<a href="/blog/extend-or-move.html">extend or move cost comparison</a>.</p>
<p><a class="cta" href="/contact.html">Get your free extension estimate</a></p>
```
On the guide:
```html
<p>Ready to see what your extension would cost?
<a href="/contact.html">Request a free feasibility and cost estimate</a>.</p>
<p>Learn more about our <a href="/services/extensions.html">home extensions in Melbourne</a>.</p>
```
locations/index.html: a simple hub listing each suburb page with one line each.
Menu: `<a href="/locations/">Locations</a>`.
Knockdown link: create `services/knockdown-rebuild.html` or remove the link.

Anchor text rule: describe the destination ("extension cost comparison"), never "click here".

## Task 8: schema + small fixes
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "HomeAndConstructionBusiness",
  "name": "Sandbox Builders",
  "url": "https://YOUR-SITE.netlify.app/",
  "telephone": "+61 3 1234 5678",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "Mulgrave",
    "addressRegion": "VIC",
    "addressCountry": "AU"
  },
  "areaServed": ["Glen Waverley", "Mulgrave", "Wheelers Hill", "Vermont"],
  "sameAs": [
    "https://www.facebook.com/example",
    "https://www.instagram.com/example"
  ]
}
</script>
```
```html
<a href="tel:+61312345678">(03) 1234 5678</a>
<meta property="og:locale" content="en_AU">
<p>&copy; <span id="yr"></span> Sandbox Builders</p>
<script>document.getElementById('yr').textContent = new Date().getFullYear();</script>
```

## Task 9: Meta Pixel
Paste Meta's base code (with your own Pixel ID) in `<head>`. Then in contact.html:
```js
fbq('track', 'Lead');
```
On a real WordPress site you'd use Meta's official integration or Google Tag Manager, and add
the Conversions API (server-side) so leads are still counted when browsers block the pixel.

## Task 10: GA4
```js
gtag('event', 'generate_lead');
```
Then mark `generate_lead` as a key event in GA4 Admin.

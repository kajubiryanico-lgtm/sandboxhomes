# Sandbox Builders: SEO + Meta Ads practice site

A small, deliberately broken builder website. It copies the kinds of problems found on rochomes.com.au
so you can practise the fixes on something you own. Nothing here touches ROC Homes.

Fixes are in ANSWER-KEY.md. Try each task first, then check.

---

## Part A: Put it online (15 minutes)

1. Create a free account at https://app.netlify.com (an account keeps the site live).
2. Unzip the download first. Then go to https://app.netlify.com/drop and drag the whole `sandbox-site` folder onto the page.
3. You get a live address like `https://something-random.netlify.app`. Rename it in
   Site configuration > Change site name, e.g. `bd-sandbox-builders`.
4. To update the site later: edit the files on your computer, then in Netlify open
   Deploys and drag the folder in again.

## Part B: Connect Google Search Console (crawling + indexing)

5. Go to https://search.google.com/search-console and add a property.
   Choose **URL prefix** and paste your full netlify address.
6. Verify with the **HTML tag** method: copy the `<meta name="google-site-verification" ...>` tag
   into the `<head>` of `index.html`, redeploy, click Verify.
7. Use **URL Inspection** on each page. Note which ones say "Excluded by noindex" or
   "Blocked by robots.txt". That is the crawling vs indexing difference, live.

---

## The practice tasks

### Task 1: Crawling
- Open `/robots.txt` in your browser. What is it blocking? Fix it.
- Create `sitemap.xml` listing every real page. Add a `Sitemap:` line to robots.txt.
- Submit the sitemap in Search Console > Sitemaps.

### Task 2: Indexing
- One service page tells Google not to index it. Find it and fix it.
- Re-run URL Inspection on that page and click **Request indexing**.

### Task 3: Titles and meta descriptions
- Give the homepage a real title (under ~60 characters) and a meta description (~150 characters)
  that includes the main keyword and a reason to click.

### Task 4: Headings and images
- The homepage has two H1s. Keep one.
- Add descriptive alt text to every image. `alt="image"` does not count.

### Task 5: Keyword cannibalisation + duplicate content
- The Cypress project page and the Glen Waverley page both target "custom home builder Glen Waverley".
  Decide which page owns that keyword. Retitle the other.
- The Glen Waverley page copies the Cypress text. Rewrite it with suburb-specific content
  (slopes, council, schools, block sizes) and a short summary that links to the Cypress case study.

### Task 6: Internal links
- Build this link path with descriptive anchor text:
  Home > Extensions service > Extend-or-Move guide > Contact
  Home > Glen Waverley page > Cypress case study > Contact
- Make "Locations" in the menu go to a real page (create `locations/index.html`).
- Fix the broken knockdown rebuild link: either create the page or remove the link.
- Afterwards, every page should be reachable within 3 clicks of the homepage.

### Task 7: Content
- Expand `blog/extend-or-move.html` into a real guide: costs of moving (stamp duty, agent fees,
  moving costs) vs costs of extending, a worked example, FAQs, and a call to action.
- Use the Victorian State Revenue Office stamp duty calculator for any stamp duty figure.

### Task 8: Local business schema
- Add a `HomeAndConstructionBusiness` JSON-LD block to the homepage (name, phone, address, area served,
  sameAs links).
- Test it at https://search.google.com/test/rich-results (paste the live URL).
- Fix the phone link: Australian numbers use `tel:+613...` with the leading 0 dropped.
- Change `og:locale` to `en_AU`. Update the copyright year.

### Task 9: Meta Pixel (no ad spend needed)
- In https://business.facebook.com create a Business portfolio, then Events Manager > Connect data > Web.
- Copy the Pixel base code into the `<head>` of every page (or at least index + contact).
- In `contact.html`, uncomment the `fbq('track', 'Lead')` line.
- Install the **Meta Pixel Helper** Chrome extension. Submit the form and confirm PageView and Lead fire.
- In Events Manager use **Test events** to watch them arrive.

### Task 10: GA4 (optional)
- Create a free GA4 property, add the gtag snippet, fire `generate_lead` on form submit,
  and watch it in GA4 > Reports > Realtime.

### Task 11: Build a Meta campaign without spending
- In Ads Manager create a campaign: objective **Leads**, conversion location **Website**, event **Lead**.
- Walk through the ad set (location, budget, placements) and ad (image/video, primary text, headline, CTA).
- If Ads Manager asks about a **special ad category**, read what it would restrict. Note it for the interview.
- Do **not** press Publish. Close it; it stays as a draft. (Nothing is charged unless you publish.)

### Task 12: Audit it like a pro
- Download Screaming Frog SEO Spider (free up to 500 URLs), crawl your netlify site before and after
  your fixes, and compare: response codes, titles, H1s, meta robots, inlinks.
- Run https://pagespeed.web.dev on the homepage.

---

When you're done: delete the site in Netlify (Site configuration > Delete) and remove the
Search Console property, so a fake builder isn't left online.

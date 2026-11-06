# TransUnion South Africa: website redesign concept (Sothopulse)

A production-structured static build of the redesign concept: 385 pages, each with its own clean URL that matches the live transunion.co.za address wherever the live site has one.

Version 36 adds the 218 pages the live site has that earlier versions left out, rebuilt in the same design: 73 blog posts, 7 opinion pieces, 11 Be the Reason articles, 30 Consumer Pulse reports and infographics, 16 Industry Insights reports and webinars, 5 Fraud Trends and 5 Mobility Insights reports, 5 summit and presentation pages, 10 research landing pages and insight guides, 16 videos, 11 Privacy Centre notices, 6 FAQ pages, 3 careers team pages, product, solution and industry pages, and the business branches page. New Blog, Opinion pieces and Videos hubs tie them together, and the Insights, Privacy Centre, FAQs, Careers, Business support and Sitemap pages now link to them.

> **Concept, not an official TransUnion website.** Page copy is taken from transunion.co.za (October 2026). Interface visuals are illustrative and photos are stock placeholders for a Sothopulse shoot. This build carries `noindex` so search engines ignore the preview.

## Preview it
- **Netlify Drop:** open https://app.netlify.com/drop and drag this whole folder onto the page. You get a private preview link in seconds.
- **Locally:** run `python3 -m http.server 8000` in this folder and open http://localhost:8000. The pages use root-relative links, so double-clicking the files won't work.

## What's in the folder
| Path | What it is |
|---|---|
| `/<section>/<page>/index.html` | One page per URL. Paths mirror transunion.co.za where the live site has an equivalent (for example `/product/hawk/`, `/solution/truvalidate/`, `/industry/retail/`), so a migration needs few redirects. |
| `/assets/` | Shared CSS, JavaScript, font and logos. Filenames are content-hashed so they can be cached for a year. |
| `/assets/search.*.js` | The site-search index. It only loads when someone opens search. |
| `/sitemap.xml`, `/robots.txt` | Sitemap of all 163 URLs. robots.txt blocks crawling for the concept and contains the production rules as a comment. |
| `/404.html` | Branded "page not found" page with search. |
| `/og-default.png` | Default social-share image (1200×630). |
| `netlify.toml` | Security headers, long-term caching for `/assets/`, and `X-Robots-Tag: noindex` for the concept. |

## Light and dark mode
The site follows the visitor's device: phones and computers set to dark mode get the dark theme automatically, everyone else gets the light one. An **Appearance** switch in the footer (Auto, Light, Dark) lets a visitor override it, and the choice is remembered in their browser. Both themes pass the same accessibility checks.

## Video
There are 75 TransUnion videos, placed on the pages where transunion.co.za has them, including the Be the Reason films and life-stage videos, summit sessions, webinars, product explainers and demos. Three careers videos live on YouTube and open there. They stream from transunion.co.za through a click-to-play player. Nothing downloads until someone presses play (the files are 9–130 MB), so page speed is unaffected. None of the live videos has captions, so add caption files (WebVTT) before launch.

## Every page includes
- A unique `<title>` and meta description, a canonical URL, and Open Graph and Twitter share tags.
- JSON-LD structured data: Organization and WebPage on every page, BreadcrumbList on pages with breadcrumbs, WebSite on the home page, FAQPage on `/faqs/` (55 real Q&As), and Product offers with ZAR prices on `/credit-report-products/`.
- `lang="en-ZA"`, a skip link, labelled forms, and accessible names on all controls.

## Measured results (October 2026)
- **Links:** 93,518 internal links checked across all pages, 0 broken.
- **Accessibility:** axe-core (WCAG 2.2 AA plus best practice) found 0 violations on all 385 pages, in both light and dark mode, at phone (375 px) and desktop (1440 px) widths.
- **JavaScript:** 0 errors on every page.
- **Lighthouse (mobile, with compression as served by Netlify):** 100 on Performance, Accessibility, Best Practices and SEO for the home, product, product comparison, credit guide, solution, business and dispute pages; the FAQ page scored 99 on Performance and 100 on the rest. SEO was measured on the indexable build; this concept build is deliberately `noindex`.
- **Layout, width and height:** tested from a 280 px folding phone to a 3840×2160 4K screen, including phones on their side (568×320, 844×390), short laptops (1280×720, 1366×768) and portrait monitors (1080×1920, 1440×2560). There is no horizontal scrolling, the page headline is visible without scrolling, fixed bars never cover more than about a third of the screen, and the footer sits at the bottom on tall screens.
- **Mobile:** the product comparison turns into swipeable plan cards with prices and subscribe buttons. Long card sets become swipe rows. Phone numbers and email addresses are tap-to-call and tap-to-email. Form controls are at least 44 px. The chat button moves out of the way while you scroll down.
- **Lighter phone reading:** on screens up to 640 px, long intros show three lines with "Read more", long paragraphs fold behind "Continue reading", card descriptions open on tap, long lists show titles only (the first six, then "Show all"), the breadcrumb becomes a back link, and the home enquiry form opens on request. No copy is removed, and desktop is unchanged.
- **Screen-size behaviour:** on short screens and phones the header slides away while you scroll down and comes back when you scroll up. Overlays use dynamic viewport units, so mobile browser toolbars never cut them off. On screens 2200 px and wider, the interface scales up instead of sitting in a narrow strip.

## Going to production on transunion.co.za
1. Rebuild without noindex. Run `build_site.py <out> index`, or remove the `robots` meta, the `X-Robots-Tag` header, and the `Disallow` line in robots.txt.
2. Replace the stock photos with the Sothopulse shoot. Each one is marked "Placeholder photo".
3. Connect the enquiry forms to TransUnion's CRM or form handler. In this concept they validate input but send nothing.
4. Add analytics, such as GA4 or the tag manager TransUnion already uses, and the consent banner TransUnion requires under POPIA.
5. Optional: move the content into a CMS (headless, or WordPress). The page structure maps cleanly to content types: Product, Solution, Industry, Article, Company page and FAQ.

<div align="center">
  <img src="public/logomark.png" width="64" height="64" alt="The Manila Collegian logomark" />
  <h1>Mkule — The Manila Collegian</h1>
  <p>Digital publishing platform for the official student newspaper of the University of the Philippines Manila.</p>
  <p>
    <a href="https://mkule.vercel.app/"><img src="https://img.shields.io/badge/Live%20Demo-mkule.vercel.app-22c55e?style=flat-square&logo=vercel" alt="Live Demo" /></a>
    <img src="https://img.shields.io/badge/version-1.0.0-22c55e?style=flat-square" alt="Version" />
    <img src="https://img.shields.io/badge/React-19-61dafb?style=flat-square&logo=react&logoColor=white" alt="React" />
    <img src="https://img.shields.io/badge/Next.js-16-000000?style=flat-square&logo=nextdotjs&logoColor=white" alt="Next.js" />
    <img src="https://img.shields.io/badge/TypeScript-5-3178c6?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript" />
    <img src="https://img.shields.io/badge/Tailwind%20CSS-4-06b6d4?style=flat-square&logo=tailwindcss&logoColor=white" alt="Tailwind CSS" />
    <img src="https://img.shields.io/badge/WordPress%20REST%20API-21759b?style=flat-square&logo=wordpress&logoColor=white" alt="WordPress REST API" />
  </p>
</div>

---

<!-- 📸 Add your screenshot or demo GIF to the assets/ folder, then uncomment: -->
<!-- ![Mkule — The Manila Collegian](assets/screenshot.png) -->

---

## Features

A headless news publication platform with a full editorial workflow — from article publishing and section archives to print edition browsing and reader engagement.

| Feature | Description |
|---|---|
| **Homepage Feed** | Hero story + live category sections pulled from WordPress with ISR |
| **Article Pages** | Full-width reader view with byline, featured image, share buttons, and JSON-LD schema |
| **Category Archives** | Six editorial sections (News, Features, Culture, Opinion, Editorial, Grafx) each with unique grid layouts |
| **Search** | Full-text search with pagination and newest/oldest sort; noindexed to protect crawl budget |
| **Author Profiles** | Staff writer pages with bio and paginated article history |
| **Print Issues Archive** | Bookshelf-style grid of past print editions with embedded PDF viewer and download |
| **Contact Form** | Server Action–powered form with Resend email delivery to the editorial team |
| **RSS Feed** | Dynamic `/rss.xml` route serving the latest 20 posts |
| **Sitemap** | Auto-generated `/sitemap.xml` from live WordPress content |

**Reading Progress Bar** &nbsp;·&nbsp; **Scroll-to-Top Button** &nbsp;·&nbsp; **Route Transition Loader** &nbsp;·&nbsp; **Google Analytics + Vercel Analytics** &nbsp;·&nbsp; **Open Graph metadata** &nbsp;·&nbsp; **Content Security Policy headers**

---

## Tech Stack

| Category | Technology |
|---|---|
| Framework | Next.js 16 (App Router) |
| Language | TypeScript 5 |
| UI Library | React 19 |
| Styling | Tailwind CSS 4 |
| Fonts | Merriweather (serif) · Libre Franklin (sans-serif) via `next/font` |
| CMS / Backend | WordPress REST API (Pantheon-hosted) |
| Email Delivery | Resend |
| Analytics | Vercel Analytics · Google Analytics (`@next/third-parties`) |
| Deployment | Vercel (Edge Network + ISR) |

---

## Project Structure

```
/
├── app/                        # Next.js App Router
│   ├── layout.tsx              # Root layout — Header, Footer, Analytics
│   ├── page.tsx                # Homepage with hero + category sections
│   ├── globals.css             # Global styles + Tailwind v4 theme
│   ├── robots.ts               # SEO robots configuration
│   ├── sitemap.ts              # Dynamically generated sitemap
│   ├── rss.xml/route.ts        # Live RSS feed endpoint
│   ├── news/[slug]/            # Article detail pages
│   ├── category/[slug]/        # Section archives (6 editorial categories)
│   ├── author/[slug]/          # Staff writer profiles
│   ├── search/                 # Full-text search with pagination
│   ├── issues/                 # Print edition PDF archive
│   ├── about/                  # Static about page
│   ├── contact/                # Contact form with server action
│   └── editorial-board/        # Editorial board listing
│
├── components/                 # Reusable UI components
│   ├── Header.tsx              # Sticky nav with scroll animations + mobile menu
│   ├── Footer.tsx              # Social links and section navigation
│   ├── CategorySection.tsx     # Adaptive grid layouts per section
│   ├── IssueCard.tsx           # PDF modal viewer with fullscreen + download
│   ├── ReadingProgress.tsx     # Scroll-based article progress bar
│   ├── Pagination.tsx          # Page navigation
│   ├── RouteLoader.tsx         # Route transition progress indicator
│   └── ScrollToTop.tsx         # Floating scroll-to-top button
│
├── lib/
│   ├── api.ts                  # WordPress REST API fetch helpers with ISR config
│   └── actions.ts              # Server Actions (contact form email delivery)
│
└── public/                     # Static assets (logos, favicons)
```

---

## Architecture Notes

- **Headless CMS with tiered ISR caching** — Article pages revalidate every 60 s; category and author pages every 3600 s (1 hour). This cuts origin requests to Pantheon by ~80% while keeping breaking news current within a minute.

- **Adaptive editorial layouts without a design system** — Each of the six content sections uses a distinct grid composition (4-col news, 50/50 features/culture, 60/40 editorial/opinion) implemented with Tailwind utility classes rather than a component library, keeping the bundle lean and layouts editable in a single file.

- **Server Actions for form handling** — The contact form avoids a dedicated API route by using a Next.js Server Action (`lib/actions.ts`) backed by Resend. Form state (pending, success, error) is managed on the server, reducing client-side JS.

- **PDF viewer without a library** — The print issues archive embeds Google Drive PDFs in an `<iframe>` inside a modal, converting `/view` URLs to `/preview` automatically. This delivers fullscreen viewing, a download button, and mobile swipe-to-close with zero third-party viewer dependencies.

- **Content Security Policy at the edge** — A strict CSP header is applied globally in `next.config.ts`, whitelisting only the specific third-party domains the app actually uses (Google Analytics, Vercel, Drive). `X-Content-Type-Options`, `Strict-Transport-Security`, and `Referrer-Policy` are also set at the edge, not in application code.

---

## License

© 2025 [jeymsx](https://github.com/jeymsx). All rights reserved.

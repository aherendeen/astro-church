# Astro Church

## Features

- **Pure Static Site Generation (SSG)**: Fast, SEO-friendly pages generated at build time
- **Content-Driven Architecture**: Content managed via Markdown files using Astro Content Collections
- **Mobile-First Responsive Design**: Tailwind CSS for beautiful, responsive layouts
- **SEO Optimized**: Complete meta tags, JSON-LD Schema, and sitemap.xml
- **CMS-Ready Structure**: Easily integrate with headless CMS solutions
- **Comprehensive Church Website Sections**: All essential pages for a complete church website
- **Accessibility Focus**: WCAG compliant design and markup
- **Modern UI Components**: Reusable components with hover states and micro-interactions
- **Integrated Church Icon**: Custom SVG church icon used throughout the site
- **Image Optimization**: Proper image organization and fallback handling

## Project Structure

```txt
astro-church/
├── public/
│   ├── uploads/          # Images directories (staff, events, sermons, etc.)
│   │   ├── staff/        # Staff profile images
│   │   ├── events/       # Event images
│   │   ├── sermons/      # Sermon thumbnail images
│   │   ├── ministries/   # Ministry logo images
│   │   └── blog/         # Blog post images
│   ├── favicon.svg
│   ├── robots.txt
│   └── site.webmanifest
├── src/
│   ├── assets/           # Astro-processed assets
│   ├── components/       # Reusable Astro components
│   │   ├── Global/       # Header, Footer, Navigation
│   │   ├── Sections/     # Page sections (Hero, Events, etc.)
│   │   └── UI/           # UI components (Button, Card, SEO)
│   ├── content/          # Astro Content Collections
│   │   ├── config.ts     # Collection schemas
│   │   ├── staff/        # Staff member profiles
│   │   ├── events/       # Church events
│   │   ├── sermons/      # Sermon content
│   │   ├── ministries/   # Ministry descriptions
│   │   ├── blog/         # Blog posts
│   │   └── siteInfo/     # Site configuration content
│   ├── layouts/          # Page layouts
│   ├── pages/            # Astro pages
│   └── utils/            # Utility functions
├── astro.config.mjs
├── tailwind.config.cjs
└── tsconfig.json
```

## Getting Started

### Prerequisites

- Node.js 18 or later
- npm or yarn

### Installation

1. Clone this repository:

   ```bash
   git clone https://github.com/aherendeen/astro-church.git
   cd astro-church
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Start the development server:

   ```bash
   npm run dev
   ```

4. Open your browser and navigate to `http://localhost:4321`

## Content Management

### Adding/Editing Content

All content is stored in Markdown (`.md`) files in the `src/content/` directory.

#### Creating a New Staff Member

1. Create a new file in `src/content/staff/` with a `.md` extension (e.g., `john-smith.md`)
2. Add the required frontmatter fields:

```markdown
---
name: "John Smith"
title: "Youth Pastor"
image: "/uploads/staff/john-smith.webp"
email: "john@astro-church.vercel.app"
phone: "+1-555-1234"
bio: "John has been serving in youth ministry for 10 years."
order: 3
draft: false
---

Detailed biography and information about John goes here...
```

#### Creating a New Event

1. Create a new file in `src/content/events/` with a `.md` extension
2. Add the required frontmatter fields:

```markdown
---
title: "Youth Summer Camp"
date: 2025-07-15
endDate: 2025-07-20
time: "9:00 AM - 5:00 PM"
location: "Camp Wilderness"
image: "/uploads/events/summer-camp.webp"
summary: "A week-long adventure for teens to grow in faith and have fun!"
tags: ["youth", "summer", "camp"]
registrationRequired: true
registrationLink: "https://astro-church.vercel.app/register"
draft: false
---

## About Summer Camp

Join us for an exciting week of activities, worship, and spiritual growth...
```

#### Creating a New Sermon

1. Create a new file in `src/content/sermons/` with a `.md` extension
2. Add the required frontmatter fields:

```markdown
---
title: "Walking in Faith"
date: 2025-02-02
speaker: "Rev. Dr. John Smith"
series: "Faith Foundations"
scripture: "Proverbs 3:5-6"
audioUrl: "https://astro-church.vercel.app/sermons/walking-in-faith.mp3"
videoUrl: "https://www.youtube.com/embed/example789"
image: "/uploads/sermons/walking-in-faith.webp"
summary: "Learn how to trust God completely and walk confidently in His plan."
tags: ["faith", "trust", "guidance"]
draft: false
---

## Sermon Overview

Content of your sermon goes here...
```

### Content Schema

See `src/content/config.ts` for the complete schema definitions for all content types.

## Key Pages and Features

### Main Pages

- **Homepage** (`/`): Hero section, service times, about preview, recent events/sermons
- **About Us** (`/about-us`): Mission, values, history, staff preview
- **Staff** (`/staff`): Complete staff directory with contact information
- **Ministries** (`/ministries`): All church ministries with detailed pages
- **Sermons** (`/sermons`): Sermon archive with audio/video support and filtering
- **Events** (`/events`): Upcoming and past events with registration support
- **Blog** (`/blog`): Church blog with filtering and search
- **I'm New** (`/im-new`): First-time visitor information
- **Contact** (`/contact`): Contact forms, location, staff contacts
- **Giving** (`/giving`): Online giving information and financial transparency

### Special Features

- **Responsive Design**: Mobile-first approach with proper breakpoints
- **Content Filtering**: Advanced filtering on sermons and blog posts
- **SEO Optimization**: Complete meta tags, JSON-LD schema, and sitemap
- **Accessibility**: WCAG compliant with proper ARIA labels and keyboard navigation
- **Performance**: Optimized images and fast loading times
- **Modern UI**: Hover states, transitions, and micro-interactions

## Customization

### Site Information

Update your church information in the following files:

- Site metadata in `astro.config.mjs`
- SEO defaults in `src/layouts/BaseLayout.astro`
- Contact information in `src/components/Global/Footer.astro`
- Church details throughout the content files

### Styling

1. Customize colors and other theme settings in `tailwind.config.cjs`
2. Global styles are in `src/assets/styles/global.css`
3. includes a comprehensive color system with primary, secondary, and accent colors

### Logo & Branding

includes a built-in church SVG icon that's used throughout the site. To customize:

1. Replace the SVG icon in `src/components/Global/Header.astro` and `src/components/Global/Footer.astro`
2. Update favicon in `public/favicon.svg`
3. Modify the site manifest in `public/site.webmanifest`

### Images

Images are organized in the `/public/uploads/` directory:

- `/uploads/staff/` - Staff profile images
- `/uploads/events/` - Event images
- `/uploads/sermons/` - Sermon thumbnails
- `/uploads/ministries/` - Ministry logos
- `/uploads/blog/` - Blog post images

includes fallback handling for missing images and uses external Unsplash images for some sections.

## Headless CMS Integration

Designed to work well with these headless CMS solutions:

### TinaCMS

1. Install TinaCMS:

   ```bash
   npm install tinacms @tinacms/cli
   ```

2. Add the Tina config file (see TinaCMS documentation)

3. The existing Content Collections schemas can be adapted for TinaCMS

### Decap CMS (formerly Netlify CMS)

1. Add Decap CMS config to `public/admin/config.yml`
2. The existing Content Collections structure works well with Decap CMS

## Deployment

This site can be deployed to any static hosting platform:

### Netlify

1. Push your repository to GitHub
2. Connect to Netlify
3. Set build command to `npm run build` and publish directory to `dist/`

### Vercel

1. Push your repository to GitHub
2. Import in Vercel
3. It will automatically detect Astro and set up the correct build settings

### GitHub Pages

1. Install gh-pages:

   ```bash
   npm install -D gh-pages
   ```

2. Add deploy script to package.json:

   ```json
   "scripts": {
     "deploy": "npm run build && gh-pages -d dist"
   }
   ```

3. Run `npm run deploy`

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Bugs / Issues

We appreciate your understanding and encourage you to report any new bugs you find by
[opening an issue](https://github.com/aherendeen/astro-church/issues)
on our GitHub repository.

## Acknowledgments

- [Astro](https://astro.build) for the awesome static site generator
- [Tailwind CSS](https://tailwindcss.com) for the utility-first CSS framework
- [Heroicons](https://heroicons.com) for the icon system
- [Pexels](https://pexels.com) & [Unsplash](https://unsplash.com) for stock photography

## Support

For questions, issues, or contributions, please visit our GitHub repository or contact the development team.

## Donate

Like my work?

[![Buy Me a Coffee](https://img.shields.io/badge/Buy%20me%20a%20coffee-Donate-ff813f)](https://www.buymeacoffee.com/aherendeen)

Support the project:

- GitHub Sponsors: <https://github.com/sponsors/aherendeen>
- Buy Me a Coffee: <https://www.buymeacoffee.com/aherendeen>

---

crafted with 🩵 for church communities worldwide

## Community & Policies

Please review our community guidelines and legal pages:

- [Code of Conduct](CODE_OF_CONDUCT.md)
- [Contributing Guide](CONTRIBUTING.md)
- [Security Policy](SECURITY.md)

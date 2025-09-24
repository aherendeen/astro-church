# Copilot instructions for astro-church

Purpose: Give AI coding agents the immediate, actionable knowledge they need to contribute safely and productively to this Astro site.

Big picture

- This is a content-driven Astro static site. Pages are rendered from content collections in `src/content/*` and templates in `src/layouts/`.
- Dynamic routes (e.g. `src/pages/sermons/[slug].astro`) read collections via `getCollection` from `astro:content` and render with layout components (`BaseLayout`, `PostLayout`).
- Styling is Tailwind (integration in `astro.config.mjs` + `tailwind.config.cjs`) and components live under `src/components/`.

Key conventions & patterns (explicit, discoverable)

- Content collections and validation live in `src/content/config.ts`. Update this file when adding new collection types or frontmatter fields.
- Image path validators require files under `public/uploads/` with collection-specific subfolders. Examples enforced by zod schemas:
  - Staff images must start with `/uploads/staff/`
  - Events: `/uploads/events/`
  - Sermons: `/uploads/sermons/`
  - Ministries: `/uploads/ministries/`
  - Blog images: `/uploads/blog/`
- Draft handling: most pages check `draft` frontmatter and only hide drafts in production. Follow the exact filter used in the codebase:
  - Example (from `src/pages/ministries/index.astro`):
    const all = await getCollection("ministries", ({ data }) =>
    import.meta.env.PROD ? !data.draft : true
    );
- Sorting: collections frequently sort by an `order` numeric field (fallback to name). Example pattern:
  - ministries.sort((a,b) => (a.data.order ?? 0) - (b.data.order ?? 0) || a.data.name.localeCompare(b.data.name))
- Slugs: `slug` is optional in many schemas — the system will auto-generate when omitted. Do not assume slug always exists in frontmatter.
- Dates: Collection fields that use dates (e.g., `events.date`, `blog.pubDate`, `sermons.date`) expect real Date values in frontmatter; use ISO dates in markdown files.
- MDX allowed: Some content files are `.mdx` (see `src/content/events/` and `src/content/sermons/`), so components may be embedded in content — preserve MDX compatibility when changing collection renderers.

Developer workflows (commands you should use)

- Install: `npm install`
- Local dev with HMR: `npm run dev` (runs `astro dev`)
- Create production build: `npm run build` (runs `astro build`)
- Local preview of build output: `npm run preview` (runs `astro preview`)
- Deployment notes (from README):
  - Netlify: build command `npm run build`, publish directory `dist/`.
  - Vercel: Auto-detected as Astro — no special config required.
  - GitHub Pages (optional): add `gh-pages` and deploy `dist/`.

Files to reference when changing behavior

- Content schema & rules: `src/content/config.ts`
- Pages that demonstrate collection usage and draft filtering: `src/pages/ministries/index.astro`, `src/pages/ministries/[slug].astro`, `src/pages/sermons/*`, `src/pages/blog/index.astro`.
- Global layout and SEO: `src/layouts/BaseLayout.astro`, `src/layouts/PostLayout.astro`, `src/components/UI/Seo.astro`.
- Utilities: `src/utils/dateUtils.js` (date formatting helper used across templates).
- Tailwind configuration (custom colors & fonts): `tailwind.config.cjs`.

Project-specific guidance for code changes

- When adding a new content type:
  1. Add collection schema to `src/content/config.ts` (use existing schemas as a template).
  2. Add example markdown under `src/content/<new>/example.md` and include required frontmatter keys.
  3. Ensure any image fields validate against `/uploads/<new>/` and add the uploads folder under `public/uploads/<new>/`.
  4. Add a page (e.g., `src/pages/<new>/index.astro` and `[slug].astro`) that uses `getCollection` and follows the draft filter pattern.
- Changing how drafts are treated: change the production-only filter consistently across pages rather than altering a single page — search for `import.meta.env.PROD ? !data.draft : true` to find usages.
- Don't change `order` sorting semantics: numeric `order` asc, then fallback to alphabetical by `name` or `title`.

Debugging hints

- If a build fails due to content validation, the error will reference the collection and frontmatter key. Check `src/content/config.ts` for exact zod validators (e.g., `startsWith('/uploads/staff/')`, `z.date()`).
- Missing images — ensure files are in `public/uploads/...` and frontmatter paths begin with `/uploads/...`.
- MDX render or hydration problems: check the page that renders the MDX (some pages load `.mdx` files directly); ensure component imports used in MDX are available.

What NOT to change without owner approval

- Site URL in `astro.config.mjs` (`site` field) and sitemap integration settings.
- Tailwind base tokens (colors/fonts) without design approval — many pages use these tokens directly.

If anything here is unclear or you need more concrete examples (e.g., a sample staff frontmatter or a sample `[slug].astro` page), tell me which area to expand and I'll update this file.

# TruePDF

Free browser-based tools. 39 tools, zero signup, zero uploads: every file is processed locally in the visitor's browser and never touches a server.

Live site: https://truepdf.vercel.app/

## Tools

**PDF** (15): PDF Editor, Images to PDF, Compress PDF, PDF to JPG, Redact PDF, Sign PDF, Unlock PDF, PDF to Word, OCR PDF, Extract Images, Extract Text, Edit PDF Metadata, Fill PDF Form, Flatten PDF, Repair PDF

**Image** (5): Image compressor, Image converter, Background remover, Image OCR, Image tracer

**Media** (8): Audio trimmer, Audio merger, Audio converter, Video compressor, Video trimmer, Video converter, Subtitle editor, Screen recorder

**Business** (3): Invoice generator, Email signature generator, Business profile

**Money** (2): Budget planner, Subscription tracker

**Design** (3): Logo maker, OG image generator, Device mockup generator

**Career** (1): Resume builder

**Generators** (2): QR code generator, Fake data generator

## Privacy

No accounts, no cookies, no server-side processing. Optional analytics uses GoatCounter (cookieless, no personal data). See "Analytics" below.

## Tech

Astro 5 static site, TypeScript. Heavy lifting is client-side: pdf-lib, pdf.js, Pyodide (pypdf) for Unlock PDF, FFmpeg WASM for media tools, Tesseract.js for OCR, BiRefNet Lite (onnxruntime-web) for background removal.

## Local development

```bash
npm ci
npm run dev
```

Build and run the automated checks:

```bash
npm run build
npm run verify
```

## Deployment

Pushes to `main` auto-deploy on Vercel. Two environment variables control the output:

- `SITE_URL`: absolute site URL (default `https://www.truepdf.com`)
- `BASE_PATH`: subpath the site is served from, ending in `/` (default `/`)

Always push the source tree, never `dist/`.

## Analytics

Pageview analytics use GoatCounter (cookieless, no personal data). The site code is set in `src/lib/site.ts` (`ANALYTICS_CODE`); empty it to disable analytics entirely.

Pageviews are then counted per tool page, which shows which tools get used. No events, no fingerprinting.

## Feedback

The `/feedback` page on the site opens a prefilled GitHub issue on this repo, so feedback lands here as issues. No backend needed.

## Project structure

- `src/pages/`: one `.astro` file per tool plus category index pages
- `src/layouts/`: `BaseLayout.astro` (head, header, footer), `ToolPage.astro` (tool page template with SEO structured data)
- `src/components/`: shared UI (command palette, support notice)
- `src/lib/`: tool logic, `tools.ts` (canonical tool index), `site.ts` (URLs, analytics, donate link)
- `scripts/verify-tools.mjs`: automated checks (run with `npm run verify`)
- `public/`: static files (`robots.txt`, `llms.txt`, OG image)

## License

MIT.

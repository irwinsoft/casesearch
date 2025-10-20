# Public Court Records Website

A static website built with Astro and TailwindCSS to display publicly available Maryland court records in a clean, professional format.

## Features

- **Static Site Generation**: Fast, secure, and SEO-friendly
- **Modern Design**: Professional government document aesthetic
- **Responsive**: Works perfectly on all devices
- **Print-Friendly**: Clean printable versions of court records
- **SEO Optimized**: Structured data and meta tags for search visibility
- **Easy Updates**: Update court data without touching code (JSON-based)

## Project Structure

```
/
├── public/
│   ├── documents/           # Place PDF files here
│   │   └── sample-small-claims.pdf
│   ├── robots.txt
│   ├── favicon.svg
│   └── .nojekyll           # Required for GitHub Pages
├── src/
│   ├── components/          # Reusable Astro components
│   │   ├── Header.astro
│   │   ├── Footer.astro
│   │   ├── DisclaimerFooter.astro
│   │   └── CaseInfoTable.astro
│   ├── data/
│   │   └── caseData.json   # Court case data (easy to update!)
│   ├── layouts/
│   │   └── Layout.astro    # Main layout with SEO
│   ├── pages/               # Page routes
│   │   ├── index.astro     # Home page
│   │   ├── case-record.astro
│   │   └── small-claims.astro
│   └── styles/
│       └── global.css      # TailwindCSS styles
├── astro.config.mjs
├── tailwind.config.mjs
└── package.json
```

## Quick Start

### Prerequisites

- Node.js 18 or higher
- npm or yarn

### Installation

1. Clone or download this repository
2. Install dependencies:

```bash
npm install
```

3. Start the development server:

```bash
npm run dev
```

4. Open your browser to `http://localhost:4321`

## Updating Court Data

### Easy Method: Edit JSON File

All court case information is stored in `src/data/caseData.json`. Simply edit this file with your actual case data:

```json
{
  "defendant": {
    "fullName": "John Michael Doe",
    "displayName": "John M. Doe"
  },
  "marylandCase": {
    "caseNumber": "DC-12-CV-123456",
    "court": "District Court of Maryland for Baltimore City",
    // ... more fields
  }
}
```

**No code changes required!** Just update the JSON and rebuild.

### Adding PDF Documents

1. Place your PDF file in the `public/documents/` directory
2. Update the `pdfPath` in `caseData.json`:

```json
"smallClaimsSuit": {
  "pdfPath": "/documents/your-actual-file.pdf"
}
```

## Building for Production

Build the static site:

```bash
npm run build
```

The output will be in the `dist/` directory, ready to deploy.

Preview the production build locally:

```bash
npm run preview
```

## Deployment

### GitHub Pages

1. Update `astro.config.mjs` with your site URL:

```javascript
export default defineConfig({
  site: 'https://yourusername.github.io',
  base: '/your-repo-name', // Only if not using custom domain
  // ...
});
```

2. Build the site:

```bash
npm run build
```

3. Deploy the `dist/` folder to GitHub Pages using GitHub Actions or manually

**GitHub Actions Setup** (recommended):

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: 20
      - name: Install dependencies
        run: npm install
      - name: Build
        run: npm run build
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./dist
  
  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

Enable GitHub Pages in your repository settings (Settings > Pages > Source: GitHub Actions).

### Netlify

1. Connect your repository to Netlify
2. Configure build settings:
   - Build command: `npm run build`
   - Publish directory: `dist`
3. Deploy!

Or use the Netlify CLI:

```bash
npm install -g netlify-cli
netlify deploy --prod
```

### Cloudflare Pages

1. Connect your repository to Cloudflare Pages
2. Configure build settings:
   - Build command: `npm run build`
   - Build output directory: `dist`
3. Deploy!

### Custom Domain

After deploying to any platform:

1. Add a custom domain in your hosting provider's dashboard
2. Update the `site` URL in `astro.config.mjs`
3. Update the `Sitemap` URL in `public/robots.txt`
4. Rebuild and redeploy

## SEO Configuration

### Before Deployment

Update these files with your actual domain:

1. **astro.config.mjs**: Set your `site` URL
2. **public/robots.txt**: Update the Sitemap URL

### Meta Tags

The site includes comprehensive SEO meta tags:
- Page titles optimized for search
- Meta descriptions for each page
- Open Graph tags for social sharing
- Twitter Card support
- Schema.org structured data for legal documents
- Automatic sitemap generation

## Customization

### Colors

Edit the color scheme in `tailwind.config.mjs`:

```javascript
colors: {
  'court-gray': { /* ... */ },
  'court-blue': { /* ... */ }
}
```

### Content

All content can be customized by editing the JSON file or the Astro page components:
- Case data: `src/data/caseData.json`
- Page layouts: `src/pages/*.astro`
- Components: `src/components/*.astro`

### Adding More Cases

To add multiple cases, you can:
1. Extend the JSON structure in `caseData.json`
2. Create new pages in `src/pages/`
3. Add links from the home page

## Browser Support

- Modern browsers (Chrome, Firefox, Safari, Edge)
- Mobile browsers (iOS Safari, Chrome Mobile)
- Print functionality for all major browsers

## Tech Stack

- **[Astro](https://astro.build)**: Static site generator
- **[TailwindCSS](https://tailwindcss.com)**: Utility-first CSS framework
- **[@astrojs/sitemap](https://docs.astro.build/en/guides/integrations-guide/sitemap/)**: Automatic sitemap generation
- **[@tailwindcss/typography](https://tailwindcss.com/docs/typography-plugin)**: Beautiful typography

## License

This project template is provided as-is. Update with your own license as needed.

## Disclaimer

This is a template for displaying public court records. Ensure that:
- All information is from publicly available sources
- You have the right to republish the information
- You comply with all applicable laws and regulations
- The disclaimer on the site accurately reflects your legal position

Consult with a legal professional if you have questions about publishing court records.

## Support

For issues or questions about Astro, visit:
- [Astro Documentation](https://docs.astro.build)
- [Astro Discord](https://astro.build/chat)

## Development Notes

### File Watching

The dev server automatically reloads when you edit:
- Page files (`src/pages/`)
- Components (`src/components/`)
- Data files (`src/data/caseData.json`)
- Styles (`src/styles/`)

### Adding New Pages

1. Create a new `.astro` file in `src/pages/`
2. Import and use the Layout component
3. Add navigation links in Header and Footer components
4. The route is automatically created based on the filename

Example: `src/pages/about.astro` → `https://yoursite.com/about`

## Performance

This site is optimized for performance:
- Zero JavaScript shipped by default
- Minimal CSS (TailwindCSS, purged in production)
- Static HTML files
- Fast page loads (<1s initial load)
- Excellent Lighthouse scores

## Accessibility

The site follows accessibility best practices:
- Semantic HTML structure
- Proper heading hierarchy
- ARIA labels where appropriate
- Keyboard navigation support
- High contrast text
- Print-friendly styles

---

**Last Updated**: October 2025


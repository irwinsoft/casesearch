# Quick Start Guide

Get your court records website up and running in 5 minutes.

## Step 1: Install Dependencies

```bash
npm install
```

## Step 2: Start Development Server

```bash
npm run dev
```

Visit `http://localhost:4321` to see your site.

## Step 3: Update Your Data

Edit `src/data/caseData.json` with your actual court case information:

```json
{
  "defendant": {
    "fullName": "Your Defendant's Full Name",
    "displayName": "Display Name"
  },
  "marylandCase": {
    "caseNumber": "Your-Case-Number",
    "court": "Your Court Name",
    // ... update all fields
  }
}
```

## Step 4: Replace the Sample PDF

1. Place your actual court PDF in `public/documents/`
2. Update the filename in `caseData.json`:
   ```json
   "pdfPath": "/documents/your-actual-file.pdf"
   ```

## Step 5: Build for Production

```bash
npm run build
```

Your static site will be in the `dist/` folder, ready to deploy!

## Next Steps

### Before Deploying

1. Update the site URL in `astro.config.mjs`:
   ```javascript
   site: 'https://yourdomain.com',
   ```

2. Update the sitemap URL in `public/robots.txt`

### Deploy Options

**GitHub Pages** (easiest):
- Push your code to GitHub
- Enable GitHub Pages in repository settings
- The included GitHub Action will auto-deploy

**Netlify**:
```bash
netlify deploy --prod
```

**Cloudflare Pages**:
- Connect your repository in Cloudflare dashboard
- Build command: `npm run build`
- Output directory: `dist`

## Customization Tips

### Change Colors
Edit `tailwind.config.mjs` to customize the color scheme.

### Add More Cases
1. Extend the JSON structure in `caseData.json`
2. Create new pages in `src/pages/`
3. Add navigation links

### Modify Layout
All components are in `src/components/` - edit freely!

## Need Help?

- See full documentation in `README.md`
- Astro docs: https://docs.astro.build
- TailwindCSS docs: https://tailwindcss.com

## Common Commands

```bash
npm run dev       # Start dev server
npm run build     # Build for production
npm run preview   # Preview production build
```

That's it! You're ready to publish your court records website.


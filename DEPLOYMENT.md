# Cloudflare Pages Deployment Guide

## Overview
This is a static website optimized for Cloudflare Pages/R2 deployment. All backend features have been removed or converted to client-side functionality.

## Files Structure
```
public/
├── index.html          # Main landing page
├── dashboard.html      # Dashboard (static demo)
├── fractal.html        # Fractal generator
├── shapes.html         # Simulation generator
├── solar.html          # Solar system simulation
├── redroom.html        # Interactive experience
├── styles.css          # Main stylesheet
├── dashboard.css       # Dashboard styles
├── fractal.css         # Fractal page styles
├── shapes.css          # Simulator styles
├── solar.css           # Solar system styles
├── *.js                # JavaScript files
└── images/             # Image assets
_redirects              # Cloudflare Pages routing rules
```

## Deployment Steps

### Option 1: Cloudflare Pages Dashboard (Recommended)

1. **Prepare Files:**
   - Ensure all files from the `public/` folder are at the root level
   - Include the `_redirects` file at the root

2. **Upload to Cloudflare:**
   - Log in to your Cloudflare account
   - Go to Pages → Create a project
   - Choose "Direct Upload"
   - Drag and drop all files from the `public/` folder
   - Add the `_redirects` file to the root
   - Click "Deploy Site"

3. **Configuration:**
   - Build command: (leave empty - static files)
   - Build output directory: `/`
   - No framework preset needed

### Option 2: Git Integration

1. **Create Repository:**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin <your-repo-url>
   git push -u origin main
   ```

2. **Connect to Cloudflare Pages:**
   - Go to Cloudflare Pages → Create a project
   - Choose "Connect to Git"
   - Select your repository
   - Configure build settings:
     - Build command: (leave empty)
     - Build output directory: `/public`

3. **Deploy:**
   - Click "Save and Deploy"
   - Cloudflare will automatically deploy on every push

### Option 3: Wrangler CLI

1. **Install Wrangler:**
   ```bash
   npm install -g wrangler
   ```

2. **Login to Cloudflare:**
   ```bash
   wrangler login
   ```

3. **Deploy:**
   ```bash
   wrangler pages deploy public --project-name=impulsive-cc
   ```

## R2 Assets (Optional)

The site references some R2 assets (audio files). These are already hosted and accessible via CORS-enabled URLs:
- Audio files: `https://pub-14b82f67a06cec7782ea14ad4ac98073.r2.dev/bucketz/`

No additional R2 setup is required unless you want to move assets to your own R2 bucket.

## Post-Deployment Checklist

- [ ] Test all pages load correctly
- [ ] Verify all simulations run smoothly
- [ ] Check that all images display properly
- [ ] Test fractal generator functionality
- [ ] Verify solar system simulation works
- [ ] Confirm Red Room audio plays correctly
- [ ] Test on mobile devices
- [ ] Check browser console for errors

## Custom Domain (Optional)

1. Go to your Cloudflare Pages project
2. Click "Custom Domains"
3. Add your domain
4. Cloudflare will automatically configure DNS

## Troubleshooting

**Issue: Pages don't load**
- Check that `_redirects` file is at the root
- Verify all HTML files are in the correct location

**Issue: Styles not loading**
- Ensure CSS files use relative paths (`./styles.css`)
- Check browser console for 404 errors

**Issue: JavaScript errors**
- Open browser console to see specific errors
- Verify all script paths use relative paths

**Issue: Images not displaying**
- Check that `images/` folder is included
- Verify image paths are relative (`./images/`)

## Performance Optimization

The site is already optimized for Cloudflare Pages:
- ✅ All assets use relative paths
- ✅ No build process required
- ✅ Static files ready for CDN caching
- ✅ Minimal external dependencies
- ✅ Canvas-based animations (GPU accelerated)

## Notes

- Backend features (auth, database) have been removed for static deployment
- Local storage is used for Red Room high scores
- All simulations run entirely client-side
- No server-side processing required

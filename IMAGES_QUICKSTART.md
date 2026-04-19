# Premium Product Images — Quick Start Guide

**Status:** ✅ Codebase Ready — Images Needed
**Last Updated:** 2026-04-19

---

## What's Done

✅ **CSS styling added** — Premium image display with theme-aware backgrounds
✅ **Product configs updated** — All 6 products now expect `.webp` format
✅ **Responsive design** — Images work on mobile, tablet, and desktop
✅ **Dark theme support** — Enhanced visibility with brightness/contrast adjustments
✅ **Lazy loading** — Shimmer effect while images load
✅ **Hover effects** — Smooth zoom and brightness on hover

---

## What You Need To Do

**Add 6 premium seafood images to:**
```
frontend/public/assets/images/
```

**Required file names (must match exactly):**
1. `vannamei-shrimp.webp`
2. `black-tiger-shrimp.webp`
3. `squid.webp`
4. `cuttlefish.webp`
5. `dried-shrimp.webp`
6. `pink-perch.webp`

---

## Image Requirements

| Property | Requirement |
|----------|-------------|
| **Format** | WebP (primary) |
| **Size** | 1200×1200px (1:1 aspect ratio) |
| **File Size** | <150KB per image |
| **Background** | Transparent OR clean white/neutral |
| **Quality** | Crystal clear, professional food photography |

---

## Quick Option: Free Stock Photos

### Recommended Sites:
- **Unsplash** (https://unsplash.com) — Best quality, free commercial use
- **Pexels** (https://pexels.com) — Good selection, free commercial use
- **Pixabay** (https://pixabay.com) — Large collection, mixed quality

### Search Terms:
```
Vannamei Shrimp:    "fresh raw shrimp white background"
Black Tiger Shrimp: "black tiger prawn striped"
Squid:              "fresh squid seafood"
Cuttlefish:         "cuttlefish sepia seafood"
Dried Shrimp:       "dried shrimp golden"
Pink Perch:         "threadfin bream fish"
```

---

## Image Processing Steps

### Option 1: Using Online Tools (Easiest)

1. **Download high-res image** from stock site (JPG/PNG)

2. **Remove background** (if needed):
   - Go to https://remove.bg
   - Upload image → Download PNG
   - Free tier: 50 images/month

3. **Convert to WebP**:
   - Go to https://cloudconvert.com/png-to-webp
   - Upload PNG → Convert → Download

4. **Resize to 1200×1200**:
   - Go to https://www.iloveimg.com/resize-image
   - Upload → Set to 1200×1200 → Download

5. **Copy to project**:
   ```bash
   cp ~/Downloads/vannamei-shrimp.webp frontend/public/assets/images/
   ```

### Option 2: Using CLI Tools (Faster)

**Install tools** (one-time setup):
```bash
# macOS
brew install imagemagick webp

# Linux
sudo apt-get install imagemagick webp
```

**Process images** (batch):
```bash
cd ~/Downloads

# Crop to square and resize to 1200×1200
for img in *.jpg *.png; do
  convert "$img" -gravity center -extent 1:1 -resize 1200x1200 "resized_$img"
done

# Convert to WebP with quality 85
for img in resized_*; do
  name=$(basename "$img" | sed 's/resized_//' | sed 's/\.[^.]*$//')
  cwebp -q 85 "$img" -o "${name}.webp"
done

# Copy to project
cp *.webp /Volumes/hex/current-work/alashore-marine/frontend/public/assets/images/
```

---

## After Adding Images

1. **No code changes needed** — CSS and configs already updated

2. **Test locally**:
   ```bash
   pnpm dev
   # Open http://localhost:8045
   # Check products section on home page
   ```

3. **Test both themes**:
   - Click theme toggle (top-right)
   - Verify images look good in light AND dark mode

4. **Check responsive**:
   - Resize browser window (mobile, tablet, desktop)
   - Images should scale properly

---

## Expected Appearance

### Light Theme:
- Images on soft white/gray gradient background
- Subtle shadow for depth
- Smooth zoom on hover (1.08x scale)
- Clean, professional presentation

### Dark Theme:
- Images on dark gray gradient background
- Enhanced brightness (+10-15%) for visibility
- Increased contrast for clarity
- Premium shadows

### All Themes:
- Images centered in card
- 1.5rem padding around image
- Smooth transitions (0.5s cubic-bezier)
- Lazy loading with shimmer effect

---

## Troubleshooting

### Images Not Showing?
```bash
# Check files exist and have correct names
ls -lh frontend/public/assets/images/*.webp

# Should show:
# vannamei-shrimp.webp
# black-tiger-shrimp.webp
# squid.webp
# cuttlefish.webp
# dried-shrimp.webp
# pink-perch.webp
```

### Browser Showing Old SVG Images?
```bash
# Hard refresh browser
# macOS: Cmd + Shift + R
# Windows/Linux: Ctrl + Shift + R
```

### Images Look Bad in Dark Mode?
- Ensure images have transparent OR light neutral background
- Dark backgrounds will look bad with our dark theme gradient
- Use remove.bg to get transparent background

### File Size Too Large?
```bash
# Re-encode with lower quality
cwebp -q 70 input.png -o output.webp

# Check size
ls -lh output.webp
# Target: <150KB
```

---

## Full Documentation

For detailed instructions, see:
- [docs/PREMIUM_IMAGES_GUIDE.md](docs/PREMIUM_IMAGES_GUIDE.md) — Complete guide with all options

---

## Summary

**Code changes:** ✅ Complete
**Your task:** Add 6 WebP images to `frontend/public/assets/images/`
**Testing:** Run `pnpm dev` and check home page products section
**Time:** 15-30 minutes to source and process images

**Files ready for images:**
```
frontend/public/assets/images/
├── vannamei-shrimp.webp       ← ADD THIS
├── black-tiger-shrimp.webp    ← ADD THIS
├── squid.webp                 ← ADD THIS
├── cuttlefish.webp            ← ADD THIS
├── dried-shrimp.webp          ← ADD THIS
└── pink-perch.webp            ← ADD THIS
```

Once images are in place, the site will automatically display them with premium styling in both light and dark themes.

---

**Need help?** Check [docs/PREMIUM_IMAGES_GUIDE.md](docs/PREMIUM_IMAGES_GUIDE.md) for detailed instructions, search queries, and troubleshooting.

# Premium Product Images — Sourcing & Integration Guide

**Status:** 🎨 Ready for Image Integration
**Impact:** Visual upgrade to enterprise-grade product presentation

---

## Image Requirements

### Technical Specifications

| Property | Requirement |
|----------|-------------|
| **Format** | WebP (primary), JPG (fallback) |
| **Resolution** | 800×800px minimum, 1200×1200px recommended |
| **Aspect Ratio** | 1:1 (square) for uniform card display |
| **File Size** | <150KB per image (WebP optimized) |
| **Background** | Transparent PNG or clean white/neutral background |
| **Color Profile** | sRGB for consistent display |

### Visual Requirements

1. **Crystal Clear Quality**
   - Professional food photography
   - Sharp focus on product
   - Natural lighting (soft, diffused)
   - High detail visible in texture

2. **Theme Compatibility**
   - Must look premium in both light and dark themes
   - Avoid harsh shadows or extreme contrast
   - Neutral or transparent background preferred
   - If on plate, use elegant white or light ceramic

3. **Composition**
   - Product centered in frame
   - Slight top-down angle (15-30°) or 45° angle
   - Generous padding around subject
   - Professional plating if served

4. **Enterprise-Grade Aesthetic**
   - Restaurant/hotel quality presentation
   - Premium plating (white ceramic, slate, or transparent)
   - Garnish minimal or absent (focus on product)
   - Clean, professional food styling

---

## Product-Specific Image Requirements

### 1. Vannamei Whiteleg Shrimp
- **File name:** `vannamei-shrimp.webp`
- **Description:** Large, fresh vannamei shrimp
- **Ideal shot:** 3-5 raw shrimp arranged in a fan or circular pattern
- **Background:** White plate or transparent
- **Key features:** Show natural white/pink color, curved shape, visible texture

### 2. Black Tiger Shrimp
- **File name:** `black-tiger-shrimp.webp`
- **Description:** Premium black tiger prawns
- **Ideal shot:** 2-3 large prawns showing distinctive black stripes
- **Background:** Dark slate or white plate for contrast
- **Key features:** Emphasize size, distinctive striped pattern, curved form

### 3. Squid (Loligo)
- **File name:** `squid.webp`
- **Description:** Whole squid or cleaned tubes
- **Ideal shot:** 1-2 whole squid or sliced rings
- **Background:** White or light blue surface
- **Key features:** Show translucent white flesh, tentacles if whole

### 4. Cuttlefish
- **File name:** `cuttlefish.webp`
- **Description:** Cleaned cuttlefish
- **Ideal shot:** Cuttlefish body showing texture
- **Background:** Neutral, light surface
- **Key features:** Show firm white flesh, distinctive texture

### 5. Dried Shrimp
- **File name:** `dried-shrimp.webp`
- **Description:** Small dried shrimp
- **Ideal shot:** Pile or scattered arrangement of dried shrimp
- **Background:** Wooden bowl or white surface
- **Key features:** Show golden-orange color, compact size, texture

### 6. Pink Perch (Threadfin Bream)
- **File name:** `pink-perch.webp`
- **Description:** Whole or filleted pink perch
- **Ideal shot:** 1-2 whole fish or clean fillets
- **Background:** White or ice bed
- **Key features:** Show pink-silver skin, fresh appearance

---

## Image Sourcing Options

### Option 1: Premium Stock Photography (Recommended)

**Shutterstock**
- Search: "fresh vannamei shrimp white background"
- Search: "black tiger prawn premium"
- License: Standard or Enhanced (commercial use)
- Cost: ~$29-49 per image (or subscription)

**iStock by Getty Images**
- High-quality seafood photography
- Professional food styling
- License: Standard commercial

**Adobe Stock**
- Integration with Creative Cloud
- Excellent seafood collection
- License: Standard

### Option 2: Free Stock Photography (Good Quality)

**Unsplash** (https://unsplash.com)
- Search: "shrimp seafood", "prawn food photography"
- License: Free for commercial use
- Quality: Variable, but many professional shots

**Pexels** (https://pexels.com)
- Search: "seafood", "shrimp", "prawn"
- License: Free for commercial use
- Quality: Good, improving collection

**Pixabay** (https://pixabay.com)
- Large seafood collection
- License: Free for commercial use
- Quality: Mixed, requires curation

### Option 3: Custom Photography

**Hire Professional Food Photographer**
- Best for brand consistency
- Full control over styling and composition
- Cost: $500-2000 for 6 product shots (India rates)
- Recommended for long-term branding

**DIY with High-Quality Setup**
- DSLR or mirrorless camera
- Softbox lighting or natural window light
- White backdrop or premium plates
- Macro lens recommended
- Cost: Equipment investment, but reusable

---

## Image Processing Workflow

### Step 1: Download Source Images
```bash
# Create temp directory for processing
mkdir -p /tmp/alashore-images
cd /tmp/alashore-images
```

Download high-resolution JPG/PNG images for all 6 products.

### Step 2: Background Removal (if needed)

**Using remove.bg (Online Tool)**
1. Visit https://remove.bg
2. Upload image
3. Download PNG with transparent background
4. Free tier: 50 images/month

**Using Photoshop/GIMP**
1. Open image
2. Use Magic Wand or Quick Selection tool
3. Select and delete background
4. Export as PNG with transparency

**Using CLI (ImageMagick)**
```bash
# Remove white background
convert input.jpg -fuzz 10% -transparent white output.png
```

### Step 3: Crop and Resize

```bash
# Install ImageMagick (if not installed)
brew install imagemagick  # macOS
# sudo apt-get install imagemagick  # Linux

# Crop to square and resize to 1200x1200
convert input.png -gravity center -extent 1:1 -resize 1200x1200 output.png

# Batch process all images
for img in *.png; do
  convert "$img" -gravity center -extent 1:1 -resize 1200x1200 "resized_$img"
done
```

### Step 4: Convert to WebP

```bash
# Install cwebp (WebP encoder)
brew install webp  # macOS
# sudo apt-get install webp  # Linux

# Convert single image
cwebp -q 85 input.png -o output.webp

# Batch convert with optimization
for img in resized_*.png; do
  name=$(basename "$img" .png)
  cwebp -q 85 -m 6 "$img" -o "${name}.webp"
done
```

### Step 5: Optimize File Size

```bash
# Target: <150KB per image
# Adjust quality if needed
cwebp -q 75 input.png -o output.webp  # Lower quality
cwebp -q 90 input.png -o output.webp  # Higher quality

# Check file size
ls -lh *.webp
```

### Step 6: Move to Project

```bash
# Copy processed images to project
cp vannamei-shrimp.webp /Volumes/hex/current-work/alashore-marine/frontend/public/assets/images/
cp black-tiger-shrimp.webp /Volumes/hex/current-work/alashore-marine/frontend/public/assets/images/
cp squid.webp /Volumes/hex/current-work/alashore-marine/frontend/public/assets/images/
cp cuttlefish.webp /Volumes/hex/current-work/alashore-marine/frontend/public/assets/images/
cp dried-shrimp.webp /Volumes/hex/current-work/alashore-marine/frontend/public/assets/images/
cp pink-perch.webp /Volumes/hex/current-work/alashore-marine/frontend/public/assets/images/
```

---

## Integration Checklist

### Phase 1: Image Preparation
- [ ] Source 6 high-quality product images
- [ ] Remove backgrounds or ensure clean background
- [ ] Crop to 1:1 aspect ratio
- [ ] Resize to 1200×1200px
- [ ] Convert to WebP format
- [ ] Optimize file size (<150KB each)
- [ ] Test visibility on light and dark backgrounds

### Phase 2: Code Integration (Automated)
- [ ] Update product markdown files (image_url paths)
- [ ] Add CSS for premium image display
- [ ] Implement theme-aware styling
- [ ] Add lazy loading and responsive sizing
- [ ] Update ProductCard component if needed

### Phase 3: Testing
- [ ] Test all 6 products in light theme
- [ ] Test all 6 products in dark theme
- [ ] Verify responsive behavior (mobile/tablet/desktop)
- [ ] Check image centering and aspect ratio
- [ ] Verify loading performance
- [ ] Ensure no functionality regression

### Phase 4: Deployment
- [ ] Run local CI: `pnpm ci:local`
- [ ] Build production: `pnpm build`
- [ ] Preview locally: `pnpm preview:dist`
- [ ] Commit changes with descriptive message
- [ ] Push to GitHub
- [ ] Manually trigger deployment workflow

---

## Example Image Search Queries

### For Unsplash/Pexels

1. **Vannamei Shrimp**
   - "fresh raw shrimp white background"
   - "vannamei prawn food photography"
   - "white shrimp premium seafood"

2. **Black Tiger Shrimp**
   - "black tiger prawn striped"
   - "large tiger shrimp raw"
   - "penaeus monodon seafood"

3. **Squid**
   - "fresh squid seafood"
   - "loligo squid tubes"
   - "calamari raw white background"

4. **Cuttlefish**
   - "cuttlefish sepia seafood"
   - "fresh cuttlefish white"
   - "cuttlefish fillet raw"

5. **Dried Shrimp**
   - "dried shrimp golden"
   - "small dried prawns bowl"
   - "dehydrated shrimp seafood"

6. **Pink Perch**
   - "threadfin bream fish"
   - "fresh fish white background"
   - "pink perch whole fish ice"

---

## CSS Implementation (Automated)

The following CSS will be added automatically once images are in place:

```css
/* Premium product image styling */
.product-card img {
  width: 100%;
  height: auto;
  aspect-ratio: 1 / 1;
  object-fit: contain;
  object-position: center;
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.product-card:hover img {
  transform: scale(1.05);
}

/* Theme-aware image background */
.product-card img {
  background: linear-gradient(135deg, #ffffff 0%, #f8f9fa 100%);
  border-radius: 12px;
  padding: 1.5rem;
}

[data-theme="dark"] .product-card img {
  background: linear-gradient(135deg, #1a1a1a 0%, #2d2d2d 100%);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
}

/* Lazy loading placeholder */
.product-card img[loading="lazy"] {
  background: linear-gradient(135deg, #e0e0e0 0%, #f0f0f0 100%);
}

[data-theme="dark"] .product-card img[loading="lazy"] {
  background: linear-gradient(135deg, #1a1a1a 0%, #2d2d2d 100%);
}
```

---

## Quick Start Command

Once you have the 6 images processed and ready:

```bash
# Navigate to project root
cd /Volumes/hex/current-work/alashore-marine

# Copy images to assets
cp /tmp/alashore-images/*.webp frontend/public/assets/images/

# Let Claude update the code automatically
# Provide this command to Claude:
# "Images are in frontend/public/assets/images/. Update all product configs and CSS for premium display."
```

---

## Troubleshooting

### Images not displaying
- Check file paths match exactly (case-sensitive)
- Verify images are in `frontend/public/assets/images/`
- Clear browser cache: Cmd+Shift+R (macOS) / Ctrl+Shift+R (Windows)
- Check browser console for 404 errors

### Images look bad in dark theme
- Ensure transparent background OR neutral light background
- Add CSS filter for dark mode if needed: `filter: brightness(0.9);`
- Consider adding subtle shadow: `box-shadow: 0 4px 12px rgba(255,255,255,0.1);`

### Images too large (slow loading)
- Re-encode WebP with lower quality: `cwebp -q 70`
- Ensure size is 1200×1200px max
- Use lazy loading (already implemented in code)

### Images not centered
- Verify CSS `object-fit: contain` is applied
- Check `object-position: center`
- Inspect element in browser DevTools

---

## Cost Estimate

| Option | Cost | Timeline | Quality |
|--------|------|----------|---------|
| **Premium Stock (Shutterstock)** | $29-49/image × 6 = $174-294 | Immediate | Excellent |
| **Stock Subscription** | $29-99/month (unlimited) | Immediate | Excellent |
| **Free Stock (Unsplash/Pexels)** | $0 | 1-2 hours curation | Good to Very Good |
| **Professional Photography** | $500-2000 | 1-2 weeks | Excellent + Brand Control |
| **DIY Photography** | $50-500 (equipment) | 1-2 days + learning | Variable |

**Recommended for MVP:** Free Stock (Unsplash/Pexels) → Professional photography later for brand consistency.

---

## Legal Compliance

### Attribution Requirements
- **Unsplash:** No attribution required, but appreciated
- **Pexels:** No attribution required
- **Pixabay:** No attribution required
- **Commercial Stock:** Must comply with license (usually no attribution needed)

### License Verification
Always verify license allows:
- ✅ Commercial use
- ✅ Modification
- ✅ No attribution required (preferred)
- ✅ Web use

### Image Credits (Optional)
If you want to credit photographers, add to footer:
```
Product photography by [Photographer Name] on [Platform]
```

---

**Last Updated:** 2026-04-19
**Next Action:** Source and process 6 premium product images following specifications above.

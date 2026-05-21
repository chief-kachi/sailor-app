# Sailor MVP App

The AI-powered fashion avatar generator for **Sailor** — create editorial-quality avatars in 3 steps.

## 🎨 Overview

**Sailor MVP** is a SvelteKit application that delivers the core Sailor experience:

1. **Upload Face** - Scan and personalize with your facial features
2. **Build Outfit** - Layer fashion elements (shirt, pants, shoes, accessories)
3. **Generate Avatar** - AI-powered avatar generation using DALL-E

## 🚀 Tech Stack

- **Framework**: SvelteKit
- **Language**: TypeScript
- **Styling**: Tailwind CSS
- **AI**: OpenAI DALL-E 3 API
- **State Management**: SvelteKit stores
- **Storage**: IndexedDB (offline support)
- **Deployment**: Vercel/Netlify

## 📦 Installation

```bash
# Clone the repository
git clone https://github.com/chief-kachi/sailor-app.git
cd sailor-app

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env.local

# Run development server
npm run dev
```

Open [http://localhost:5173](http://localhost:5173) in your browser.

## 📁 Project Structure

```
sailor-app/
├── src/
│   ├── routes/
│   │   ├── +page.svelte           # Main landing/entry
│   │   ├── +layout.svelte         # Root layout
│   │   ├── step-1-upload/
│   │   │   └── +page.svelte       # Face upload step
│   │   ├── step-2-outfit/
│   │   │   └── +page.svelte       # Outfit builder step
│   │   ├── step-3-generate/
│   │   │   └── +page.svelte       # Avatar generation step
│   │   ├── gallery/
│   │   │   └── +page.svelte       # Saved avatars gallery
│   │   └── api/
│   │       ├── generate/
│   │       │   └── +server.ts     # DALL-E API endpoint
│   │       └── save-avatar/
│   │           └── +server.ts     # Save avatar endpoint
│   ├── lib/
│   │   ├── stores/
│   │   │   ├── user.ts            # User face upload data
│   │   │   ├── outfit.ts          # Outfit selections
│   │   │   ├── gallery.ts         # Saved avatars
│   │   │   └── settings.ts        # App settings (theme, etc.)
│   │   ├── api/
│   │   │   ├── openai.ts          # DALL-E integration
│   │   │   └── storage.ts         # IndexedDB utilities
│   │   ├── components/
│   │   │   ├── FaceUpload.svelte
│   │   │   ├── OutfitBuilder.svelte
│   │   │   ├── AvatarPreview.svelte
│   │   │   ├── Gallery.svelte
│   │   │   └── Navigation.svelte
│   │   └── utils/
│   │       ├── prompt-generator.ts # DALL-E prompt crafting
│   │       └── image-utils.ts     # Image processing
│   ├── app.css                    # Global styles
│   └── app.html                   # HTML template
├── static/
│   └── assets/                    # Brand assets, icons
├── .env.example
├── svelte.config.js
├── vite.config.ts
├── tailwind.config.ts
├── tsconfig.json
└── package.json
```

## 🎯 Core Features

### Step 1: Upload Face
- Camera capture or file upload
- Face detection & normalization
- Facial feature extraction
- Preview before proceeding

### Step 2: Build Outfit
- **Shirt**: Color, pattern, style (casual, formal, streetwear)
- **Pants**: Style (jeans, cargo, trousers, skirt)
- **Shoes**: Type (sneakers, boots, heels, loafers)
- **Accessories**: Hats, bags, jewelry
- **Aesthetic**: Preset categories (Tokyo Streetwear, Cyber Couture, etc.)
- Real-time preview with outfit layers

### Step 3: Generate Avatar
- AI prompt generation from uploaded face + outfit selections
- DALL-E 3 API integration
- High-quality portrait generation
- Watermark with Sailor branding
- Download, save, or share options

### Gallery & Sharing
- Save generated avatars locally (IndexedDB)
- Tag and organize by aesthetic/date
- Export with Sailor watermark
- Share to social media (Twitter, Instagram)
- Offline sync when reconnected

## 🔗 Environment Variables

Create a `.env.local` file:

```env
# OpenAI DALL-E API
VITE_OPENAI_API_KEY=sk-your-key-here
VITE_OPENAI_API_ENDPOINT=https://api.openai.com/v1/images/generations

# App Configuration
VITE_APP_NAME=Sailor
VITE_APP_URL=http://localhost:5173
VITE_LANDING_URL=http://localhost:3000

# Feature Flags
VITE_ENABLE_OFFLINE_MODE=true
VITE_ENABLE_SHARING=true
VITE_ENABLE_GALLERY=true
```

## 📋 Outfit Categories

### Shirts
- T-Shirt
- Button-Up
- Oversized Blazer
- Crop Top
- Tank Top
- Long-Sleeve

### Pants
- Jeans
- Cargo Pants
- Trousers
- Skirt
- Shorts
- Leggings

### Shoes
- Sneakers
- Combat Boots
- Heels
- Loafers
- Sandals
- Platform Boots

### Accessories
- Baseball Cap
- Beanie
- Sunglasses
- Chain Necklace
- Backpack
- Tote Bag

### Aesthetics
- Tokyo Streetwear
- Cyber Couture
- Noir Minimalist
- Futuristic Athlete
- Avant-Garde Editorial
- Y2K Revival
- Maximalist Glam

## 🚢 Deployment

### Vercel

```bash
npm i -g vercel
vercel
```

### Netlify

```bash
npm run build
# Deploy the 'build' folder
```

## 📊 API Endpoints

### Generate Avatar

```
POST /api/generate
Content-Type: application/json

{
  "faceImage": "base64-encoded-image",
  "outfit": {
    "shirt": "Oversized Blazer",
    "pants": "Cargo Pants",
    "shoes": "Combat Boots",
    "accessories": ["Beanie", "Chain Necklace"],
    "aesthetic": "Cyber Couture",
    "mood": "cinematic, editorial, professional lighting"
  }
}

Response:
{
  "avatarUrl": "https://...",
  "prompt": "Generated DALL-E prompt",
  "timestamp": "2026-05-21T10:30:00Z"
}
```

### Save Avatar

```
POST /api/save-avatar
Content-Type: application/json

{
  "avatarUrl": "https://...",
  "outfit": { ... },
  "tags": ["cyberpunk", "streetwear"]
}

Response:
{
  "id": "avatar-uuid",
  "saved": true
}
```

## 🎨 Styling

- **Tailwind CSS** for utility-first styling
- **Dark mode optimized** (matching landing page)
- **Glassmorphism effects** for modern UI
- **Smooth animations** with Svelte transitions

## 🔄 State Management

### Stores

```
user.ts         → Face upload, personal data
outfit.ts       → Selected outfit pieces & aesthetic
gallery.ts      → Saved avatars, tags
settings.ts     → Theme, notifications, preferences
```

## 📱 Offline Mode

- IndexedDB caching of generated avatars
- Queue generation requests when offline
- Sync to cloud when connection restored
- Local avatar editing

## 🎬 User Flow

```
Landing → Step 1 (Upload Face)
       → Step 2 (Build Outfit)
       → Step 3 (Generate Avatar)
       → Gallery (Save/Share/Tag)
```

## 📝 Development

### Scripts

```bash
npm run dev       # Start dev server
npm run build     # Build for production
npm run preview   # Preview production build
npm run lint      # Run ESLint
```

### Component Pattern

```svelte
<script lang="ts">
  import { outfit } from '$lib/stores/outfit';

  let isLoading = false;

  async function handleGenerate() {
    isLoading = true;
    // Call API
    isLoading = false;
  }
</script>

<div class="container">
  <!-- Component JSX -->
</div>

<style>
  /* Scoped styles */
</style>
```

## 🧪 Testing

```bash
npm run test      # Run tests
npm run test:ui   # Open test UI
```

## 📄 License

MIT License

## 🎬 Related Projects

- **[Sailor Landing Page](https://github.com/chief-kachi/sailor-landing)** - Marketing website (Next.js)

---

**Last Updated**: 2026-05-21  
**Status**: MVP Development  
**Maintainer**: @chief-kachi

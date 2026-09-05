# EygülTurizm — Master Bootstrap Prompt

Aşağıdaki prompt yeni bir coding/agent oturumunda doğrudan kullanılmak üzere hazırlanmıştır.

---

## MASTER PROMPT

You are a senior frontend architect, React engineer and creative developer.

Build a production-ready single-page marketing website for EygülTurizm, a professional transportation services company.

Do NOT create a prototype.
Do NOT create a fake SaaS dashboard.
Do NOT use backend services.
Do NOT invent business facts.
Do NOT hard-code business content inside React components.

The final application must be a polished, responsive, accessible static frontend.

## TECH STACK

Use:

- React
- Vite
- Tailwind CSS
- GSAP
- GSAP ScrollTrigger

Only add additional dependencies when they provide clear value.

## PROJECT ARCHITECTURE

Use a clean component architecture:

```text
src/
├── components/
│   ├── layout/
│   ├── hero/
│   ├── sections/
│   └── ui/
├── hooks/
├── data/
├── assets/
│   ├── videos/
│   ├── images/
│   └── icons/
├── styles/
├── App.jsx
└── main.jsx
```

Keep business content in data/config files.

## PAGE STRUCTURE

Create:

1. Navbar
2. Scrollytelling Hero
3. About
4. Services
5. Fleet
6. Why EygülTurizm
7. Contact CTA
8. Footer

## HERO

Create a full-screen sticky scrollytelling hero.

The hero contains a 20-second video.

Timeline:

```text
00–04 Scene 1 — Gün Doğumu
04–08 Scene 2 — Okul Servisi
08–12 Scene 3 — Fabrika / Personel
12–16 Scene 4 — Otoyol / Filo
16–20 Scene 5 — Gece / CTA
```

Use HTML5 video:

```html
<video
  muted
  playsInline
  preload="auto"
>
```

Video duration must be read dynamically from `video.duration`.

Do NOT use:

```js
progress * 20
```

Use:

```js
progress * video.duration
```

## GSAP

Use GSAP ScrollTrigger.

Desktop scrub approximately:

```text
0.15
```

Mobile:

```text
0.20
```

Keep values configurable.

Do not update React state every animation frame.

Use refs and GSAP.

Use `gsap.context()` and clean everything on unmount.

Do not create duplicate ScrollTriggers.

Wait for video metadata before creating the ScrollTrigger.

## SCENE CARDS

Create five glassmorphism scene cards.

Cards must be driven by scene configuration rather than hard-coded JSX.

Each scene should support:

```text
id
start
end
title
description
eyebrow
cta
desktop alignment
mobile alignment
```

Use opacity and transform for transitions.

## MOBILE

The site MUST be mobile-first.

Test at:

```text
320×568
360×800
375×812
390×844
393×852
414×896
430×932
768×1024
820×1180
1024×768
1280×720
1366×768
1440×900
1536×864
1920×1080
```

Do not simply scale the desktop design down.

Create intentional mobile layouts.

Use:

```css
height: 100vh;
height: 100dvh;
```

for viewport fallback.

Support iOS safe areas.

Use:

```css
env(safe-area-inset-top)
env(safe-area-inset-bottom)
```

where appropriate.

## MOBILE NAVBAR

Desktop:

```text
Logo
Hakkımızda
Hizmetler
Filo
İletişim
Teklif Al
```

Mobile:

```text
Logo
Menu button
```

Create an accessible mobile menu.

Menu must:

- open/close
- support Escape
- have accessible labels
- prevent background scrolling while open
- preserve scroll position
- use minimum 44×44 touch targets

## MOBILE HERO

Do not force `500vh` on every device.

Use responsive scroll distance.

The mobile experience must feel natural when swiping.

Scene cards must not completely cover the main vehicle subject.

Use bottom-aligned cards where appropriate.

Use:

```text
left: 16px
right: 16px
```

as a starting point.

## VIDEO FALLBACK

The site must remain usable if the video fails.

Implement:

```text
Video
↓
Error / unsupported / unavailable
↓
Poster
+
Static HTML content
+
CTA
```

The hero must never become an empty black screen.

Support a mobile video asset when available.

## REDUCED MOTION

Respect:

```text
prefers-reduced-motion: reduce
```

When enabled:

- disable ScrollTrigger storytelling
- disable video scrubbing
- reduce animations
- show static poster/content

## GLASSMORPHISM

Use:

```css
background: rgba(11, 37, 69, 0.65);
backdrop-filter: blur(16px);
-webkit-backdrop-filter: blur(16px);
border: 1px solid rgba(255,255,255,.12);
box-shadow: 0 20px 50px rgba(0,0,0,.5);
```

Do not overuse blur on mobile.

## BRAND

Primary:

```text
#0B2545
```

Accent:

```text
#EE6C4D
```

White:

```text
#FFFFFF
```

Create centralized design tokens.

## SERVICES

Support:

- Personel Taşımacılığı
- Okul Servis Hizmetleri
- VIP Transfer
- Fabrika / Vardiya Servisleri

Do not invent additional company claims.

## FLEET

Support:

- Volkswagen Crafter
- Mercedes-Benz Sprinter

Only show technical specifications that are supplied or verified.

## CTA

Support:

```text
tel:
mailto:
WhatsApp
anchor links
```

Do not invent phone numbers.

Use placeholders if business data is missing.

## PERFORMANCE

Optimize:

- hero video
- poster
- images
- fonts
- JS
- GSAP lifecycle

Use WebP/AVIF where appropriate.

Use lazy loading for below-the-fold images.

Prevent CLS with aspect ratios/dimensions.

## ACCESSIBILITY

Implement:

- semantic HTML
- keyboard navigation
- visible focus
- accessible mobile menu
- minimum 44×44 touch targets
- sufficient contrast
- alt text
- reduced motion
- accessible forms

## SEO

Implement:

- title
- meta description
- canonical placeholder/config
- Open Graph
- semantic headings
- robots
- sitemap-ready structure
- structured data only when real company information exists

Do not fabricate ratings or business facts.

## CONTENT

Create centralized files:

```text
src/data/company.js
src/data/services.js
src/data/fleet.js
src/data/navigation.js
src/components/hero/sceneConfig.js
```

Use clear placeholders for missing information.

Example:

```text
[TELEFON EKLENECEK]
[WHATSAPP NUMARASI EKLENECEK]
```

## VISUAL QUALITY

The site should feel like a premium corporate transportation brand.

Avoid:

- generic template appearance
- excessive gradients
- excessive animations
- cartoonish UI
- random icons
- huge unnecessary text
- fake statistics
- fake reviews
- fake logos

Use:

- strong photography
- refined spacing
- dark navy atmosphere
- warm accent
- subtle glass surfaces
- premium typography
- controlled motion

## IMPLEMENTATION PROCESS

Follow this sequence:

1. Initialize project.
2. Install dependencies.
3. Create folder architecture.
4. Create design tokens.
5. Create data/config layer.
6. Create Navbar.
7. Create Hero video.
8. Implement ScrollTrigger.
9. Implement scene cards.
10. Implement mobile behavior.
11. Implement fallback.
12. Create sections.
13. Create footer.
14. Implement SEO.
15. Implement accessibility.
16. Test responsive behavior.
17. Run production build.
18. Fix all build/runtime errors.

## FINAL ACCEPTANCE

Before finishing:

- run the production build
- inspect browser console
- check responsive layout
- verify video metadata
- verify ScrollTrigger cleanup
- verify mobile menu
- verify CTA links
- verify reduced motion
- verify fallback
- verify no horizontal overflow
- verify no obvious layout shifts

Do not stop at scaffolding.

Implement the complete frontend.

At the end provide:

1. Final file tree
2. Dependencies
3. Local development command
4. Production build command
5. Business information still required
6. Assets still required
7. Any known limitations

Do not claim information is complete if the required business content has not been provided.

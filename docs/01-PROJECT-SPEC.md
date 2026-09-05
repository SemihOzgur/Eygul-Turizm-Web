# EygülTurizm — Project Specification

Production-ready, static React marketing website.

## Stack

- React
- Vite
- Tailwind CSS
- GSAP
- ScrollTrigger

## Main experience

A 20-second hero video is controlled by scroll position.

## Page

Navbar → Hero → About → Services → Fleet → Why EygülTurizm → Contact CTA → Footer.

## Architecture

Keep components, animation logic and business content separate.

Recommended:

```text
src/
├── components/
├── hooks/
├── data/
├── assets/
└── styles/
```

## Business data

Phone, email, WhatsApp, address, services, fleet details, statistics and claims must come from user-provided content.

Never invent factual company information.

## Hero

Five 4-second scenes:

1. Sunrise
2. School
3. Factory/personnel
4. Highway/fleet
5. Night/CTA

Video duration is dynamic.

## Glass

Use dark navy translucent glass, blur, subtle white border and controlled shadow.

## Responsive

Mobile-first and intentional. See `02-RESPONSIVE-SPEC.md`.

## Animation

See `03-SCROLLYTELLING-SPEC.md`.

## Design

See `04-DESIGN-SYSTEM.md`.

## Content

See `05-CONTENT-MODEL.md`.

## Performance

See `06-PERFORMANCE.md`.

## Accessibility

See `07-ACCESSIBILITY.md`.

## SEO

See `08-SEO-SPEC.md`.

## Deployment

See `09-DEPLOYMENT.md`.

## User input

See `10-USER-PROVIDED-CONTENT.md`.

## Bootstrap

See `11-MASTER-BOOTSTRAP-PROMPT.md`.

## Definition of done

Production build succeeds, hero works, responsive layouts work, video fallback exists, reduced motion works, CTAs work, SEO/accessibility basics exist and console is clean.

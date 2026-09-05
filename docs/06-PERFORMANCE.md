# EygülTurizm — Performance Specification

## 1. Goal

Özellikle mobil cihazlarda hızlı ilk açılış, düşük layout shift ve akıcı scroll deneyimi hedeflenir.

## 2. Video

Hero video optimize edilmelidir.

Tercih:

```text
Desktop: optimized 1920×1080 MP4
Mobile: dedicated mobile asset when beneficial
Poster: optimized WebP/AVIF
```

Video gereksiz yüksek bitrate ile servis edilmemelidir.

## 3. Video preload

Hero ana deneyim olduğu için:

```html
preload="auto"
```

kullanılabilir.

Ancak düşük bağlantı / data saver durumları için poster fallback'i bulunmalıdır.

## 4. Images

Hero dışındaki görseller:

```html
loading="lazy"
```

kullanmalıdır.

Modern format:

- AVIF
- WebP

önceliklidir.

## 5. Dimensions

Görsellerin boyutları veya aspect ratio'ları önceden tanımlanmalıdır.

Amaç CLS'yi azaltmaktır.

## 6. JavaScript

Scroll sırasında:

```text
React setState
```

her frame tetiklenmemelidir.

GSAP animation state'i doğrudan DOM/ref üzerinden yönetmelidir.

## 7. GSAP

Tekrarlayan ScrollTrigger instance'ları oluşturulmamalıdır.

Unmount sırasında cleanup zorunludur.

## 8. Blur

`backdrop-filter` mobilde pahalı olabilir. Aynı anda çok sayıda büyük blur panel kullanılmamalıdır.

## 9. Fonts

Web font kullanılıyorsa:

```text
font-display: swap
```

tercih edilmelidir.

Gereksiz font ağırlıkları yüklenmemelidir.

## 10. Code splitting

Gerçek ihtiyaç oluşmadıkça agresif code splitting yapılmamalıdır. Basit landing page için gereksiz complexity eklenmemelidir.

## 11. Performance testing

Kontrol:

- Lighthouse Performance
- Lighthouse Accessibility
- Lighthouse Best Practices
- Lighthouse SEO
- Chrome Performance
- Mobile throttling

## 12. Performance acceptance

- [ ] No obvious long tasks on initial load.
- [ ] No continuous React render loop during scrolling.
- [ ] No duplicate animation instances.
- [ ] Images optimized.
- [ ] Video optimized.
- [ ] CLS minimized.
- [ ] Mobile fallback works.

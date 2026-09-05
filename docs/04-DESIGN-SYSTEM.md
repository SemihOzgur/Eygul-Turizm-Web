# EygülTurizm — Design System

## 1. Design direction

Marka dili:

- premium
- güvenilir
- modern
- kurumsal
- sakin
- yüksek kalite
- ulaşılabilir

Tasarım aşırı teknoloji/startup görünümüne kaymamalıdır.

## 2. Colors

```text
Primary Navy: #0B2545
Accent: #EE6C4D
White: #FFFFFF
```

Accent gerektiğinde CTA ve önemli vurgu için kullanılmalıdır.

## 3. Glass

```css
background: rgba(11, 37, 69, 0.65);
backdrop-filter: blur(16px);
-webkit-backdrop-filter: blur(16px);
border: 1px solid rgba(255,255,255,.12);
box-shadow: 0 20px 50px rgba(0,0,0,.5);
```

Glass yüzeyler içerik okunabilirliğini bozmayacak şekilde kullanılmalıdır.

## 4. Radius

Öneri:

```text
Buttons: 12–16px
Cards: 20–24px
Large panels: 24–32px
```

## 5. Spacing

Temel sistem 4/8 tabanlı olabilir:

```text
4
8
12
16
20
24
32
40
48
64
80
96
120
144
```

## 6. Container

```text
Mobile: 16–20px side padding
Tablet: 24–40px
Desktop: max-width 1200–1280px
Large: max-width 1400px
```

## 7. Typography

Hiyerarşi:

```text
Hero H1: 42–76px desktop / 30–42px mobile
H2: 36–56px desktop / 28–36px mobile
H3: 20–28px
Body: 16–18px
Small: 14–15px
```

Final değerler `clamp()` ile ayarlanabilir.

## 8. Buttons

Minimum touch target:

```text
44×44px
```

Önerilen button height:

```text
48–52px
```

CTA'larda net fiiller kullanılmalıdır:

- Teklif Al
- Hemen Ara
- WhatsApp'tan Ulaş

## 9. Icons

Lucide veya benzeri tutarlı outline icon sistemi kullanılabilir.

Emoji UI icon olarak kullanılmamalıdır.

## 10. Motion

Premium motion:

- kısa
- yumuşak
- kontrollü
- dikkat dağıtmayan

olmalıdır.

Aşırı bounce, rotate ve elastic efektlerden kaçınılmalıdır.

## 11. Images

Görseller:

- gerçekçi
- yüksek kaliteli
- marka ile uyumlu
- mümkünse WebP/AVIF

olmalıdır.

Araç görsellerinde logo ve araç bütünlüğü korunmalıdır.

## 12. Section style

Her section farklı bir görsel dünya gibi tasarlanmamalıdır. Tek bir marka dili korunmalıdır.

## 13. Dark aesthetic

Hero ve kritik CTA alanlarında dark navy atmosfer kullanılabilir. Tüm siteyi tamamen siyah yapmak tercih edilmemelidir.

## 14. Accessibility

Text contrast, focus states ve reduced motion tasarım sisteminin parçasıdır.

## 15. Design tokens

Renk, radius, spacing, shadow ve typography mümkün olduğunca merkezi CSS variables/Tailwind tokens üzerinden yönetilmelidir.

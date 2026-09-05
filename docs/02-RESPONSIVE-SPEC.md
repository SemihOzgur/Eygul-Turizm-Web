# EygülTurizm — Responsive & Mobile Specification

## 1. Purpose

Bu doküman sitenin mobile-first, tablet, desktop ve large desktop davranışlarını tanımlar. Responsive davranış yalnızca genişlik değişimi değil; navigation, hero, video crop, scene cards, typography, CTA, touch, viewport, safe-area, animation ve performance davranışlarını kapsar.

## 2. Core principle

Desktop tasarım küçültülerek mobile dönüştürülmeyecektir.

Öncelik:

```text
Mobile → Tablet → Desktop → Large Desktop
```

## 3. Breakpoints

Mantıksal ekran grupları:

| Grup | Genişlik |
|---|---:|
| Extra Small | <375px |
| Mobile | 375–767px |
| Tablet | 768–1023px |
| Desktop | 1024–1279px |
| Large Desktop | 1280–1535px |
| XL | 1536px+ |

Tailwind karşılıkları kullanılabilir:

```text
sm 640
md 768
lg 1024
xl 1280
2xl 1536
```

## 4. Container

Mobile:

```css
width: 100%;
padding-inline: 16px;
```

Tablet:

```text
24–40px
```

Desktop:

```text
max-width: 1200–1280px
```

Large desktop:

```text
max-width: 1400px
```

`100vw` kaynaklı scrollbar taşmalarından kaçınılmalıdır.

## 5. Horizontal overflow

Site hiçbir normal durumda yatay scroll üretmemelidir.

Özellikle kontrol:

- video
- navbar
- glass cards
- images
- CTA groups
- footer
- long headings
- long URLs

`overflow-x:hidden` tek başına çözüm olarak kullanılmamalı; taşmanın kaynağı düzeltilmelidir.

## 6. Extra-small screens

320px ve 360px ekranlarda:

- içerik taşmayacak
- başlıklar ekran dışına çıkmayacak
- CTA'lar gerektiğinde alt alta inecek
- card padding azaltılacak
- logo gerektiğinde küçülecek
- navbar sıkışmayacak

## 7. Mobile navbar

Mobile navbar yaklaşık 64–76px olmalıdır.

Desktop navigation yerine logo + menu button gösterilir.

Menu:

- accessible
- touch-friendly
- Escape ile kapanabilir
- body scroll lock destekli
- minimum 44×44px button

olmalıdır.

## 8. Safe area

iOS için gerektiğinde:

```css
padding-top: env(safe-area-inset-top);
padding-bottom: env(safe-area-inset-bottom);
```

kullanılmalıdır.

## 9. Mobile menu scroll lock

Menu açıkken arka sayfa scroll edilmemelidir.

Menu kapanınca kullanıcı önceki scroll pozisyonunda kalmalıdır.

## 10. Hero viewport

Hero sticky viewport:

```css
height: 100vh;
height: 100dvh;
```

şeklinde fallback içermelidir.

`100dvh` mobile dynamic viewport için tercih edilir.

## 11. Hero scroll distance

Desktop yaklaşık `400vh–500vh` kullanabilir.

Mobile'da 500vh zorunlu değildir. Başlangıç olarak scene count × viewport yaklaşımı kullanılabilir.

Beş scene için yaklaşık:

```text
5 × 100dvh
```

uygulanabilir; gerçek değer UX testine göre ayarlanmalıdır.

## 12. Hero video

Video:

```html
<video
  muted
  playsInline
  preload="auto"
  poster="..."
>
```

olmalıdır.

Video `object-fit:cover` ile viewportu doldurabilir.

## 13. Mobile video asset

Mümkünse ayrı mobile video kullanılmalıdır.

Örnek:

```text
hero-desktop.mp4
hero-mobile.mp4
hero-poster.webp
```

Mobile kullanıcı gereksiz büyük desktop assetini indirmemelidir.

## 14. Video crop

Araç, logo ve ana subject crop nedeniyle kaybolmamalıdır.

Scene bazında `object-position` override edilebilir.

Örnek:

```text
Scene 1: 50% 50%
Scene 2: 45% 50%
Scene 3: 50% 50%
Scene 4: 50% 45%
Scene 5: 50% 55%
```

Bu değerler gerçek asset testine göre değiştirilmelidir.

## 15. Hero overlay

Overlay:

- yazıyı okunabilir yapmalı
- video detaylarını öldürmemeli
- mobile'da gerektiğinde güçlenmeli
- desktop'ta daha hafif olabilir

## 16. Scene cards desktop

Desktop cardlar sol/sağ konumlandırılabilir.

Card video subjectinin üzerine gelmemelidir.

Yaklaşık max-width:

```text
440–520px
```

## 17. Scene cards mobile

Mobile'da card:

```text
left:16px
right:16px
bottom:safe-area-aware offset
```

yaklaşımıyla konumlandırılabilir.

Ana video subjectinin ortasına büyük bir panel bindirilmemelidir.

## 18. Mobile card

Öneri:

```text
width: calc(100% - 32px)
padding: 18–22px
radius: 18–24px
```

Title 2–3 satırı, description 3–5 satırı geçmemeye çalışmalıdır.

## 19. Mobile CTA

Touch target minimum:

```text
44×44px
```

Önerilen button height:

```text
48px
```

İki CTA sığmıyorsa alt alta alınmalıdır.

## 20. Typography

Başlangıç aralıkları:

```text
Hero H1: 30–42px mobile / 42–76px desktop
H2: 28–36px mobile / 36–56px desktop
H3: 20–26px
Body: 16–18px
Small: 14–15px
```

`clamp()` kullanılabilir.

## 21. Long text

Türkçe kelimeler gereksiz şekilde harf bazında parçalanmamalıdır.

Başlıkların container genişliği kontrollü tutulmalıdır.

## 22. Services grid

Mobile:

```text
1 column
```

Tablet:

```text
2 columns
```

Desktop:

```text
4 columns
```

Kart minimum okunabilir genişliği korunmalıdır.

## 23. Fleet

Mobile:

```text
Image
Details
CTA
```

şeklinde dikey.

Tablet split layout olabilir.

Desktop iki veya daha fazla kart/split layout kullanılabilir.

## 24. Images

```css
max-width:100%;
height:auto;
```

veya kontrollü aspect ratio kullanılmalıdır.

Araç fotoğraflarında önemli subject crop edilmemelidir.

## 25. About

Mobile:

```text
Heading
Text
Image
```

Desktop:

```text
Text | Image
```

veya tersidir.

## 26. Contact

Mobile iletişim seçenekleri kolay dokunulabilir şekilde dikey veya geniş butonlar halinde sunulmalıdır.

## 27. Footer

Desktop multi-column olabilir.

Mobile tek kolon tercih edilmelidir.

## 28. Landscape mobile

Örnek 667×375 cihazlarda:

- card maksimum yükseklik kontrolü
- navbar kontrolü
- video subject görünürlüğü
- heading küçültme

uygulanmalıdır.

Landscape'ta card yaklaşık `%45 viewport height` üzerinde olmamalı; içerik fazlaysa önce metin azaltılmalıdır.

## 29. Tablet

Tablet yalnızca büyütülmüş mobile olmamalıdır.

Daha geniş cardlar, 2-column gridler ve daha geniş typography kullanılabilir.

## 30. Desktop

Desktop'ta:

- geniş whitespace
- asymmetric composition
- side-aligned cards
- güçlü typography

kullanılabilir.

## 31. Large desktop

1440px+ ekranlarda içerik sonsuza kadar büyütülmemelidir.

Max-width container kullanılmalıdır.

## 32. ScrollTrigger responsive

Başlangıç:

```text
Desktop scrub: 0.15
Tablet scrub: 0.15
Mobile scrub: 0.20
```

Config üzerinden değiştirilebilir.

## 33. Resize / orientation

Viewport veya orientation değiştiğinde gerektiğinde ScrollTrigger refresh edilmelidir.

Refresh sürekli çalıştırılmamalıdır.

## 34. Mobile jitter

Scroll eventinde sürekli React `setState` kullanılmamalıdır.

Video scrub doğrudan ref/GSAP üzerinden yapılmalıdır.

## 35. Video metadata

`loadedmetadata` beklenmeden video duration kullanılmamalıdır.

## 36. Video failure

Video yüklenmezse:

```text
Poster
+
Static headline
+
Description
+
CTA
```

gösterilmelidir.

Boş/siyah hero kabul edilmez.

## 37. Slow connection

Poster ilk kullanılabilir görsel fallback olmalıdır.

Video hazır olduğunda storytelling devreye girebilir.

## 38. Data saver

Data-saving tercihleri desteklenebiliyorsa video yerine poster/static hero tercih edilebilir.

## 39. Reduced motion

`prefers-reduced-motion: reduce` aktifse:

- ScrollTrigger kapat
- video scrubbing kapat
- ağır transitionları kapat
- static hero göster

## 40. Glass performance

Mobile'da çok sayıda büyük `backdrop-filter` paneli kullanılmamalıdır.

## 41. Animation

Animation ağırlıklı olarak:

```text
opacity
transform
```

üzerinden yapılmalıdır.

Scroll sırasında width/height/top/left sürekli animate edilmemelidir.

## 42. Forms

Mobile input minimum 48px yükseklikte olabilir.

Input font-size en az 16px tutulmalıdır; iOS zoom davranışını azaltır.

## 43. Sticky CTA

Mobile bottom CTA gerekiyorsa safe-area desteklemeli ve sayfa içeriğini kapatmamalıdır.

## 44. Anchor scrolling

Sticky navbar içerik başlıklarını kapatmamalıdır.

`scroll-margin-top` kullanılabilir.

## 45. Responsive test matrix

Minimum:

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

## 46. Browser matrix

Test:

- iOS Safari
- Android Chrome
- Desktop Chrome
- Safari
- Edge
- Firefox

## 47. iOS checklist

- [ ] 100dvh
- [ ] playsInline
- [ ] muted
- [ ] video inline
- [ ] safe-area
- [ ] menu scroll lock
- [ ] scrub
- [ ] fallback
- [ ] landscape

## 48. Final responsive acceptance

- [ ] 320px çalışıyor
- [ ] 375px çalışıyor
- [ ] 390px çalışıyor
- [ ] 430px çalışıyor
- [ ] tablet çalışıyor
- [ ] desktop çalışıyor
- [ ] landscape çalışıyor
- [ ] horizontal overflow yok
- [ ] CTA'lar dokunulabilir
- [ ] video crop doğru
- [ ] cards taşmıyor
- [ ] reduced motion çalışıyor
- [ ] fallback çalışıyor
- [ ] production build başarılı

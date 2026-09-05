# EygülTurizm — Scrollytelling Specification

## 1. Amaç

20 saniyelik hero videosu scroll pozisyonuna bağlanacak. Kullanıcı aşağı kaydıkça video `currentTime` üzerinden kontrollü biçimde ilerleyecek.

## 2. Sahne zaman çizelgesi

| Scene | Video | İçerik |
|---|---:|---|
| 1 | 00:00–00:04 | Gün doğumu / hero |
| 2 | 00:04–00:08 | Okul servisi |
| 3 | 00:08–00:12 | Fabrika / personel |
| 4 | 00:12–00:16 | Otoyol / filo |
| 5 | 00:16–00:20 | Gece / CTA |

## 3. Temel mimari

```text
ScrollTrigger progress
        ↓
0..1 normalized progress
        ↓
video.duration
        ↓
video.currentTime
        ↓
Scene progress
        ↓
Glass card opacity / transform
```

Video süresi asla `20` saniye olarak hard-code edilmemelidir. Gerçek `video.duration` kullanılmalıdır.

## 4. Hero DOM

```text
.hero-scroll
└── .hero-sticky
    ├── video
    ├── overlay
    ├── scene-cards
    └── progress indicator
```

## 5. ScrollTrigger

Desktop için yaklaşık `400vh–500vh` scroll alanı kullanılabilir. Sticky içerik `100dvh` olmalıdır.

GSAP ScrollTrigger yalnızca video metadata hazır olduktan sonra oluşturulmalıdır.

Örnek mantık:

```js
ScrollTrigger.create({
  trigger: container,
  start: "top top",
  end: "bottom bottom",
  scrub: 0.15,
  onUpdate: self => {
    if (!video.duration) return;
    video.currentTime = self.progress * video.duration;
  }
});
```

Production implementasyonunda doğrudan her scroll eventinde React state güncellenmemelidir.

## 6. Scrub

Önerilen başlangıç:

- Desktop: `0.15`
- Tablet: `0.15`
- Mobile: `0.20`

Değerler merkezi config üzerinden değiştirilebilir olmalıdır.

## 7. Scene hesaplama

Bir scene:

```js
{
  id: "sunrise",
  start: 0,
  end: 4,
  title: "...",
  description: "...",
}
```

şeklinde tanımlanabilir.

Scene aktifliği:

```js
time >= scene.start && time < scene.end
```

mantığıyla belirlenebilir.

## 8. Scene transitions

Scene kartları aynı anda DOM'da bulunabilir. Aktif scene:

- opacity: 1
- translateY: 0
- pointer-events: auto

Inactive scene:

- opacity: 0
- translateY: 20px
- pointer-events: none

olmalıdır.

CSS/GSAP transitionları transform ve opacity ağırlıklı olmalıdır.

## 9. Video metadata

`loadedmetadata` event'i beklenmelidir.

Metadata hazır olmadan:

- ScrollTrigger oluşturulmamalı
- duration hesaplanmamalı
- currentTime seek edilmemeli

Video daha önce yüklenmişse `readyState` kontrolü yapılabilir.

## 10. Video seeking

Bazı tarayıcılarda çok sık `currentTime` değişimi pahalı olabilir.

GSAP ticker veya ScrollTrigger update kullanılırken gereksiz tekrarlar azaltılmalıdır.

Örneğin yeni zaman önceki zamandan anlamsız derecede farklı değilse seek atlanabilir.

Ancak video storytelling'in akıcılığı bozulacak kadar agresif throttling yapılmamalıdır.

## 11. Initialization lifecycle

```text
React mount
↓
refs available
↓
video source assigned
↓
metadata loaded
↓
GSAP context created
↓
ScrollTrigger created
↓
initial position applied
```

Unmount:

```text
ScrollTrigger.kill()
GSAP context revert()
listeners removed
```

olmalıdır.

## 12. Resize

Viewport değiştiğinde ScrollTrigger gerektiğinde `refresh()` edilmelidir.

Resize listener debounce edilebilir.

Sürekli `refresh()` çalıştırılmamalıdır.

Orientation change ayrıca dikkate alınmalıdır.

## 13. Mobile

Mobile'da aynı timeline korunabilir fakat scroll mesafesi ve scrub değeri responsive olabilir.

Portrait ve landscape farklı kart yerleşimine sahip olabilir.

## 14. Reduced motion

`prefers-reduced-motion: reduce` aktifse ScrollTrigger ve video scrubbing devre dışı bırakılmalıdır.

Static poster + HTML content gösterilmelidir.

## 15. Video fallback

Aşağıdaki durumlarda static fallback kullanılmalıdır:

- source bulunamadı
- codec desteklenmiyor
- metadata alınamadı
- video load error
- data-saving stratejisi devrede

Fallback:

```text
poster
+
headline
+
description
+
CTA
```

olmalıdır.

## 16. Autoplay

Scroll-controlled video için autoplay temel mekanizma değildir.

Video `muted` ve `playsInline` olmalıdır. Tarayıcı autoplay davranışına güvenilmemelidir.

## 17. Scene card accessibility

Video decorative ise `aria-hidden="true"` olabilir; ancak scene mesajları ayrıca normal HTML metni olarak erişilebilir kalmalıdır.

Animation yalnızca görsel enhancement'tır. İçerik animasyon olmadan da okunabilir olmalıdır.

## 18. Performance

- React state'i her frame değiştirilmemeli.
- Layout properties sürekli animate edilmemeli.
- `transform` ve `opacity` tercih edilmeli.
- GSAP context kullanılmalı.
- Event listener cleanup yapılmalı.
- Aynı ScrollTrigger birden fazla kez oluşturulmamalı.

## 19. Acceptance criteria

- [ ] Scroll video ile senkron.
- [ ] 5 scene doğru zamanlarda aktif.
- [ ] Video duration dinamik.
- [ ] Metadata bekleniyor.
- [ ] Resize güvenli.
- [ ] Orientation change güvenli.
- [ ] Mobile scrub çalışıyor.
- [ ] iOS Safari fallback mevcut.
- [ ] Reduced motion çalışıyor.
- [ ] Unmount cleanup çalışıyor.
- [ ] Duplicate ScrollTrigger oluşmuyor.

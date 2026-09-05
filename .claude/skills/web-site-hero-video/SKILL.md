---

name: web-site-hero-video
description: >
  Use when a landing or marketing page needs a hero video whose playback
  position is synchronized with page scroll instead of autoplaying.
  The visitor scrolls down and the video advances; scrolling up reverses
  the video. Triggers: "scroll'a bağlı video yap", "hero video sayfa
  kaydıkça ilerlesin", "scroll-linked hero video", "scrollytelling hero",
  "scroll scrub video".
---

# web-site-hero-video

## Genel Bakış

Klasik autoplay hero video yerine, HTML5 `<video>` elementinin
`currentTime` değerini sayfa scroll pozisyonuna bağlayan bir
**scroll-linked / scroll-scrub hero video** oluştur.

Kullanıcı aşağı doğru scroll yaptığında video ileri gider.
Kullanıcı yukarı scroll yaptığında video geri sarar.

Amaç:

* Sinematik bir landing page açılışı oluşturmak
* Video ile scroll pozisyonu arasında birebir görsel ilişki kurmak
* Smooth ve kontrollü bir scrollytelling deneyimi sağlamak
* Mobil cihazlarda performansı korumak
* `prefers-reduced-motion` kullanıcılarını desteklemek
* Video yüklenemediğinde veya desteklenmediğinde anlamlı bir fallback sunmak

---

# 1. Temel Teknik Kurallar

Hero video şu özelliklere sahip olmalıdır:

```html
<video
  muted
  playsinline
  preload="auto"
  aria-hidden="true"
>
```

Zorunlu:

* `muted`
* `playsinline`
* `preload="auto"`

Kullanma:

* autoplay
* controls
* kullanıcıdan video oynatma butonuna basmasını isteme
* scroll sırasında `play()` / `pause()` çağrılarını sürekli tetikleme

Scroll kontrollü sistemde esas kontrol:

```js
video.currentTime = targetTime;
```

üzerinden yapılmalıdır.

---

# 2. Video Konsepti

Hero video üretiminden önce tek bir güçlü görsel konsept belirle.

İdeal süreç:

1. Hero için konsept görsel oluştur.
2. Görseli image-to-video modeliyle hareketlendir.
3. 3–6 saniyelik kısa hero video üret.
4. Videoyu optimize et.
5. HTML5 video olarak projeye ekle.
6. Video zamanını scroll pozisyonuna bağla.

Video yalnızca dekoratif olmamalı.

Kamera hareketi, araç hareketi, ışık değişimi veya çevresel hareket
scroll ile kontrol edildiğinde anlamlı bir sinematik sonuç vermelidir.

---

# 3. Video Süresi

Varsayılan hedef:

**3–6 saniye.**

Daha uzun video yalnızca tasarım gerektiriyorsa kullanılmalıdır.

Scroll-scrub sistemlerinde kısa ve kontrollü videolar tercih edilir.

Örnek:

```text
0.0s → başlangıç kompozisyonu
1.5s → kamera / ana hareket
3.0s → ana mesaj
4.5s → final kompozisyon
5.0s → scene completion
```

Video süresi kod içerisinde hard-code edilmemelidir.

Yanlış:

```js
video.currentTime = progress * 5;
```

Doğru:

```js
video.currentTime = progress * video.duration;
```

---

# 4. Video Optimizasyonu

Hero video mümkün olduğunca küçük tutulmalıdır.

Hedef:

* H.264 / MP4
* mümkünse `< 5 MB`
* gereksiz yüksek bitrate kullanma
* gereksiz yüksek çözünürlük kullanma
* web için optimize edilmiş encoding kullan

Önerilen başlangıç:

```text
Desktop:
1920×1080 veya tasarıma göre 1920×1080 civarı

Mobile:
ayrı optimize edilmiş video mümkünse tercih edilir
```

Video dosyasını sırf 4K olduğu için 4K kullanma.

Scroll sırasında `currentTime` sürekli değiştiğinden,
ağır video dosyaları performansı ciddi şekilde etkileyebilir.

---

# 5. Video Metadata Hazır Olmadan ScrollScrub Başlatma

`video.duration` değeri metadata yüklenmeden güvenilir olmayabilir.

Bu nedenle ScrollTrigger kurulmadan önce video metadata'sının
hazır olmasını bekle.

Örnek:

```js
const initializeVideoScroll = () => {
  if (!video.duration || !Number.isFinite(video.duration)) return;

  // ScrollTrigger initialization
};

if (video.readyState >= 1) {
  initializeVideoScroll();
} else {
  video.addEventListener("loadedmetadata", initializeVideoScroll, {
    once: true,
  });
}
```

Amaç:

* `duration === Infinity` durumunu önlemek
* `duration === 0` durumunu önlemek
* yanlış progress hesaplamasını önlemek
* ScrollTrigger'ın yanlış başlangıç değerleriyle kurulmasını engellemek

---

# 6. Scroll Container

Hero bölümü sticky bir viewport sistemi kullanabilir.

Önerilen yapı:

```text
Hero Scroll Section
└── Sticky Viewport
    ├── Video
    ├── Overlay
    └── Content
```

Örnek:

```css
.hero {
  position: relative;
  height: 400vh;
}

.hero__sticky {
  position: sticky;
  top: 0;
  height: 100dvh;
  overflow: hidden;
}
```

Ancak `400vh` zorunlu değildir.

Scroll mesafesi tasarıma göre ayarlanmalıdır.

Genel başlangıç aralığı:

```text
300vh – 500vh
```

Kısa video + fazla scroll mesafesi:

```text
daha sinematik / yavaş scrub
```

Az scroll mesafesi:

```text
daha hızlı video ilerlemesi
```

---

# 7. GSAP + ScrollTrigger

GSAP kullanılıyorsa ScrollTrigger tercih edilir.

Temel yaklaşım:

```js
gsap.registerPlugin(ScrollTrigger);

const animation = gsap.to(video, {
  currentTime: video.duration,
  ease: "none",
  scrollTrigger: {
    trigger: hero,
    start: "top top",
    end: "bottom bottom",
    scrub: 0.15,
    pin: false,
  },
});
```

Ancak `video.duration` metadata yüklenmeden kullanılmamalıdır.

Daha güvenli yaklaşım:

```js
const setupScrollVideo = () => {
  const duration = video.duration;

  gsap.to(video, {
    currentTime: duration,
    ease: "none",
    scrollTrigger: {
      trigger: hero,
      start: "top top",
      end: "bottom bottom",
      scrub: 0.15,
    },
  });
};
```

---

# 8. Scrub Ayarı

Desktop başlangıç:

```js
scrub: 0.15
```

Mobil başlangıç:

```js
scrub: 0.1
```

Gerekirse:

```text
0.1 – 0.2
```

aralığında ayarla.

Amaç:

* scroll hareketini videoya yumuşak aktarmak
* frame jumping'i azaltmak
* hızlı scroll sırasında aşırı sert geçişleri önlemek

`ease` video scrub animasyonunda:

```js
ease: "none"
```

olmalıdır.

Çünkü scroll zaten progress'i kontrol etmektedir.

---

# 9. Scroll Progress Mantığı

Video zamanını doğrudan scroll progress üzerinden düşün.

```text
scroll progress = 0.00
→ video.currentTime = 0%

scroll progress = 0.25
→ video.currentTime = 25%

scroll progress = 0.50
→ video.currentTime = 50%

scroll progress = 0.75
→ video.currentTime = 75%

scroll progress = 1.00
→ video.currentTime = 100%
```

Temel matematik:

```js
const targetTime = progress * video.duration;
```

---

# 10. Scene / Scrollytelling Desteği

Hero birden fazla mesaj veya sahneden oluşuyorsa video timeline'ı
scene'lere bölünebilir.

Örnek:

```js
const scenes = [
  {
    start: 0,
    end: 0.2,
    title: "Güne Zamanında Başlıyoruz",
  },
  {
    start: 0.2,
    end: 0.4,
    title: "Geleceğimizi Güvenle Taşıyoruz",
  },
  {
    start: 0.4,
    end: 0.6,
    title: "İş Dünyasının Zamanına Değer Katıyoruz",
  },
  {
    start: 0.6,
    end: 0.8,
    title: "Yüksek Standartlı Filomuz",
  },
  {
    start: 0.8,
    end: 1,
    title: "Günün Her Anında Yanınızdayız",
  },
];
```

Scene metinleri video timeline'ına göre görünür / gizli yapılmalıdır.

Örneğin:

```text
0–20%   Scene 1
20–40%  Scene 2
40–60%  Scene 3
60–80%  Scene 4
80–100% Scene 5
```

---

# 11. Scene Transition

Scene değişimlerinde ani DOM değişimleri yapma.

Tercih edilen:

```text
fade in
fade out
opacity
translateY
scale
```

Örneğin:

```js
gsap.to(sceneElement, {
  opacity: 1,
  y: 0,
  duration: 0.4,
});
```

Geçişler scroll progress ile senkronize edilmelidir.

---

# 12. Responsive Kurallar

Mobile için desktop tasarımını küçültüp bırakma.

Aşağıdakileri ayrı değerlendir:

* video crop
* focal point
* typography
* text width
* CTA boyutu
* scene card konumu
* navbar
* spacing
* viewport height
* safe area
* video çözünürlüğü

Hero viewport yüksekliğinde:

```css
height: 100dvh;
```

tercih et.

Fallback:

```css
height: 100vh;
```

gerektiğinde kullanılabilir.

---

# 13. Mobile Video

Mümkünse mobile için ayrı optimize edilmiş video kullan.

Örneğin:

```html
<video>
  <source
    src="/videos/hero-mobile.mp4"
    media="(max-width: 768px)"
  />

  <source
    src="/videos/hero-desktop.mp4"
  />
</video>
```

Mobile video:

* daha düşük bitrate
* daha düşük çözünürlük
* daha küçük dosya
* mobil crop'a uygun framing

kullanmalıdır.

---

# 14. Mobile Scrub

Mobil cihazlarda scroll hareketi daha agresif olabilir.

Bu nedenle:

```js
scrub: 0.1
```

ile başlanabilir.

Mobilde video çok hızlı veya jittery görünüyorsa:

```js
scrub: 0.15
```

veya:

```js
scrub: 0.2
```

denenebilir.

Ancak kullanıcı scroll hareketinden belirgin şekilde kopuk
hissetmemelidir.

---

# 15. Reduced Motion

`prefers-reduced-motion: reduce` kesinlikle desteklenmelidir.

Kontrol:

```js
const prefersReducedMotion = window.matchMedia(
  "(prefers-reduced-motion: reduce)"
).matches;
```

Reduced motion aktifse:

**Scroll-scrub devre dışı bırakılmalıdır.**

Alternatif davranışlardan biri kullanılabilir:

### Seçenek A — Static poster

```text
Video yerine poster / static hero
```

### Seçenek B — Normal video

Video otomatik ve yavaş şekilde oynatılabilir.

Ancak kullanıcı hareket hassasiyetine göre
static poster en güvenli varsayılan seçenektir.

---

# 16. Video Fallback

Video yüklenemezse sayfa kullanılabilir kalmalıdır.

Kontrol edilmesi gereken durumlar:

```text
video error
network failure
unsupported format
metadata failure
mobile browser limitation
autoplay restriction
```

Fallback:

```text
video
↓
poster image
↓
hero background
↓
content remains usable
```

Video başarısız olduğunda:

* beyaz / boş alan bırakma
* kritik metni gizleme
* CTA'yı kaldırma
* sayfanın kullanılabilirliğini bozma

---

# 17. Poster Image

Video için poster mutlaka tanımlanmalıdır.

```html
<video
  poster="/images/hero-poster.webp"
  ...
>
```

Poster:

* video'nun ilk frame'iyle uyumlu
* yüksek kaliteli
* optimize edilmiş
* mobile crop'a uygun

olmalıdır.

---

# 18. Video Loading

Hero video sayfanın kritik asset'i olduğundan loading davranışı
dikkatli yönetilmelidir.

Öncelik:

```text
HTML
↓
critical CSS
↓
hero poster
↓
video metadata
↓
video frames
↓
secondary content
```

Video yüklenirken poster gösterilmelidir.

---

# 19. Cleanup

React kullanılıyorsa component unmount olduğunda:

* ScrollTrigger öldürülmeli
* event listener'lar kaldırılmalı
* GSAP context temizlenmeli

Örnek:

```js
return () => {
  ctx.revert();
};
```

veya uygun ScrollTrigger cleanup uygulanmalıdır.

Memory leak bırakma.

---

# 20. Resize / Orientation

Viewport değiştiğinde ScrollTrigger yeniden hesaplanmalıdır.

Özellikle:

* mobil orientation değişimi
* browser toolbar açılıp kapanması
* desktop resize
* responsive breakpoint değişimi

sonrasında:

```js
ScrollTrigger.refresh();
```

gerekiyorsa çağrılmalıdır.

Ancak resize sırasında gereksiz şekilde yüzlerce refresh
tetikleme.

Debounce / GSAP lifecycle mekanizmalarını kullan.

---

# 21. Browser Compatibility

En azından şu senaryolar test edilmelidir:

```text
Chrome desktop
Safari desktop
Firefox desktop
Chrome Android
Safari iOS
```

Özellikle Safari / iOS'ta:

* `playsinline`
* `muted`
* video metadata
* `currentTime`
* viewport height
* sticky positioning

kontrol edilmelidir.

---

# 22. Performance

Scroll sırasında her frame'de pahalı DOM işlemleri yapma.

Kaçınılması gereken:

```js
scroll event → layout calculation → DOM reflow → video update
```

Mümkün olduğunca GSAP / ScrollTrigger kullanılmalıdır.

Video dışında:

* büyük blur alanları
* ağır box-shadow
* çok sayıda backdrop-filter
* büyük PNG
* devasa background image
* gereksiz React re-render

kullanma.

Scroll sırasında özellikle React state'i sürekli değiştirme.

Yanlış:

```js
onUpdate: ({ progress }) => {
  setProgress(progress);
};
```

Bu yaklaşım gereksiz render üretebilir.

Video ve animasyon değerlerini mümkün olduğunca doğrudan
GSAP / DOM üzerinden yönet.

---

# 23. Glassmorphism Overlay

Hero üzerinde glassmorphism kullanılabilir.

Örnek:

```css
background: rgba(11, 37, 69, 0.65);
backdrop-filter: blur(16px);
-webkit-backdrop-filter: blur(16px);
border: 1px solid rgba(255, 255, 255, 0.12);
box-shadow: 0 20px 50px rgba(0, 0, 0, 0.5);
```

Ancak mobile GPU performansını göz önünde bulundur.

Çok büyük yüzeylerde sürekli `backdrop-filter` kullanma.

---

# 24. Accessibility

Hero video dekoratifse:

```html
aria-hidden="true"
```

kullanılabilir.

Ancak hero içindeki gerçek içerik erişilebilir olmalıdır.

Kontrol et:

* heading hiyerarşisi
* keyboard navigation
* focus state
* CTA erişilebilirliği
* yeterli contrast
* screen reader metni
* reduced motion
* mobile menu
* touch target boyutları

Video, kritik bilgi taşıyan tek kaynak olmamalıdır.

---

# 25. UX Kuralları

Hero video kullanıcıyı engellememelidir.

Şunları yapma:

* scroll'u kilitleme
* kullanıcıyı videoyu bitirmeye zorlama
* sürekli autoplay davranışı oluşturma
* uzun loading ekranı gösterme
* video yoksa hero'yu bozma

Kullanıcı her zaman normal şekilde scroll edebilmelidir.

---

# 26. Validation Checklist

Implementasyon tamamlandığında mutlaka test et.

### Desktop

* [ ] Sayfa açılıyor
* [ ] Hero poster görünüyor
* [ ] Video yükleniyor
* [ ] Aşağı scroll → video ileri gidiyor
* [ ] Yukarı scroll → video geri gidiyor
* [ ] Hızlı scroll → video kabul edilebilir şekilde takip ediyor
* [ ] Yavaş scroll → video akıcı ilerliyor
* [ ] Scene metinleri doğru zamanda değişiyor
* [ ] Hero sonunda CTA doğru görünüyor

### Mobile

* [ ] iOS Safari
* [ ] Android Chrome
* [ ] `100dvh` doğru çalışıyor
* [ ] Video crop doğru
* [ ] Text taşmıyor
* [ ] CTA ekrandan çıkmıyor
* [ ] Horizontal overflow yok
* [ ] Scrub jitter kabul edilebilir seviyede
* [ ] Navbar kullanılabilir

### Reduced Motion

* [ ] `prefers-reduced-motion: reduce` algılanıyor
* [ ] Scroll-scrub kapanıyor
* [ ] Kullanıcı hareketi zorlanmıyor
* [ ] Hero içeriği hâlâ kullanılabilir

### Failure

* [ ] Video yüklenemezse poster gösteriliyor
* [ ] Kritik metin kaybolmuyor
* [ ] CTA çalışıyor
* [ ] Sayfa scroll edilebilir kalıyor

---

# 27. Acceptance Criteria

İş tamamlanmış sayılması için:

1. Video autoplay ile başlamamalı.
2. Video scroll progress'e bağlı ilerlemeli.
3. Yukarı scroll edildiğinde video geri sarabilmeli.
4. Video `currentTime` üzerinden kontrol edilmeli.
5. `video.duration` dinamik okunmalı.
6. Metadata yüklenmeden ScrollTrigger kurulmamamalı.
7. GSAP ScrollTrigger kullanılmalı veya eşdeğer sağlam bir scroll
   progress sistemi kurulmalı.
8. `scrub` yaklaşık `0.1–0.2` aralığında optimize edilmeli.
9. Mobile responsive davranış ayrı ele alınmalı.
10. `prefers-reduced-motion` desteklenmeli.
11. Video hata durumunda poster/fallback çalışmalı.
12. React lifecycle cleanup yapılmalı.
13. Resize/orientation sonrası ScrollTrigger doğru hesaplanmalı.
14. Hero'da horizontal overflow oluşmamalı.
15. Video mümkün olduğunca optimize edilmiş olmalı.
16. Desktop ve mobile gerçek cihazlarda test edilmeli.
17. Yavaş ve hızlı scroll senaryolarında video takip hissini korumalı.

---

# 28. Implementation Priority

Implementasyonu şu sırayla yap:

```text
1. Hero HTML / React structure
2. Video + poster
3. Video metadata handling
4. ScrollTrigger
5. currentTime synchronization
6. Scene system
7. Scene text transitions
8. Responsive behavior
9. Mobile optimization
10. Reduced-motion fallback
11. Video error fallback
12. Performance optimization
13. Accessibility
14. Resize / orientation handling
15. Browser testing
```

Önce sistemi çalıştır.

Sonra görsel efekt ekle.

Görsel efektler temel scroll-video davranışının önüne geçmemelidir.

---

# 29. Claude İçin Uygulama Talimatı

Bu skill tetiklendiğinde:

1. Mevcut projeyi incele.
2. Framework ve animation stack'i tespit et.
3. Mevcut hero yapısını bozma; mümkünse mevcut mimariye entegre ol.
4. Video asset'lerinin nerede olduğunu kontrol et.
5. Video yoksa uygun poster/fallback yapısını oluştur.
6. `loadedmetadata` durumunu ele al.
7. Scroll progress'i video `currentTime` değerine bağla.
8. GSAP kullanılıyorsa ScrollTrigger tercih et.
9. React lifecycle cleanup yap.
10. Responsive davranışı uygula.
11. Mobile davranışı ayrıca test et.
12. `prefers-reduced-motion` fallback'i uygula.
13. Video hata durumunu ele al.
14. Gereksiz React state update'lerinden kaçın.
15. Scroll sırasında performansı koru.
16. Son olarak yavaş/hızlı scroll, mobile ve reduced-motion
    senaryolarını kontrol et.

Var olan tasarım sistemine, component yapısına ve naming convention'a
uyum sağla.

Gereksiz dependency ekleme.

Gereksiz refactor yapma.

Çalışan özellikleri bozma.

---

# 30. Definition of Done

Hero aşağıdaki deneyimi vermelidir:

```text
Kullanıcı sayfayı açar
        ↓
Poster / ilk video frame'i görünür
        ↓
Kullanıcı aşağı scroll eder
        ↓
Video sinematik şekilde ilerler
        ↓
Scene içerikleri timeline'a göre değişir
        ↓
Kullanıcı yukarı scroll eder
        ↓
Video geri sarar
        ↓
Hero tamamlanır
        ↓
Normal sayfa içeriğine geçilir
```

Deneyim:

**smooth + responsive + performant + accessible + resilient**

olmalıdır.

Ana hedef:

> Video scroll'un peşinden gitmemeli; video scroll ile aynı hareketin
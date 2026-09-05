# EygülTurizm — Deployment Specification

## 1. Build

Production build:

```bash
npm run build
```

başarılı olmalıdır.

## 2. Preview

```bash
npm run preview
```

ile production build lokal olarak test edilmelidir.

## 3. Hosting

Static hosting desteklenmelidir.

Uygun seçenekler:

- Vercel
- Netlify
- Cloudflare Pages
- GitHub Pages
- Static web server

## 4. Environment variables

Gizli anahtarlar frontend içine hard-code edilmemelidir.

Bu proje backend gerektirmediği için public business bilgileri environment variable yerine config dosyasında da tutulabilir.

Secret gerekiyorsa frontend'e koyulmamalıdır.

## 5. Assets

Video ve büyük görseller deploy boyutu açısından kontrol edilmelidir.

## 6. SPA routing

Tek sayfa anchor yapısı kullanılıyorsa özel routing gerekmeyebilir.

React Router eklenmesi yalnızca ihtiyaç halinde yapılmalıdır.

## 7. HTTPS

Production HTTPS üzerinden servis edilmelidir.

## 8. Cache

Static assets uygun cache header'ları ile servis edilmelidir.

## 9. Pre-deploy checklist

- [ ] npm run build
- [ ] npm run preview
- [ ] Console temiz
- [ ] Mobile test
- [ ] Tablet test
- [ ] Desktop test
- [ ] Video assetleri mevcut
- [ ] Poster mevcut
- [ ] CTA linkleri doğru
- [ ] SEO metadata doğru
- [ ] Favicon mevcut
- [ ] 404 davranışı uygun

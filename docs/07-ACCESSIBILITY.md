# EygülTurizm — Accessibility Specification

## 1. Goal

Site tüm kullanıcıların temel içeriğe erişebilmesini sağlamalıdır.

## 2. Semantic HTML

Öncelik:

```text
header
nav
main
section
article
footer
button
a
h1–h6
```

olmalıdır.

Div her şey için kullanılmamalıdır.

## 3. Heading hierarchy

Sayfada bir ana H1 bulunmalıdır.

Heading seviyeleri görsel boyut için atlanmamalıdır.

## 4. Keyboard

Desktop kullanıcı:

- Tab
- Shift+Tab
- Enter
- Space
- Escape

ile navigasyon yapabilmelidir.

## 5. Focus

Interactive elementlerde görünür focus state bulunmalıdır.

Focus sadece mouse hover ile gösterilmemelidir.

## 6. Touch

Minimum target:

```text
44×44px
```

## 7. Contrast

Metin video üzerinde okunamıyorsa overlay/gradient kullanılmalıdır.

## 8. Video

Video dekoratifse:

```html
aria-hidden="true"
```

kullanılabilir.

Ancak video içindeki anlamlı mesajlar HTML metni olarak ayrıca bulunmalıdır.

## 9. Reduced motion

`prefers-reduced-motion: reduce`:

- ScrollTrigger kapalı
- video scrubbing kapalı
- ağır animation kapalı
- static content açık

olmalıdır.

## 10. Mobile menu

Menu:

- button ile açılmalı
- accessible label içermeli
- Escape ile kapanabilmeli
- focus yönetimi yapılmalı
- açıkken background scroll kilitlenebilmeli

## 11. Links

Telefon:

```text
tel:
```

WhatsApp:

```text
https://wa.me/
```

E-mail:

```text
mailto:
```

şeklinde çalışmalıdır.

Gerçek değerler kullanıcıdan alınmalıdır.

## 12. Images

Dekoratif:

```text
alt=""
```

Anlamlı:

```text
alt="..."
```

kullanmalıdır.

## 13. Forms

Her input label'a sahip olmalıdır.

Error mesajları anlaşılır olmalıdır.

Placeholder label yerine kullanılmamalıdır.

## 14. Accessibility acceptance

- [ ] Keyboard navigation.
- [ ] Visible focus.
- [ ] Screen reader sensible structure.
- [ ] Reduced motion.
- [ ] Touch targets.
- [ ] Contrast.
- [ ] Accessible menu.
- [ ] Accessible CTA.

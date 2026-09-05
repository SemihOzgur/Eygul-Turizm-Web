# EygülTurizm — Content Model

## 1. Amaç

Business content componentlerden ayrılacaktır. İçerik değişiklikleri JSX'e dokunmadan yapılabilmelidir.

## 2. Company

```js
const company = {
  name: "",
  shortName: "",
  tagline: "",
  phone: "",
  whatsapp: "",
  email: "",
  address: "",
  workingHours: "",
  website: "",
  social: {
    instagram: "",
    linkedin: "",
    facebook: ""
  }
};
```

Boş alanlar gerçek bilgi yoksa doldurulmamalıdır.

## 3. Navigation

```js
const navigation = [
  { label: "Hakkımızda", href: "#about" },
  { label: "Hizmetler", href: "#services" },
  { label: "Filo", href: "#fleet" },
  { label: "İletişim", href: "#contact" }
];
```

## 4. Services

Her hizmet:

```js
{
  id: "",
  title: "",
  shortDescription: "",
  description: "",
  icon: "",
  image: "",
  features: []
}
```

alanlarını destekleyebilir.

## 5. Fleet

```js
{
  id: "",
  name: "",
  image: "",
  description: "",
  capacity: "",
  comfortFeatures: [],
  safetyFeatures: [],
  useCases: []
}
```

Teknik bilgi kullanıcı tarafından doğrulanmadan yazılmamalıdır.

## 6. Hero scenes

```js
{
  id: "",
  start: 0,
  end: 4,
  title: "",
  description: "",
  eyebrow: "",
  cta: null,
  desktopAlign: "left",
  mobileAlign: "bottom"
}
```

## 7. CTA

```js
{
  label: "",
  type: "phone | whatsapp | email | anchor",
  value: ""
}
```

## 8. Trust signals

Başarı oranı, sertifika, araç yaşı, GPS sistemi gibi iddialar yalnızca doğrulanmış bilgi varsa kullanılmalıdır.

Örneğin `%99.8 zamanında varış` gerçek şirket verisi değilse kullanılmamalıdır.

## 9. Legal content

Aşağıdakiler ayrı content alanlarında tutulmalıdır:

- KVKK metni
- Gizlilik politikası
- Çerez politikası
- Kullanım şartları

Gerçek hukuki metinler kullanıcı/uzman tarafından sağlanmalıdır.

## 10. Content rules

- Lorem ipsum kullanılmamalı.
- Uydurma müşteri logoları kullanılmamalı.
- Uydurma sertifika kullanılmamalı.
- Uydurma başarı oranı kullanılmamalı.
- Uydurma telefon/adres kullanılmamalı.
- Teknik araç bilgileri doğrulanmadan yazılmamalı.

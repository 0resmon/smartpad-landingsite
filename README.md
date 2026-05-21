# GitHub Pages çıktısı (`out`)

Bu repo, Next static export (`out`) içeriğinin kopyasıdır. **Sayfadaki tüm yollar, build alınırken seçilen GitHub repo adına (`basePath`) kilitlenir.**

## Şu anki HTML ne diyor?

`index.html` içinde linkler şöyle:

- `/smartpad-landingsite/_next/...`
- `/smartpad-landingsite/logo.png`
- vb.

Bu dosyaların yüklenmesi için GitHub Pages adresin **tam olarak** şu olmalı:

`https://<kullanıcı>.github.io/smartpad-landingsite/`

Yani GitHub’daki repo adı **`smartpad-landingsite`** olmalı (sonunda ekstra `s` yok).

## Klasör adı `smartpad-landingsits` ama site `.../landingsits/` ise

Repo adı `smartpad-landingsits` ise URL `.../smartpad-landingsits/` olur; o zaman mevcut `index.html` **yanlış** build’tir — tarayıcı `/smartpad-landingsite/...` dosyalarını arar, sunucuda ise dosyalar `.../smartpad-landingsits/...` altındadır → **CSS yok / 404**.

**Çözüm (birini seç):**

1. GitHub’da repo adını `smartpad-landingsite` yap (veya bu `out`’u o isimli repoya yükle), **veya**
2. Kaynak projede (`smartpad-landing`) build’i **gerçek repo adına** göre al:

   ```bash
   cross-env GITHUB_PAGES=true GITHUB_REPOSITORY_NAME=smartpad-landingsits npm run build
   ```

   Sonra oluşan `out/` içeriğinin tamamını bu repoya tekrar kopyala / push et.

## `.nojekyll`

Kökte `.nojekyll` olmalı (Jekyll’in `_next` klasörünü yok saymasını engeller). `out` postbuild ile üretiliyorsa otomatik gelir.

## Gereksiz dosyalar

Kökte `__next.*.txt`, `index.txt` gibi dosyalar genelde yanlışlıkla kopyalanmış export artığıdır; silinmesi Pages’i bozmaz, repo daha temiz olur.

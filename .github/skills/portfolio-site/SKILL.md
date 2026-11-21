---
name: portfolio-site
description: Gamze İbrahimağaoğlu'nun Türkçe statik portfolyo sitesini (index.html, colors.css) düzenleme kuralları. İçerik, bölüm, proje kartı, renk, stil, form veya yayınlama değişikliklerinde kullan.
---

# Portfolyo sitesi

Build adımı olmayan, tek sayfalık statik bir site. Netlify `main` dalını kök dizinden yayınlar; build komutu yoktur.

## Dosyalar

- `index.html`: Tüm HTML, CSS (`<style>`) ve JavaScript (`<script>`) bu dosyadadır. Ayrı CSS/JS dosyası, framework veya paket ekleme.
- `colors.css`: Renk paleti. Bütün renkler buradaki CSS değişkenlerinden gelir.
- `profile.jpeg`: Hero bölümündeki profil fotoğrafı; 700×700 kare kesit, CSS ile yuvarlak (`border-radius: 50%`) ve en fazla 320px gösterilir. Retina netliği için en az 640px kare olmalı; büyütülerek üretme.
- `shared-image.jpeg`: Orijinal fotoğraf (1500×2000). Yeni kesit gerekirse buradan `sips -c <boy> <en> --cropOffset <y> <x>` ile kırp.
- `README.md`: Proje açıklaması. Dosya yapısı veya kurulum değişirse güncelle.

## Dil ve içerik

- Sitedeki tüm metinler Türkçe (`lang="tr"`). Hitap samimi "sen" diliyle, birinci tekil şahıstan yazılır.
- `.eyebrow` gibi `text-transform: uppercase` kullanan öğelerdeki İngilizce metinlere `lang="en"` ekle; yoksa Türkçe kuralla "i" harfi "İ" olur (ör. "BUSİNESS").
- Hata ve durum mesajları da Türkçe olmalı.
- Kişisel bilgileri (deneyim, eğitim, iletişim) kullanıcı istemedikçe değiştirme ve uydurma.

## Stil kuralları

- Renk kodu yazma; `var(--c-950)`, `var(--c-400)`, `var(--text-muted)`, `var(--danger)` gibi değişkenleri kullan. Yeni renk gerekirse önce `colors.css` dosyasına ekle.
- İstisnalar `<meta name="theme-color">` ve `<link rel="icon">` içindeki SVG favicon'dur; palet değişirse bunları `--c-950` / `--c-400` ile eşitle.
- Boşluk için `--sp-1`…`--sp-9`, yazı boyutu için `--fs-*`, köşe için `--radius`, süre için `--dur-fast` / `--dur-mid` kullan.
- Başlıklar `--font-display`, gövde metni `--font-body` kullanır.
- Kırılım noktaları: `1023px` (tablet) ve `767px` (mobil). Yeni ızgaraları bu iki sorguda da tek/iki sütuna düşür.
- Animasyonlarda yalnızca `transform` ve `opacity` kullan; `prefers-reduced-motion` bloğu korunmalı.

## Erişilebilirlik

- Tıklanabilir öğeler en az 44px yüksekliğinde olmalı.
- Düğmelerde `type="button"`, ikon düğmelerde `aria-label`, dekoratif SVG'lerde `aria-hidden="true"` kullan.
- Görsellerde anlamlı `alt` ile `width`/`height` bulunmalı.
- Odak stili (`:focus-visible`) ve "İçeriğe geç" bağlantısı kaldırılmamalı.

## Yapı ve davranış

- Her bölüm `<section id="...">` içinde `.wrap` kullanır; başlık `.sec-head` içinde `.eyebrow` + `h2` ile yazılır. Bölüm numaraları (01, 02…) CSS sayacıyla otomatik gelir, elle yazma.
- Yeni bölüm eklerken `nav.main` içine aynı `href="#id"` bağlantısını ekle; aktif menü vurgusu bu eşleşmeye bağlıdır.
- Görünürken beliren öğelere `reveal` sınıfı ver.
- Proje/çalışma alanı kartları HTML'de değil, script içindeki `PROJECTS` dizisinde tutulur. Her öğe `title`, `cat`, `label`, `desc`, `tags` (Yetenekler bölümündeki araç/yetkinliklerden) ve `topic` alanlarına sahiptir. `cat` değeri bir `.filter` düğmesinin `data-filter` değeriyle ve `CAT_ICONS` anahtarıyla eşleşmeli; yeni kategori eklenirse filtre düğmesini ve ikonunu da ekle. Filtre sayaçları otomatik hesaplanır.
- "Birlikte çalışalım" kartlarındaki ve `PROJECTS` öğelerindeki `data-topic` / `topic` değerleri, iletişim formundaki `#topic` seçeneklerinin metniyle birebir aynı olmalı. Tıklamalar `document` üzerinde yetkilendirmeyle dinlenir; dinamik öğelere ayrıca olay bağlama.
- Pano (`#dashboard`) verileri script'teki `CAREER` dizisinden (`role`, `org`, `start`/`end` `YYYY-MM`, `end: null` = günümüz, `track: 'fin' | 'bi'`) ve `PROJECTS` dizisinden hesaplanır. Deneyim bölümü değişirse `CAREER` dizisini de güncelle. KPI'lardaki HTML değerleri yalnızca JS kapalıyken görünen yedek değerlerdir. Uydurma metrik ekleme; yeni rakamları kullanıcıdan al.
- DOM'a içerik eklerken `innerHTML` yerine `textContent` / `createElement` kullan.

## İletişim formu

Form Netlify Forms ile gönderilir (`name="contact"`, `data-netlify="true"`, `bot-field` honeypot). Script `fetch('/')` ile urlencoded POST yapar; `form-name` gizli alanı kaldırılmamalı. Yeni alanlar statik HTML'de `name` ile tanımlanmalı, yoksa Netlify kaydetmez. Doğrulama kuralları `rules` nesnesinde; hata metinleri `#<alan>Err` öğelerine yazılır. Gönderim hatasında `#formStatus` öğesine `is-error` sınıfı eklenir. Yerel sunucuda POST desteklenmediği için hata mesajı görmek normaldir.

## Doğrulama

Değişiklikten sonra yerel sunucuyla kontrol et:

```bash
python3 -m http.server 8000
```

`http://localhost:8000` adresinde masaüstü ve 375px mobil genişlikte; menü, proje filtreleri, form hataları ve tarayıcı konsolunda hata olmadığını kontrol et.

## Git ve yayın

- Uzak depo: `https://github.com/memisoglugamze/Kis-isel-Portfolyo-Sitesi.git`, dal `main`.
- Varsayılan git kimliği iş hesabıdır ve bu depoya yazamaz. Push için kişisel `memisoglugamze` hesabı gerekir; global git ayarlarını veya VS Code oturumunu değiştirme.
- `main` dalına yapılan her push Netlify'da otomatik yayına çıkar.

---
name: portfolio-site
description: Gamze İbrahimağaoğlu'nun Türkçe/İngilizce, açık/koyu temalı statik portfolyo sitesini (index.html, colors.css) düzenleme kuralları. İçerik, çeviri, bölüm, proje kartı, renk, tema, stil, form veya yayınlama değişikliklerinde kullan.
---

# Portfolyo sitesi

Build adımı olmayan, tek sayfalık statik bir site. İki yerde yayınlanır: Netlify `main` dalını kök dizinden otomatik yayınlar (https://gamzeagaoglu.netlify.app); Firebase Hosting'e elle `firebase deploy` ile yayınlanır (https://gamzeagaoglu.web.app). Build komutu yoktur.

## Dosyalar

- `index.html`: Tüm HTML, CSS (`<style>`) ve JavaScript (`<script>`) bu dosyadadır. Ayrı CSS/JS dosyası, framework veya paket ekleme.
- `colors.css`: Renk paleti. Bütün renkler buradaki CSS değişkenlerinden gelir.
- `profile.jpeg`: Hero bölümündeki profil fotoğrafı; 680×680 kare kesit, CSS ile yuvarlak (`border-radius: 50%`) ve en fazla 320px gösterilir. Retina netliği için en az 640px kare olmalı; büyütülerek üretme.
- Yeni profil fotoğrafı gelirse baş ve omuzları ortalayan kare bir kesiti `sips -c <boy> <en> --cropOffset <y> <x>` ile kırp ve `profile.jpeg` olarak kaydet. Gelen görselin uzantısına güvenme; `file` ile gerçek formatı kontrol et ve JPEG'e çevir. Orijinal dosyalar depoda tutulmaz.
- `README.md`: Proje açıklaması. Dosya yapısı veya kurulum değişirse güncelle.

## Dil ve içerik

- Varsayılan dil Türkçe (`lang="tr"`); hitap samimi "sen" diliyle, birinci tekil şahıstan yazılır. Site ayrıca İngilizce gösterilebilir (başlıktaki TR/EN düğmesi, seçim `localStorage.lang`).
- Çeviri yapısı: Türkçe metin HTML'de kalır; öğeye `data-i18n="anahtar"` (öznitelik için `data-i18n-attr="aria-label:anahtar"`) verilir ve İngilizcesi script'teki `STR.en` içine yazılır. Öğe yalnızca metin içermeli; karışık içerikte metni ayrı bir `<span data-i18n>` ile sar. JS'in ürettiği metinler `t('anahtar')` ile alınır ve hem `STR.tr` hem `STR.en` içinde bulunur. Yeni metin eklerken İngilizcesini de ekle.
- `PROJECTS` öğelerinde metinler `tr` / `en` alt nesnelerindedir (`title`, `desc`, `tags`); kategori etiketi `cat.<cat>` anahtarından gelir. Dil değişince `renderProjects()` ve `renderDashboard()` yeniden çizilir.
- İngilizce metinlerde Türkçe karakter kullanma (ör. "Istanbul"); özel isimler (kişi ve şirket adları) olduğu gibi kalır.
- `.eyebrow` gibi `text-transform: uppercase` kullanan öğelerdeki İngilizce metinlere `lang="en"` ekle; yoksa Türkçe kuralla "i" harfi "İ" olur (ör. "BUSİNESS").
- Hata ve durum mesajları her iki dilde de olmalı; `.err::before` ön eki `:lang(en)` ile "Error: " olur.
- Kişisel bilgileri (deneyim, eğitim, iletişim) kullanıcı istemedikçe değiştirme ve uydurma.

## Stil kuralları

- Renk kodu yazma; `var(--c-950)`, `var(--c-400)`, `var(--text-muted)`, `var(--danger)` gibi değişkenleri kullan. Yeni renk gerekirse önce `colors.css` dosyasına, hem koyu (`:root`) hem açık (`:root[data-theme="light"]`) temaya ekle.
- Tema: `data-theme="light" | "dark"` `<html>` üzerindedir; `<head>` içindeki küçük script kayıtlı seçimi (`localStorage.theme`) veya cihaz tercihini boyamadan önce uygular. Açık temada ölçek ters çevrilir (`--c-950` zemin, `--c-100` metin). Pano grafikleri `--chart-fin` / `--chart-bi` kullanır.
- İstisnalar `<meta name="theme-color">` ve `<link rel="icon">` içindeki SVG favicon'dur. `theme-color` tema değişince script tarafından `--c-950` değerine eşitlenir; palet değişirse HTML'deki ilk değeri ve favicon'u koyu temadaki `--c-950` / `--c-400` ile eşitle.
- Boşluk için `--sp-1`…`--sp-9`, yazı boyutu için `--fs-*`, köşe için `--radius`, süre için `--dur-fast` / `--dur-mid` kullan.
- Başlıklar `--font-display`, gövde metni `--font-body` kullanır.
- Kırılım noktaları: `1023px` (tablet) ve `767px` (mobil). Yeni ızgaraları bu iki sorguda da tek/iki sütuna düşür. Üst menü `1199px` altında hamburger menüye döner (JS'teki `mq` ile aynı); menüye öğe eklersen 1200px'te iki dilde de tek satıra sığdığını kontrol et (şu an sınırda: 1200px'te Türkçe menüde yaklaşık 20px, İngilizcede 35px boşluk var).
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
- Proje/çalışma alanı kartları HTML'de değil, script içindeki `PROJECTS` dizisinde tutulur. Her öğe `cat`, `topic` ve `tr` / `en` alt nesnelerinde `title`, `desc`, `tags` (Yetenekler bölümündeki araç/yetkinliklerden) alanlarına sahiptir. `cat` değeri bir `.filter` düğmesinin `data-filter` değeriyle, `CAT_ICONS` anahtarıyla ve `cat.<cat>` çeviri anahtarıyla eşleşmeli; yeni kategori eklenirse filtre düğmesini, ikonunu ve çevirisini de ekle. Filtre sayaçları otomatik hesaplanır.
- "Birlikte çalışalım" kartlarındaki ve `PROJECTS` öğelerindeki `data-topic` / `topic` değerleri, iletişim formundaki `#topic` seçeneklerinin `value` değeriyle birebir aynı olmalı (değerler Türkçe sabit anahtardır; görünen metin dile göre çevrilir). Tıklamalar `document` üzerinde yetkilendirmeyle dinlenir; dinamik öğelere ayrıca olay bağlama.
- Pano (`#dashboard`) verileri script'teki `CAREER` dizisinden (`role`, `org`, `start`/`end` `YYYY-MM`, `end: null` = günümüz, `track: 'fin' | 'bi'`) ve `PROJECTS` dizisinden hesaplanır. Deneyim bölümü değişirse `CAREER` dizisini de güncelle. KPI'lardaki HTML değerleri yalnızca JS kapalıyken görünen yedek değerlerdir. Uydurma metrik ekleme; yeni rakamları kullanıcıdan al.
- Graphify (`#graph`) bilgi grafiği kütüphanesiz SVG'dir. Düğümler `GX_NODES` (`id`, `g` grup, `label`/`detail` metin ya da `{tr, en}`, mobil için isteğe bağlı `short`, alanlarda `proj` = `PROJECTS` sırası, `url` dış site, `sec` sayfa bölümü), bağlantılar `GX_EDGES`, konumlar `GX_POLAR` (`[açı, halka]`; mobilde 90° döner) içindedir. Grup renkleri `colors.css` içindeki `--g-*` değişkenleridir. Yeni düğüm eklerken üçünü de güncelle, yalnızca sitede olan bilgiyi kullan, dış adresin açıldığını kontrol et ve masaüstü ile 375px'te etiketlerin taşmadığını/çakışmadığını doğrula. Yeni proje, araç veya yetkinlik eklenirse grafiğe de ekle.
- DOM'a içerik eklerken `innerHTML` yerine `textContent` / `createElement` kullan.

## İletişim formu

Netlify'da (`location.hostname` `.netlify.app` ile bitiyorsa) form Netlify Forms ile gönderilir (`name="contact"`, `data-netlify="true"`, `bot-field` honeypot). Script `fetch('/')` ile urlencoded POST yapar; `form-name` gizli alanı kaldırılmamalı. Yeni alanlar statik HTML'de `name` ile tanımlanmalı, yoksa Netlify kaydetmez. Diğer tüm adreslerde (Firebase, yerel sunucu) Netlify Forms yoktur; "Gönder" doldurulmuş bir `mailto:` bağlantısı açar ve `mailOpened` mesajını gösterir. Netlify'a özel alan adı bağlanırsa bu hostname kontrolünü de güncelle. Doğrulama kuralları `rules` nesnesinde; hata metinleri `#<alan>Err` öğelerine yazılır. Gönderim hatasında `#formStatus` öğesine `is-error` sınıfı eklenir.

## Doğrulama

Değişiklikten sonra yerel sunucuyla kontrol et:

```bash
python3 -m http.server 8000
```

`http://localhost:8000` adresinde masaüstü ve 375px mobil genişlikte; menü, proje filtreleri, form hataları ve tarayıcı konsolunda hata olmadığını kontrol et. Metin veya renk değiştiyse her iki dilde ve her iki temada da kontrol et. Yerel sunucuda tarayıcı `colors.css` dosyasını önbellekten verebilir; değişiklik görünmüyorsa sayfayı önbelleksiz yenile.

## Git ve yayın

- Uzak depo: `https://github.com/memisoglugamze/Kis-isel-Portfolyo-Sitesi.git`, dal `main`.
- Varsayılan git kimliği iş hesabıdır ve bu depoya yazamaz. Push için kişisel `memisoglugamze` hesabı gerekir; global git ayarlarını veya VS Code oturumunu değiştirme.
- `main` dalına yapılan her push Netlify'da otomatik yayına çıkar.
- Firebase Hosting otomatik değildir: proje `kisiselportfolyositesi`, site `gamzeagaoglu` (`.firebaserc`, `firebase.json`). Değişiklikten sonra kişisel `memisoglugamze@gmail.com` hesabıyla `firebase login` yapılmış CLI ile `firebase deploy --only hosting` çalıştır; kullanıcı istemedikçe yalnızca Netlify'a push yetmez, iki siteyi de güncel tut. Bu makinede global Node/Firebase CLI yoktur ve Apple Silicon'da Firebase'in tek dosyalık CLI'ı çalışmaz; geçici bir klasöre taşınabilir Node indirip `firebase-tools`'u oraya kur, sisteme kurulum yapma.
- `firebase.json` içindeki `ignore` listesindeki `**/.*/**` kuralı `.git` ve `.github` klasörlerinin yayınlanmasını engeller; kaldırma. Yayından sonra `https://gamzeagaoglu.web.app/.git/HEAD` adresinin 404 verdiğini kontrol et. Yayın sırasında oluşan `firebase-debug.log` dosyasını sil (`.gitignore`'da).

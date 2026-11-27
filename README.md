# Kişisel Portfolyo Sitesi

Gamze İbrahimağaoğlu için hazırlanmış, Türkçe ve duyarlı kişisel portfolyo sitesi. Business Intelligence ve veri ambarı deneyimini, yetkinliklerini ve çalışma alanlarını tanıtır.

## Projeyi görüntüleme

Proje derleme veya paket kurulumu gerektirmez. `index.html` dosyasını bir tarayıcıda açabilir ya da proje klasöründe yerel bir HTTP sunucusu başlatabilirsiniz.

Örneğin Python kuruluysa:

```bash
python3 -m http.server 8000
```

Ardından tarayıcıda [http://localhost:8000](http://localhost:8000) adresini açın.

## İçerik ve özellikler

- Kariyer panosu: KPI kartları, kariyer zaman çizelgesi, deneyim dağılımı ve projeleri filtreleyen çalışma alanı grafiği
- Graphify bilgi grafiği: araçlar, yetkinlikler, çalışma alanları, kurumlar, eğitim ve profiller arasındaki bağlantıları gösteren etkileşimli ağ; noktalar ilgili dış siteye ve sayfa bölümüne bağlanır
- Türkçe/İngilizce dil seçeneği ve açık/koyu tema (seçimler tarayıcıda hatırlanır; tema ilk açılışta cihaz tercihine uyar)
- Hakkımda, yetenekler, deneyim ve eğitim bölümleri
- Kategori filtreleriyle çalışma alanları
- Mobil gezinme menüsü ve duyarlı sayfa düzeni
- Erişilebilirlik iyileştirmeleri: klavye odağı, atlama bağlantısı, ARIA durumları ve azaltılmış hareket tercihi
- İletişim formu için temel doğrulama ve iş birliği konusunu forma aktarma
- Bağlantı paylaşım önizlemesi için Open Graph etiketleri ve favicon

**İletişim formu:** Netlify'da (`*.netlify.app`) Netlify Forms ile gönderilir; gelen mesajlar Netlify panelinde **Forms → contact** altında görünür. Diğer adreslerde (Firebase, yerel sunucu) "Gönder" butonu ziyaretçinin e-posta uygulamasını doldurulmuş mesajla açar.

## Yayın

Site iki yerde yayındadır:

- **Netlify:** https://gamzeagaoglu.netlify.app — `main` dalına yapılan her push otomatik yayınlanır.
- **Firebase Hosting:** https://gamzeagaoglu.web.app — Firebase projesi `kisiselportfolyositesi`, site `gamzeagaoglu`. Otomatik değildir; değişiklikten sonra elle yayınlanır:

```bash
firebase login          # memisoglugamze@gmail.com
firebase deploy --only hosting
```

Ayarlar `firebase.json` ve `.firebaserc` dosyalarındadır. Yalnızca site dosyaları yayınlanır; gizli dosya ve klasörler (`.git`, `.github`) ile README ve ayar dosyaları hariç tutulur.

## Dosyalar

- `index.html` — Sayfa içeriği, stiller ve etkileşimler
- `colors.css` — Ortak renk paleti
- `profile.jpeg` — Hero bölümündeki yuvarlak profil fotoğrafı (680×680)
- `firebase.json`, `.firebaserc` — Firebase Hosting ayarları

## Özelleştirme

- Metinleri ve proje/çalışma alanı kartlarını `index.html` içinde güncelleyin. Türkçe metin HTML'de durur; İngilizcesi script'teki `STR.en` sözlüğünde, kartlarınki `PROJECTS` içindeki `en` alanındadır. Bir metni değiştirirseniz İngilizcesini de güncelleyin.
- Yeni bir iş deneyimi eklerseniz hem "Deneyim" bölümünü hem de script'teki `CAREER` dizisini güncelleyin; pano süreleri bu diziden hesaplanır.
- Renkleri `colors.css` dosyasındaki CSS değişkenlerinden düzenleyin; koyu tema `:root`, açık tema `:root[data-theme="light"]` bloğundadır.
- Profil görselini değiştirecekseniz en az 640×640 piksel kare bir görseli `profile.jpeg` adıyla kaydedin ve `index.html` içindeki `width`/`height` değerlerini görselin boyutuyla eşleştirin. Görsel CSS ile yuvarlak gösterilir.
- Form alanı eklerseniz `name` özniteliği verin; Netlify yalnızca HTML'de tanımlı alanları kaydeder.

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

**İletişim formu:** Mesajlar her iki adreste de Firestore'a (`messages` koleksiyonu) kaydedilir ve admin panelinde okunur. Kayıt başarısız olursa "Gönder" butonu ziyaretçinin e-posta uygulamasını doldurulmuş mesajla açar.

## Admin paneli

`/admin.html` (ör. https://gamzeagaoglu.web.app/admin.html) adresinden e-posta ve şifreyle giriş yapılır. Sayfa arama motorlarına kapalıdır ve ana sitede bağlantısı yoktur. Panelde:

- **Mesajlar:** İletişim formundan gelen mesajlar; okundu/okunmadı işaretleme, yanıtlama ve silme
- **Durum:** Ana sayfadaki "Yeni iş birliklerine açığım" etiketini açıp kapatma ve metnini değiştirme
- **Metinler:** Giriş metni, Hakkımda paragrafları ve bölüm açıklamaları (Türkçe ve İngilizce)
- **Çalışma alanları:** Kart ekleme, düzenleme, sıralama ve kaldırma

Panelde kaydedilen içerik Firestore'daki `content/site` belgesinde tutulur ve sitede `index.html`'deki varsayılan metinlerin üzerine yazılır. Değişiklikler yeniden yayın gerektirmez; sayfa yenilenince görünür. Firestore'a ulaşılamazsa site varsayılan içerikle açılır.

Güvenlik `firestore.rules` dosyasındaki kurallarla sağlanır. Ziyaretçiler içeriği okuyabilir ve kurallara uyan mesaj bırakabilir. Mesajları okuma ve içeriği değiştirme yalnızca Firebase Authentication'daki admin hesabının UID'sine açıktır. Admin şifresi Firebase konsolundan (**Authentication → Users**) ya da giriş ekranındaki **"Şifremi unuttum"** bağlantısıyla değiştirilebilir.

## Yayın

Site iki yerde yayındadır:

- **Netlify:** https://gamzeagaoglu.netlify.app — `main` dalına yapılan her push otomatik yayınlanır.
- **Firebase Hosting:** https://gamzeagaoglu.web.app — Firebase projesi `kisiselportfolyositesi`, site `gamzeagaoglu`. Otomatik değildir; değişiklikten sonra elle yayınlanır:

```bash
firebase login          # memisoglugamze@gmail.com
firebase deploy --only hosting            # site dosyaları
firebase deploy --only firestore:rules    # firestore.rules değiştiyse
```

Ayarlar `firebase.json` ve `.firebaserc` dosyalarındadır. Yalnızca site dosyaları yayınlanır; gizli dosya ve klasörler (`.git`, `.github`) ile README, kurallar ve ayar dosyaları hariç tutulur.

## Dosyalar

- `index.html` — Sayfa içeriği, stiller ve etkileşimler
- `admin.html` — Admin paneli (Firebase Authentication + Firestore)
- `colors.css` — Ortak renk paleti
- `profile.jpeg` — Hero bölümündeki yuvarlak profil fotoğrafı (680×680)
- `firebase.json`, `.firebaserc` — Firebase Hosting ayarları
- `firestore.rules` — Firestore güvenlik kuralları

## Özelleştirme

- Metinleri ve proje/çalışma alanı kartlarını `index.html` içinde güncelleyin. Türkçe metin HTML'de durur; İngilizcesi script'teki `STR.en` sözlüğünde, kartlarınki `PROJECTS` içindeki `en` alanındadır. Bir metni değiştirirseniz İngilizcesini de güncelleyin.
- Yeni bir iş deneyimi eklerseniz hem "Deneyim" bölümünü hem de script'teki `CAREER` dizisini güncelleyin; pano süreleri bu diziden hesaplanır.
- Renkleri `colors.css` dosyasındaki CSS değişkenlerinden düzenleyin; koyu tema `:root`, açık tema `:root[data-theme="light"]` bloğundadır.
- Profil görselini değiştirecekseniz en az 640×640 piksel kare bir görseli `profile.jpeg` adıyla kaydedin ve `index.html` içindeki `width`/`height` değerlerini görselin boyutuyla eşleştirin. Görsel CSS ile yuvarlak gösterilir.
- Form alanı eklerseniz `firestore.rules` içindeki `isValidMessage` kuralına da ekleyin; kural listede olmayan alanları reddeder.
- Durum etiketi, metinler ve çalışma alanları admin panelinden de değiştirilebilir. Panelde kaydedilmiş içerik koddaki varsayılanların önüne geçer; `index.html`'de bu metinleri değiştirdiyseniz admin panelinden de güncelleyin.

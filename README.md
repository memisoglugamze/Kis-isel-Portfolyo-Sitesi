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

- Hakkımda, yetenekler, deneyim ve eğitim bölümleri
- Kategori filtreleriyle çalışma alanları
- Mobil gezinme menüsü ve duyarlı sayfa düzeni
- Erişilebilirlik iyileştirmeleri: klavye odağı, atlama bağlantısı, ARIA durumları ve azaltılmış hareket tercihi
- İletişim formu için temel doğrulama ve iş birliği konusunu forma aktarma

**İletişim formu demo amaçlıdır.** Form verileri gönderilmez; gerçek gönderim için bir form/API servisi bağlanmalıdır.

## Dosyalar

- `index.html` — Sayfa içeriği, stiller ve etkileşimler
- `colors.css` — Ortak renk paleti
- `shared-image.jpeg` — Profil fotoğrafı

## Özelleştirme

- Metinleri ve proje/çalışma alanı kartlarını `index.html` içinde güncelleyin.
- Renkleri `colors.css` dosyasındaki CSS değişkenlerinden düzenleyin.
- Profil görselini değiştirecekseniz `index.html` içindeki `shared-image.jpeg` yolunu yeni görselin yolu ile eşleştirin.
- Gerçek form gönderimi için `index.html` içindeki iletişim formu JavaScript koduna bir gönderim servisi ekleyin.

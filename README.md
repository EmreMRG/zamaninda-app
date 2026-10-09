# Zamanında — Takvim ve Hatırlatıcı (Android)

Hatırlatma ekle, zamanı gelince telefon sesli bildirim versin. "Yaptım" demezsen
bildirim **10 dakikada bir** tekrar gelir (ayarlardan 5/10/15/30 dk seçilebilir).
Yazı boyutu Küçük / Orta / Büyük seçilebilir, veriler telefonda saklanır.

Uygulamanın tamamı `www/index.html` dosyasındadır. Android tarafı Capacitor ile
hazırlanmıştır (`android/` klasörü).

---

## 1. Yol: Bilgisayara hiçbir şey kurmadan APK almak (önerilen)

GitHub, APK'yı senin yerine derler.

1. github.com'da yeni, **boş** bir depo aç (ör. `zamaninda`).
2. Depo sayfasında **"uploading an existing file"** bağlantısına tıkla ve bu zip'in
   içindeki **tüm dosya ve klasörleri** (`.github` klasörü dahil) sürükleyip bırak,
   **Commit changes** de.
   - `.github` klasörü gizli görünebilir; sürüklerken atlanmadığından emin ol.
3. Üstteki **Actions** sekmesine gir. "APK oluştur" işi kendiliğinden başlar
   (başlamazsa soldan seç → **Run workflow**). 3–6 dakika sürer.
4. İş yeşil tik alınca içine gir, en alttaki **Artifacts** bölümünden
   **Zamaninda-APK** dosyasını indir. Zip'i açınca `app-debug.apk` çıkar.
5. APK'yı telefona at (Drive, WhatsApp'ta kendine, USB…), dokunup kur.
   Telefon "bilinmeyen kaynak" uyarısı verirse o uygulama için izin ver.

## 2. Yol: Android Studio ile

Gerekenler: Node.js 22+, Android Studio (güncel sürüm).

```bash
npm install
npx cap sync android
npx cap open android
```

Android Studio açılınca telefonu USB ile bağla (Geliştirici seçenekleri → USB hata
ayıklama açık) ve ▶ Run'a bas. Ya da **Build → Build App Bundle(s)/APK(s) → Build APK(s)**.

---

## İlk açılışta telefonda yapılacaklar (önemli)

1. **Bildirim izni** sorulduğunda **İzin ver** de.
2. **Pil kısıtlamasını kaldır:** Ayarlar → Uygulamalar → Zamanında → Pil →
   **Kısıtlama yok / Optimize etme**. Xiaomi, Samsung, Huawei, Oppo gibi markalar
   bunu yapmazsan arka plandaki bildirimleri geciktirebilir veya hiç göstermeyebilir.
   (Xiaomi'de ayrıca **Otomatik başlatma**'yı aç.)
3. Uygulamada **Ayarlar → "1 dakika sonrasına deneme hatırlatması kur"** de, telefonu
   kilitle ve bildirimin geldiğini kontrol et.

## Nasıl çalışır

- Bildirimler telefonun kendi alarm sistemine kurulur; uygulama kapalı, telefon
  kilitli olsa da çalar. Telefon yeniden başlarsa kurulu bildirimler geri yüklenir.
- Onaylanmayan her hatırlatma için 3 saatlik tekrar zinciri kurulur (10 dk aralıkla
  18 bildirim). Uygulamayı her açtığında zincir yenilenir.
- Bildirimdeki **Yaptım ✓** düğmesi uygulamayı açar ve hatırlatmayı tamamlar;
  kalan tekrarlar iptal edilir. Tekrarlı hatırlatmalar (her gün/hafta/ay) bir
  sonraki tarihe geçer.
- Telefon **sessiz moddaysa** bildirim sesi çalmaz, yalnızca titrer.
- Bildirim sesini Android ayarlarından değiştirebilirsin:
  Ayarlar → Uygulamalar → Zamanında → Bildirimler → Hatırlatmalar → Ses.

## Değişiklik yapmak

`www/index.html` dosyasını düzenle, sonra `npx cap sync android` çalıştır
(GitHub yolunu kullanıyorsan dosyayı depoda güncellemen yeterli, APK yeniden derlenir).

Paket adı: `com.mrg.zamaninda` · Capacitor 8

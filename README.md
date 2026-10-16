# 🏮 Fener Bekçisi

Fenerleri yak, karanlığı yen. Tek dosyalık (`index.html`) bir tarayıcı oyunu: 1-2 kişilik görevler, düello, online oyun,
özel modlar ve Bom Kartları. Aynı oyun üç yoldan dağıtılır:

| Nerede | Nasıl |
|---|---|
| **PC / telefon tarayıcısı, iPhone ana ekranı** | GitHub Pages (otomatik yayın) |
| **Android APK** | GitHub Actions ile derlenir |
| **Tek dosya** | `index.html`'i direkt aç |

## Klasörler

```
index.html              oyunun kendisi (düzenlenecek tek dosya)
manifest.webmanifest    iPhone/Android "ana ekrana ekle" bilgileri (ad, simge)
sw.js                   çevrimdışı çalışma
*.png                   uygulama simgeleri
android/                Android uygulama projesi (içinde oyunun kopyası var)
tools/android_html.py   index.html'i Android için hazırlar (workflow çalıştırır)
.github/workflows/      pages.yml (site) ve apk.yml (APK)
```

## 1) GitHub'a yükleme (bilgisayara bir şey kurmadan)

1. github.com'da **New repository** ile boş bir depo aç (örn. `fener-bekcisi`).
2. Bu zip'in **içindekileri** (klasörün kendisini değil) çıkar; `.github` klasörü dahil hepsini depoya sürükle-bırak:
   **Add file → Upload files**. `.github` gizli klasör görünür; Mac'te `Cmd+Shift+.` ile gösterebilirsin.
3. **Commit changes** de.

Komut satırı tercih edersen:

```bash
git init -b main && git add . && git commit -m "Fener Bekçisi"
git remote add origin https://github.com/KULLANICI/fener-bekcisi.git
git push -u origin main
```

## 2) Siteyi aç (GitHub Pages)

1. Depoda **Settings → Pages → Build and deployment → Source: GitHub Actions** seç.
2. **Actions** sekmesinde "Siteyi yayinla" çalışır (1-2 dk). Bitince adres:
   `https://KULLANICI.github.io/DEPO-ADI/`
3. Bu adres https olduğu için **online 6 haneli kod** burada çalışır (Claude önizlemesinde çalışmaz).

## 3) iPhone'a "uygulama" gibi kur (App Store gerekmez)

1. iPhone'da **Safari** ile yukarıdaki adresi aç.
2. **Paylaş (□↑) → Ana Ekrana Ekle → Ekle**.
3. Ana ekranda "Fener Bekçisi" adı ve fener simgesiyle tam ekran açılır, internetsiz de çalışır.
4. Eski simge görünürse ana ekrandan sil, sayfayı yenile, yeniden ekle.

Android Chrome'da da ⋮ menüsü → **Uygulamayı yükle**.

## 4) Android APK

1. **Actions → "Android APK derle" → Run workflow**.
2. 3-5 dakika sonra çalışmanın sayfasında **Artifacts → Fener-Bekcisi-APK** dosyasını indir (zip içinde `app-debug.apk`).
3. Telefona at, aç; "bilinmeyen kaynaklardan yükleme" izni iste.

APK'yı **Releases** sayfasında kalıcı yapmak için bir etiket at: `git tag v1.0 && git push --tags`
(APK sürüm sayfasına otomatik eklenir). Debug imzalıdır; Google Play için kendi imza anahtarınla release derlemesi gerekir.

## Güncelleme

`index.html`'i düzenle → commit et. Site otomatik güncellenir, APK de `index.html` değişince yeniden derlenir.
Sürüm numarası dosyada `BUILD='v56'` (ayarlarda ve ana ekranda görünür). Yeni sürüm açılınca eski önbellek kendini yeniler.

## Online oyun hakkında

- Oyuncular birbirine doğrudan (WebRTC) bağlanır. Oda kodları ücretsiz `ntfy.sh` sunucusu üzerinden eşleşir.
- Farklı ağlarda (mobil veri/ev Wi-Fi) bağlanma olmazsa Ayarlar → Online → **Bağlantı testi** ekranından kendi TURN sunucunu ekleyebilirsin.
- Hata ayıklama için Ayarlar → Online → **Hata / bağlantı kaydı**.

## Reklam / ileride eklemek için

`index.html` içinde boş bir `adBreak(tür, geriÇağrı)` fonksiyonu hazır; reklam kodu buraya bağlanır.
Reklam gelirli kullanımda barındırma sağlayıcının şartlarını kontrol et (GitHub Pages ve Cloudflare Pages uygundur).

# Mersin Toprak Lastik — Web Sitesi

Goodyear Yetkili Bayii **Mersin Toprak Lastik** için hazırlanmış, GitHub Pages üzerinde
doğrudan yayınlanabilen, backend gerektirmeyen kurumsal web sitesi.

Kod yazmayı bilmenize gerek yok — bu dosya size adım adım her şeyi anlatıyor.

---

## 1. Klasör Yapısı

```
mersin-toprak-lastik/
│
├── index.html          → Ana sayfa
├── lastikler.html       → Goodyear lastikleri + filtre
├── hizmetler.html       → Tüm hizmetler (Lastik Oteli dahil)
├── kampanyalar.html     → Kampanyalar / duyurular
├── hakkimizda.html      → Hakkımızda
├── galeri.html          → Fotoğraf galerisi
├── iletisim.html        → İletişim + Google Harita
│
├── css/
│   └── style.css        → Tüm site tasarımı
│
├── js/
│   ├── main.js           → Navbar, WhatsApp linkleri, ürün kartları
│   └── arac-bulucu.js    → "Aracınıza Uygun Lastiği Bulun" mantığı
│
├── data/
│   ├── vehicles.json     → Araç / lastik ebadı verisi (şu an boş)
│   └── products.json     → Goodyear ürün verisi (şu an boş)
│
├── images/
│   ├── logo/              → Logo dosyaları buraya eklenebilir
│   ├── hero/               → Ana sayfa hero fotoğrafı (gerçek mağaza fotoğrafı burada)
│   ├── products/            → Ürün görselleri
│   ├── services/             → Hizmet görselleri
│   └── gallery/               → Galeri fotoğrafları
│
├── favicon.svg
├── robots.txt
├── sitemap.xml
└── README.md
```

---

## 2. GitHub Pages'te Yayınlama (Adım Adım)

1. **GitHub'da hesap açın** (yoksa) → https://github.com
2. **Yeni bir repository (depo) oluşturun**
   - Sağ üstteki **+** işaretine tıklayın → **New repository**
   - İsim verin, örn: `mersin-toprak-lastik`
   - **Public** seçili olsun
   - **Create repository** butonuna basın
3. **Dosyaları yükleyin**
   - Depo sayfasında **Add file → Upload files** butonuna tıklayın
   - Bu klasördeki **tüm dosya ve klasörleri** (index.html, css/, js/, data/, images/ vb.) sürükleyip bırakın
   - Alt kısımda **Commit changes** butonuna basın
4. **Settings (Ayarlar) sekmesine gidin**
   - Depo sayfasının üstünde **Settings** sekmesine tıklayın
5. **Pages bölümünü bulun**
   - Sol menüde **Pages** yazısına tıklayın
6. **Deploy from branch** seçin
   - **Source**: "Deploy from a branch" seçili olmalı
7. **main** dalını seçin
   - Branch: **main**
8. **/root** klasörünü seçin
   - Klasör: **/ (root)**
9. **Save** butonuna basın
10. Birkaç dakika içinde siteniz şu adreste yayında olacak:
    `https://KULLANICI-ADINIZ.github.io/mersin-toprak-lastik/`

> Not: Site canlıya alındıktan sonra `index.html`, tüm `.html` dosyaları ve
> `sitemap.xml` içindeki `https://mersintopraklastik.github.io/` adresini,
> GitHub'ın size verdiği gerçek adresle (veya aşağıdaki özel alan adınızla)
> değiştirmeniz SEO açısından faydalı olacaktır.

---

## 3. İleride Özel Alan Adı (Custom Domain) Bağlama

Bir alan adı (ör. `mersintopraklastik.com`) satın aldığınızda:

1. Alan adını aldığınız firmanın panelinden bir **CNAME kaydı** oluşturun:
   - Ad: `www` (veya kullanmak istediğiniz alt alan adı)
   - Değer: `KULLANICI-ADINIZ.github.io`
2. Kök alan adı (`mersintopraklastik.com`) için GitHub'ın önerdiği **A kayıtlarını** ekleyin (GitHub Pages → Settings → Pages → Custom domain kısmında bu kayıtlar gösterilir).
3. GitHub deposunda **Settings → Pages → Custom domain** alanına alan adınızı yazıp **Save** deyin.
4. **Enforce HTTPS** kutucuğunu işaretleyin (DNS yayıldıktan sonra aktif olur, birkaç saat sürebilir).
5. Yayılma tamamlandığında siteniz kendi alan adınızdan erişilebilir olacaktır.

---

## 4. Yeni Araç Nasıl Eklenir? (`data/vehicles.json`)

Bu dosya, ana sayfadaki "Aracınıza Uygun Lastiği Bulun" bölümünü besler.
**Sadece doğrulanmış, gerçek verileri ekleyin.** Uydurma veri eklemeyin.

Dosyayı GitHub üzerinde açıp kalem ikonuna (Edit) tıklayarak düzenleyebilirsiniz.

### Örnek yapı:

```json
{
  "brands": [
    {
      "name": "Renault",
      "models": [
        {
          "name": "Clio",
          "years": [
            {
              "year": 2022,
              "versions": [
                {
                  "name": "1.0 TCe Joy",
                  "tireSizes": ["195/55 R16", "205/45 R17"]
                }
              ]
            }
          ]
        }
      ]
    }
  ]
}
```

### Adım adım:
1. `"brands"` dizisine yeni bir marka nesnesi ekleyin (örn. `"name": "Renault"`).
2. O markanın içine `"models"` dizisinde modelleri ekleyin (örn. `"name": "Clio"`).
3. Her modelin `"years"` dizisine yıl bilgisi ekleyin (örn. `"year": 2022`).
4. Her yılın `"versions"` dizisine motor/versiyon adı ve o versiyona ait
   **fabrika çıkışı / doğrulanmış lastik ebatlarını** (`"tireSizes"`) ekleyin.
5. Dosyayı kaydedin (Commit changes). Site birkaç dakika içinde günceli gösterecektir.

Veri eklemediğiniz sürece site kullanıcıya dürüstçe
**"Bu araç için henüz doğrulanmış veri eklenmemiştir."** mesajını gösterir —
bu normaldir ve kasıtlıdır.

---

## 5. Yeni Goodyear Ürünü Nasıl Eklenir? (`data/products.json`)

Bu dosya "Goodyear Lastikleri" bölümünü ve `lastikler.html` sayfasındaki
kataloğu besler.

### Örnek yapı:

```json
{
  "products": [
    {
      "name": "Goodyear EfficientGrip Performance 2",
      "season": "Yaz",
      "vehicleType": "Binek",
      "size": "205/55 R16",
      "description": "Yakıt tasarrufu ve ıslak zemin performansı odaklı yaz lastiği.",
      "image": "./images/products/efficientgrip-performance-2.jpg"
    }
  ]
}
```

### Alanlar:
- `name` → Ürün adı (zorunlu)
- `season` → "Yaz", "Kış" veya "4 Mevsim" (filtrelemede kullanılır)
- `vehicleType` → "Binek", "SUV" veya "Ticari" (filtrelemede kullanılır)
- `size` → Lastik ebadı, örn. `205/55 R16`
- `description` → Kısa açıklama (opsiyonel)
- `image` → Görsel dosya yolu, örn. `./images/products/urun-adi.jpg` (opsiyonel — boş bırakılırsa nötr bir simge gösterilir)

Görseli önce `images/products/` klasörüne yükleyin, sonra `image` alanına
dosya yolunu yazın.

Sitede **fiyat gösterilmez** — her ürün kartında "WhatsApp'tan Fiyat Al"
butonu bulunur, bu tasarım gereği değiştirilmemelidir.

---

## 6. Gelecekte API Entegrasyonu

`js/arac-bulucu.js` dosyasındaki şu fonksiyonlar modüler tasarlanmıştır:

```
getBrands()
getModels(marka)
getYears(marka, model)
getVersions(marka, model, yıl)
getTireSizes(marka, model, yıl, versiyon)
```

Şu an bu fonksiyonlar `/data/vehicles.json` dosyasından okuma yapıyor.
İleride profesyonel bir lastik fitment API'sine geçmek isterseniz,
**sadece bu fonksiyonların içini** `fetch()` ile ilgili API endpoint'ine
bağlanacak şekilde değiştirmeniz yeterlidir — sayfanın geri kalanı
(dropdown'lar, sonuç kartları) hiç değişmeden çalışmaya devam eder.

**ÖNEMLİ GÜVENLİK NOTU:** GitHub Pages salt statik dosya barındırır ve
gizli bilgi saklayamaz. Bu yüzden API anahtarı gerektiren bir servise
bağlanacaksanız, anahtarı **asla** bu JavaScript dosyalarına yazmayın.
Bunun yerine anahtarı saklayan basit bir sunucu/proxy (örn. Cloudflare
Workers, Vercel Functions) kullanın ve bu sayfadan sadece o proxy'ye
istek atın.

---

## 7. Sık Sorulan Sorular

**Cumartesi çalışma saatiniz neden yazmıyor?**
Doğrulanmış bir bilgi verilmediği için sitede uydurma saat gösterilmemiştir.
Kesin saat belirlendiğinde `index.html` ve `iletisim.html` dosyalarındaki
"Çalışma saatleri için iletişime geçiniz." metnini gerçek saatle
değiştirebilirsiniz (metni arayıp bulun ve düzenleyin).

**WhatsApp numarası nereden değişir?**
`js/main.js` dosyasının en üstündeki `BUSINESS` nesnesindeki
`whatsappNumber` alanından. Tüm site bu tek kaynaktan besleniyor.

**Telefon numarası nereden değişir?**
Aynı dosyada `phoneHref` ve `phoneDisplay` alanlarından. Ayrıca her
sayfadaki `tel:+90...` linklerinin de güncellenmesi gerekir (arama/bulma ile
kolayca yapılabilir).

**Google yorumları neden yok?**
Google API bağlantısı kurulmadan sahte yorum/puan oluşturulmaması bilinçli
bir tercihtir. Google Business Profile API veya benzeri bir entegrasyon
kurulduğunda bu bölüm gerçek yorumlarla doldurulabilir.

---

## 8. Yerel Olarak Önizleme (İsteğe Bağlı)

Herhangi bir kurulum yapmadan `index.html` dosyasına çift tıklayarak
tarayıcınızda önizleyebilirsiniz. `fetch()` ile JSON okuma özelliğinin
tam çalışması için basit bir yerel sunucu kullanmanız önerilir
(zorunlu değildir, GitHub Pages'te sorunsuz çalışır):

```bash
# Python yüklüyse, proje klasöründe:
python3 -m http.server 8000
# Tarayıcıda: http://localhost:8000
```

---

© 2026 Mersin Toprak Lastik. Tüm hakları saklıdır.

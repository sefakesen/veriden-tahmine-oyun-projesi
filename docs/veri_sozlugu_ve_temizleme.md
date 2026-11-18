# Aşama 2: Veri Sözlüğü ve Temizleme Adımları

## Veri Seti Hakkında

- **Dosya:** `data/oyun_verileri.csv`
- **Ham Boyut:** 96 satır, 11 sütun (Temizleme sonrası: 89 satır, 11 sütun)
- **Kapsam:** Çeşitli tür ve platformlardaki tanınmış oyunların temel mağaza ve oynanış bilgileri ile yaklaşık kullanıcı puanı verilerinden derlenmiştir.

## Veri Sözlüğü

| Sütun Adı | Tip | Anlamı |
| :--- | :--- | :--- |
| `oyun_adi` | Kategorik (Metin) | Oyunun adı. Model eğitiminde kullanılmaz, kayıtları ayırt etmek içindir. |
| `tur` | Kategorik | Oyunun ana türü (`Aksiyon`, `RPG`, `Strateji`, `Simulasyon`, `Bulmaca`, `Spor`). |
| `platform` | Kategorik | Oyunun yayınlandığı platform (`PC`, `Konsol`, `Mobil`, `Coklu Platform`). |
| `gelistirme_olcegi` | Kategorik | Geliştirici stüdyo ve bütçe ölçeği (`Indie`, `Orta Olcekli`, `AAA`). |
| `cikis_yili` | Sayısal | Oyunun çıkış yılı (`2009`-`2024`). |
| `fiyat_usd` | Sayısal | Satış fiyatı (USD). `0` değeri ücretsiz oyunları ifade eder. |
| `ortalama_oynanis_saati` | Sayısal | Oyuncuların oyunu ortalama oynama süresi (saat). |
| `cok_oyunculu` | Kategorik | Çok oyunculu mod desteği olup olmadığı (`Evet` / `Hayir`). |
| `erken_erisim` | Kategorik | Erken erişim (Early Access) sürecinden geçip geçmediği (`Evet` / `Hayir`). |
| `dlc_sayisi` | Sayısal | Oyun için yayınlanan ek paket (DLC) sayısı. |
| `kullanici_puani` | Sayısal (**Hedef y**) | Oyunun 0-100 arasındaki kullanıcı puanı. |

## Veri Temizleme Adımları

Ham veri `pd.read_csv` ile okunduktan sonra şu temizleme adımları uygulanmıştır:

1. **Tekrar eden satırların kaldırılması (`drop_duplicates`):** Birebir aynı olan 2 tekrarlı satır silinmiştir.
2. **Hedef değişkendeki eksik ve hatalı puanların çıkarılması (`dropna` + aralık filtresi):** `kullanici_puani` boş olan 2 satır ile 0-100 aralığı dışındaki 1 hatalı puan (`115.0`) çıkarılmıştır. Hedef değişken tahmin edilmeye çalışılan sütun olduğu için doldurulmaz.
3. **Hatalı özellik değerlerinin temizlenmesi:** Negatif fiyat (`-19.99`) ve gelecekten hatalı çıkış yılı (`2099`) içeren 2 hatalı satır filtrelenmiştir.
4. **Eksik özellik değerlerinin doldurulması (`isnull` + `fillna`):** `platform` sütunundaki 2 boş değer en sık geçen kategoriyle (mod), `fiyat_usd`, `ortalama_oynanis_saati` ve `dlc_sayisi` sütunlarındaki boş değerler ise uç değerlerden etkilenmemesi için medyan ile doldurulmuştur.

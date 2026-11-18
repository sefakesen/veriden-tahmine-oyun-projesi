# Aşama 1: Problem Tanımı ve Proje Planı

## Proje Tanım Formu

- **Proje Adı:** Uçtan Uca Yapay Zeka Projesi: Veriden Tahmine
- **Seçilen Alan:** Oyun (Video Oyunları)
- **Problem Cümlesi:** Bir oyunun türü, platformu, geliştirme ölçeği, çıkış yılı, fiyatı (USD), ortalama oynanış süresi, çok oyunculu desteği, erken erişim durumu ve DLC sayısı bilgilerinden yola çıkarak kullanıcı puanını (0–100) tahmin et.
- **Özellik Değişkenleri (X):** `tur`, `platform`, `gelistirme_olcegi`, `cikis_yili`, `fiyat_usd`, `ortalama_oynanis_saati`, `cok_oyunculu`, `erken_erisim`, `dlc_sayisi`
- **Hedef Değişken (y):** `kullanici_puani`
- **Problem Türü:** Regresyon (hedef değişken 0–100 arasında sürekli bir sayısal puan olduğu için)

## Gerekçe (Bu Problem Neden Önemli?)

Bir oyun geliştirilirken satış fiyatının ne olacağı, erken erişimle çıkıp çıkmayacağı, çok oyunculu mod eklenip eklenmeyeceği veya kaç adet ek paket (DLC) hazırlanacağı doğrudan oyuncu tepkisini etkiler. Özellikle küçük ve orta ölçekli oyun stüdyoları sınırlı bütçelerini doğru yönetebilmek için bu özelliklerin oyuncu memnuniyetine nasıl yansıdığını önceden görmek ister. Benzer oyunların geçmiş verilerine bakarak kullanıcı puanını tahmin eden bir model, geliştiricilere çıkış öncesinde fiyat ve içerik dengesini ayarlama konusunda fikir verirken; oyunculara ve yayıncılara da bir oyunun beklenen kalitesi hakkında ön değerlendirme imkânı sunar.

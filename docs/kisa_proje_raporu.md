# Kısa Proje Raporu: Uçtan Uca Yapay Zeka Projesi (Veriden Tahmine)

## 1. Problem
Bu projede video oyunlarına ait temel özellikler (`tur`, `platform`, `gelistirme_olcegi`, `cikis_yili`, `fiyat_usd`, `ortalama_oynanis_saati`, `cok_oyunculu`, `erken_erisim`, `dlc_sayisi`) kullanılarak oyunun `kullanici_puani` (0-100) tahmin edilmiştir. Hedef değişken sayısal olduğu için problem **Regresyon** olarak ele alınmıştır. Amaç, geliştiricilere çıkış öncesi fiyat ve içerik dengesini değerlendirmede veri destekli bir ön bakış sunmaktır.

## 2. Veri
Çeşitli tür ve platformlardaki tanınmış oyunlardan derlenen **96 satır, 11 sütunluk** `oyun_verileri.csv` dosyası `pd.read_csv` ile okunmuştur. Temizleme sürecinde 2 tekrar eden satır (`drop_duplicates`), 2 eksik hedef satırı (`dropna`), 1 aralık dışı puan (`115.0`) ile 2 hatalı özellik kaydı (`-19.99` fiyat, `2099` yılı) çıkarılmış; kalan boş özellikler mod ve medyan ile (`fillna`) doldurularak **89 temiz kayıt** elde edilmiştir. Keşif analizinde `Indie` oyunların ortalama `90.1`, `AAA` oyunların ise `73.4` puana sahip olduğu görülmüştür.

## 3. Model
Kategorik sütunlar `pd.get_dummies` ile sayısal hale getirilmiş (16 özellik) ve veri `%75` eğitim (`66` satır), `%25` test (`23` satır) olarak bölünmüştür. Sayısal tahmin için `LinearRegression` ana model olarak kurulmuş, karşılaştırma amacıyla da `DecisionTreeRegressor` (`max_depth=3`, `min_samples_leaf=5`) eğitilmiştir.

## 4. Sonuç
| Model | Eğitim $R^2$ | Test $R^2$ (`score`) | Test MAE | Test RMSE |
| :--- | :---: | :---: | :---: | :---: |
| **LinearRegression** | 0.555 | **0.524** | 9.65 | 13.00 |
| **DecisionTreeRegressor** | 0.518 | 0.453 | 9.49 | 13.93 |

Seçilen `LinearRegression` modeli 4 yeni senaryoda Indie RPG (`87.2`) ve Indie Strateji (`89.8`) oyunlarına yüksek; pahalı ve kısa süreli AAA Aksiyon (`65.4`) ile ücretsiz mobil spor oyununa (`49.3`) daha düşük tahminler üretmiştir.

## 5. Çıkarım
Eğitim (`0.555`) ve test (`0.524`) $R^2$ skorlarının birbirine yakın olması modelin aşırı öğrenmeye (overfitting) düşmediğini göstermektedir. Yaklaşık `9.6` puanlık ortalama hata payı, kullanıcı puanının yalnızca mağaza fiyatına veya oynanış süresine değil; hikaye kalitesi, optimizasyon sorunları ve oyun içi satın alma tepkileri gibi veri setinde yer almayan etkenlere de bağlı olmasından kaynaklanmaktadır. Gelecek çalışmalarda örnek sayısını artırıp oyuncu yorumu metinleri veya eleştirmen puanı eklenerek doğruluk yükseltilebilir.

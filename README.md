# INTEL IMAGE CLASSIFICATION PROJESİ

Bu proje, Intel Image Classification veri seti kullanılarak **CNN ve Transfer Learning (VGG16)** modelleri ile doğal sahne görüntülerinin sınıflandırılmasını amaçlamaktadır.

## Veri Seti
- [Intel Image Classification Dataset](https://www.kaggle.com/dataset/puneet6060/intel-image-classification)
- 6 sınıf :
{'buildings' -> 0,
'forest' -> 1,
'glacier' -> 2,
'mountain' -> 3,
'sea' -> 4,
'street' -> 5 }
- 25.000 eğitim ve 14.000 test verisi olarak ayrılmıştır.


## 1.Kütüphanelerin Yüklenmesi ve GPU Kontrolü
- TensorFlow, Keras, NumPy, Matplotlib, Seaborn, Scikit-learn gibi kütüphaneler yüklendi.
- GPU nun çalışıp çalışmadığı kontrol edildi.

## 2.Veri Setinin Yüklenmesi ve Hazırlanması
- Intel Image Classification veri seti kullanıldı.
- Görseller 150*150 boyutuna dönüştürüldü.
- Normalizasyon (0-1 aralığına ölçekleme) yapıldı.
- Eğitim ve test verisi %80-%20 oranında ayrıldı.

## 3.Veri Görselleştirme
- Eğitim verisinden 25 görsel görselleştirildi.
- Eğitim ve test verisi sınıf dağılımları grafikleştirildi.

## 4.One-Hot Encoding ve Veri Artırma
- Etiketler one-hot encoding  formatına dönüştürüldü.
- Data Augmentation(rotation,width/height shift, horizontal flip, zoom) kullanılarak modelin genelleme gücünü artırmak ve overfitting' azaltmak amaçlanmıştır.

## 5.Temel CNN Modeli
- 3 evrişim bloğu (Conv2D+BatchNormalization+MaxPooling+Dropout) kullanıldı.
- Dense katmanlar ve softmax aktivasyonu ile 6 sınıfa ayrım yapıldı.
- `Adam` optimizer ;`categorical_crossentropy` loss ; `accuracy` metrik
- EarlyStopping ve ReduceLROnPlateau callback'leri kullanıldı.

## 6.Modelin Eğitilmesi
- 50 epoch boyunca batch size 65 ile eğitim yapıldı.
- Eğitim/Doğrulama doğruluğu ve Eğitim/Doğruluk kaybı grafikleri çizildi.

## 7.Model Değerlendirme
- Test setinde model doğruluk ve kaybı hesaplandı.
- Classification report ve confusion matrix üretildi.
- Doğru ve yanlış tahmin edilen örnekler görselleştirildi.

## 8.Transfer Learning(VGG16)
- ImageNet ağırlıklı VGG16 modeli kullanıldı.
- Katmanlar donduruldu üstüne yeni Dense katmanlar eklendi.
- Model 20 epoch boyunca eğitildi ve test doğruluğu hesaplandı.

## 9.Model Performans Karşılaştırılması
- Temel CNN ile Transfer Learning doğrulukları karşılaştırıldı.
- Bar chat yöntemi ile görselleştirme yapıldı.
- CNN ara katman öznitelik haritaları görselleştirildi.

## Kullanılan Yöntemler
- Temel CNN modeli:3 evrişim bloğu, dropout ve batch normalization
- Transfer Learning: VGG16 ile katmanlar donduruldu ve sınıflandırıcı eklendi
- Data augmentation: Döndürme,yatay çevirme,kaydırma,zoom
- Optimizatörler:Adam,RMSprop,SGD karşılaştırma

## Sonuçlar
| Model   |     Test Doğruluğu       |
|---------|--------------------------|
| CNN     |      0.9020              | 
| VGG16   |      0.8881              |


**En iyi optimizatör: Adam(0.8440)**

## Kaggle Notebook
[Kaggle Notebook Linki](https://www.kaggle.com/code/burinreyyan/notebookba3b467302)

## Dataset
[Dataset Linki](https://www.kaggle.com/datasets/puneet6060/intel-image-classification)


## Sonuç
- Temel CNN modeli , Transfer Learning modeline kıyasla daha yüksek doğruluk sağlamıştır.
- Adam optimizatörü, denenen optimizatörler arasında en iyi performansı göstermiştir.
- Veri artırma ve doğru optimizatör seçimi, modelin performansını artırmada önemli rol oynamıştır.
- Öznitelik haritaları ve görselleştirmeler , modelin görsel özellikleri nasıl öğrendiğini anlamaya yardımcı olmuştur.(Model hangi filtreler ile görüntüdeki kenarları, dokuları veya nesne parçalarını yakaladığını görebildik.Hangi katmanların daha genel veya daha spesifik özellikleri öğrendiğini gözlemleyebildik.)

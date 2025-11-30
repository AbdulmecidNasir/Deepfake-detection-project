# 🕵️‍♂️ Deepfake Tespiti: Görüntü İşleme ve Derin Öğrenme Yaklaşımı

![Project Banner](images/Detectify_Group_Banner.png)


| **Bölüm** | **Proje Detayları** |
| :--- | :--- |
| **Ders / Grup** | [cite_start]Görüntü İşleme (FET312) - Güz 2024 / **Detectify** [cite: 4, 7] |
| **Proje Amacı** | Bu proje, **FaceForensics++ (C23)** veri setini kullanarak, manipüle edilmiş (deepfake) ve gerçek videoları ayırt edebilen yüksek doğruluklu derin öğrenme modelleri geliştirmeyi amaçlar. [cite_start]Proje, video karelerinden yüz tespiti, özellik çıkarma ve sınıflandırma süreçlerini kapsayan uçtan uca bir sistem sunar[cite: 9, 10, 11]. |
| **Veri Seti** | [cite_start]**Kaynak:** FaceForensics++ (C23 Sıkıştırma)<br>**İçerik:** 250 Gerçek Video (Original), 50 Sahte Video (Deepfakes, Face2Face, FaceSwap, FaceShifter)<br>**İşleme:** Her videodan 20 kare (frame) çıkarılmıştır.<br>**Eğitim/Test:** %80 Eğitim, %20 Doğrulama ayrımı yapılmıştır[cite: 23, 24, 25, 26]. |
| **Metodoloji** | **1. [cite_start]Ön İşleme:** Videolardan kare çıkarma, **MTCNN** ile yüz tespiti ve kırpma, yeniden boyutlandırma (128x128 / 224x224), Normalizasyon (0-1 arası)[cite: 33, 34, 35].<br>**2. Veri Artırma:** RandomFlip, RandomRotation gibi tekniklerle veri seti zenginleştirilmiştir.<br>**3. Modelleme:** Ekip üyeleri tarafından 3 farklı mimari (Custom CNN, Transfer Learning, EfficientNet) geliştirilmiştir. |
| **Kullanılan Modeller** | [cite_start]Projede karşılaştırmalı analiz için 3 farklı yaklaşım uygulanmıştır:<br>• **Model 1 (Custom CNN):** Sıfırdan tasarlanan, 4 bloklu konvolüsyonel sinir ağı.<br>• **Model 2 (InceptionResNetV2 + SVM):** Transfer learning ile özellik çıkarma ve klasik makine öğrenmesi ile sınıflandırma.<br>• **Model 3 (EfficientNetB0):** Hafif ve verimli bir modern mimari kullanımı[cite: 42, 44, 45]. |
| **Performans** | [cite_start]**Custom CNN Sonuçları:**<br>• Doğrulama Doğruluğu (Val Accuracy): **%98**<br>• Kayıp (Loss): Düşük hata oranı ile stabil öğrenme.<br>*(Diğer modellerin sonuçları karşılaştırmalı olarak rapora eklenmiştir)*[cite: 68, 69]. |
| **Teknolojiler** | [cite_start]Python, TensorFlow/Keras, OpenCV, MTCNN, Scikit-learn, Matplotlib, Google Colab (T4 GPU)[cite: 63, 64]. |
| **Kurulum** | Projeyi yerel ortamınızda çalıştırmak için:<br>```bashgit clone [https://github.com/KULLANICI_ADINIZ/Detectify-Deepfake-Detection.gitcd](https://github.com/KULLANICI_ADINIZ/Detectify-Deepfake-Detection.gitcd) Detectify-Deepfake-Detectionpip install tensorflow opencv-python mtcnn scikit-learn matplotlib``` |
| **Takım Üyeleri** | [cite_start]**Diyorjon Ochilov** (22040101007)<br>• *Model:* **InceptionResNetV2 + SVM/RandomForest** (Transfer Learning) [cite: 13][cite_start]<br><br>**Khaiitmurod Khabibullayev** (22040101002)<br>• *Model:* **Custom CNN** (Özel Tasarım Derin Ağ) [cite: 14][cite_start]<br><br>**Abdumajid Abdulkhaev** (22040101003)<br>• *Model:* **EfficientNetB0 + LSTM** (Hibrit Mimari) [cite: 15] |
| **Lisans** | Bu proje akademik eğitim amaçlı geliştirilmiştir. |

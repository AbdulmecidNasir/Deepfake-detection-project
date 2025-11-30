# 🕵️‍♂️ Deepfake Tespiti: Görüntü İşleme ve Derin Öğrenme Yaklaşımı

![Project Banner](images/Detectify_Group_Banner.png)

| **Bölüm** | **Proje Detayları** |
| :--- | :--- |
| **Ders / Grup** | Görüntü İşleme (FET312) - Güz 2024 / **Detectify** |
| **Proje Amacı** | Bu proje, **FaceForensics++ (C23)** veri setini kullanarak, manipüle edilmiş (deepfake) ve gerçek videoları ayırt edebilen yüksek doğruluklu derin öğrenme modelleri geliştirmeyi amaçlar. [cite_start]Proje; video karelerinden yüz tespiti, özellik çıkarma ve sınıflandırma süreçlerini kapsayan uçtan uca bir sistem sunar. |
| **Veri Seti** | [cite_start]**Kaynak:** FaceForensics++ (C23 Sıkıştırma)<br>**İçerik:** 250 Gerçek Video (Original), 50 Sahte Video (Deepfakes, Face2Face, FaceSwap, FaceShifter)<br>**İşleme:** Her videodan 20 kare (frame) çıkarılmıştır.<br>**Eğitim/Test:** %80 Eğitim, %20 Doğrulama ayrımı yapılmıştır. |
| **Metodoloji** | **1. Ön İşleme:** Videolardan kare çıkarma, **MTCNN** ile yüz tespiti ve kırpma, yeniden boyutlandırma (128x128), Normalizasyon (0-1 arası).<br>**2. Veri Artırma:** RandomFlip, RandomRotation gibi tekniklerle veri seti zenginleştirilmiştir.<br>**3. [cite_start]Modelleme:** CNN mimarileri ve Transfer Learning yaklaşımları uygulanmıştır. |
| **Kullanılan Modeller** | Projede karşılaştırmalı analiz için farklı CNN mimarileri geliştirilmiştir:<br>• **SimpleCNN:** Temel seviye, 3 evrişim katmanlı mimari.<br>• **Custom CNN:** Girdi boyutu optimize edilmiş özelleştirilmiş mimari.<br>*(Detaylar takım üyeleri bölümündedir)* |
| **Performans** | [cite_start]**Pilot Sonuçlar:**<br>• **Custom CNN:** Eğitim Doğruluğu %99, Doğrulama Doğruluğu **%98** (Yüksek Başarım).<br>• **SimpleCNN:** Eğitim Doğruluğu %95, Doğrulama Doğruluğu %77 (Overfitting gözlemlendi, geliştirmeler planlandı)[cite: 17]. |
| **Teknolojiler** | Python, TensorFlow/Keras, OpenCV, MTCNN, Scikit-learn, Matplotlib, Google Colab (T4 GPU). |
| **Kurulum** | Projeyi yerel ortamınızda çalıştırmak için:<br>```bashgit clone [https://github.com/KULLANICI_ADINIZ/Detectify-Deepfake-Detection.gitcd](https://github.com/KULLANICI_ADINIZ/Detectify-Deepfake-Detection.gitcd) Detectify-Deepfake-Detectionpip install tensorflow opencv-python mtcnn scikit-learn matplotlib``` |
| **Takım Üyeleri** | **Abdumajid Abdulkhaev** (22040101002)<br>• Girdi boyutunu optimize ederek (128x128) ve Rescaling katmanı kullanarak özelleştirilmiş bir CNN mimarisi tasarlamış ve test etmiştir. Final aşamasında hafif ve hızlı **MobileNetV2** mimarisi üzerinde çalışmayı planlamaktadır.<br><br>**Khaiitmurod Khabibullayev** (22040101116)<br>• Veri işleme boru hattını (pipeline) kurmuş; 3 evrişim katmanlı, Dropout destekli "SimpleCNN" temel modelini geliştirmiş ve analiz etmiştir. Final aşamasında **InceptionV3** mimarisi üzerinde çalışmayı planlamaktadır. |
| **Lisans** | Bu proje akademik eğitim amaçlı geliştirilmiştir. |

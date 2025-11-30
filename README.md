<div align="center">
<!-- BURAYA BANNER FOTOĞRAFINIZI EKLEYİN. Örnek: -->
<!-- <img src="https://user-images.githubusercontent.com/username/repo/banner.png" alt="Proje Banner'ı" width="900"/> -->
Derin Evrişimli Sinir Ağları ile Deepfake Video Tespiti
FET312 - Derin Öğrenme Dersi / 2025-2026 Güz Dönemi Vize Projesi
Ekip Adı: Detectify
</div>
Bu proje, İstanbul Topkapı Üniversitesi FET312 - Derin Öğrenme dersi kapsamında, Deepfake teknolojisiyle manipüle edilmiş videoları tespit etmek için temel (baseline) Konvolüsyonel Sinir Ağı (CNN) modellerinin geliştirilmesi ve performans analizini konu almaktadır.
📝 İçindekiler
Problem Tanımı ve Hedefler
Veri Seti
Genel Metodoloji
Ekip Katkıları ve Geliştirilen Modeller
Performans Sonuçları ve Analiz
Gelecek Çalışmalar: Final Aşaması Planı
Kullanılan Teknolojiler ve Kütüphaneler
Kurulum ve Çalıştırma
🎯 Problem Tanımı ve Hedefler
Günümüzde "Deepfake" teknolojisi, yapay zeka ile gerçeği manipüle etme konusunda ciddi bir tehdit oluşturmaktadır. Bu projenin temel bilimsel sorusu, insan gözüyle ayırt edilmesi zorlaşan görsel manipülasyonların, piksel düzeyindeki tutarsızlıklar kullanılarak otomatik olarak tespit edilip edilemeyeceğidir.
Proje, İkili Sınıflandırma (Binary Classification) problemi olarak ele alınmış ve bir videonun "Gerçek (Real)" mi yoksa "Sahte (Fake)" mi olduğunu belirlemeyi amaçlamaktadır.
Vize Aşaması (Baseline): Sıfırdan tasarlanan sığ (shallow) CNN modelleri ile rassal tahminin (%50) üzerine çıkarak, modelin manipülasyon izlerini öğrenmeye başladığını kanıtlamak. Hedef, %60-65 arası doğruluk ve 0.50 üzeri F1 Skoru'na ulaşmaktır.
Final Aşaması (Advanced): Transfer Öğrenme (Transfer Learning) tekniği kullanarak literatürdeki standartlara yaklaşmak ve %85 üzeri doğruluk hedeflemek.
📊 Veri Seti
Veri Kümesi: FaceForensics++ (FF++)
Kaynak: Kaggle ve TU Munich
Detaylar: C23 (orta seviye) sıkıştırma uygulanmış videolardan oluşmaktadır.
Eğitim Seti: Toplam 500 video (250 Gerçek, 250 Sahte). Sahte videolar, farklı manipülasyon tekniklerinden (Deepfakes, Face2Face, FaceSwap vb.) 50'şer adet içermektedir.
Test Seti: Eğitimde hiç kullanılmamış 50 video (25 Gerçek, 25 Sahte) içeren bir "Hold-out Test Seti" oluşturulmuştur.
⚙️ Genel Metodoloji
Tüm ekip üyeleri tarafından ortak bir veri işleme boru hattı (pipeline) izlenmiştir:
Video Okuma: Eğitim ve test setlerindeki .mp4 formatındaki videolar okunur.
Karelere Ayırma (Frame Extraction): Her videodan saniyede belirli aralıklarla kareler çıkarılır.
Yüz Tespiti ve Kırpma: MTCNN veya face_recognition kütüphaneleri kullanılarak her karedeki insan yüzleri tespit edilir ve kırpılır.
Yeniden Boyutlandırma: Kırpılan yüz görüntüleri, her üyenin kendi model mimarisine uygun olarak yeniden boyutlandırılır.
Model Eğitimi: Hazırlanan yüz görüntüleri ile her üyenin kendi tasarladığı CNN modeli eğitilir.
Değerlendirme: Modelin performansı, test setindeki videolar üzerinde karelerin çoğunluk oyu (Majority Voting) yöntemiyle ölçülür.
👥 Ekip Katkıları ve Geliştirilen Modeller
Ekibimiz, farklı temel model yaklaşımlarını karşılaştırmak amacıyla aşağıdaki şekilde iş bölümü yapmıştır:
Geliştirici	Öğrenci No	Geliştirilen Model	Öne Çıkan Mimarî Özellikler
Khaiitmurod Khabibullayev	22040101116	SimpleCNN	3 evrişim katmanlı temel bir yapı. Aşırı öğrenmeyi engellemek için %50 Dropout katmanı kullanılmıştır. Girdi boyutu 224x224 pikseldir.
Muhammed Ali Cüre	23040101006	BatchNormCNN	4 evrişim katmanı ile daha derin bir özellik çıkarımı hedeflenmiştir. Eğitimi stabilize etmek için her evrişim katmanından sonra Batch Normalization ve "ölü nöron" problemini çözmek için LeakyReLU aktivasyon fonksiyonu eklenmiştir. Girdi boyutu 224x224 pikseldir.
Abdumajid Abdulkhaev	22040101002	RescaledCNN	İşlem yükünü azaltmak amacıyla girdi boyutu 128x128 piksele optimize edilmiştir. Modelin girişine piksel değerlerini aralığına normalize eden yerleşik bir Rescaling katmanı eklenmiştir. Daha az parametre ile öğrenmesi hedeflenmiştir.
📈 Performans Sonuçları ve Analiz
Tüm modeller, 50 videoluk (25 Gerçek, 25 Sahte) "Hold-out Test Seti" üzerinde değerlendirilmiştir.
Performans Karşılaştırma Tablosu
Model Geliştiricisi	Model Mimarisi	Doğruluk (Accuracy)	Hassasiyet (Precision-Fake)	Duyarlılık (Recall-Fake)	F1 Skoru
Muhammed Ali Cüre	BatchNormCNN	%62.00	0.80	0.32	0.46
Khaiitmurod Khabibullayev	SimpleCNN	%58.00	0.83	0.20	0.32
Abdumajid Abdulkhaev	RescaledCNN	%50.00	0.50	1.00	0.67
Sonuçların Yorumlanması
En İyi Başarı (BatchNormCNN): Muhammed Ali'nin geliştirdiği model, %62 doğruluk oranıyla en iyi genel performansı sergilemiştir. Batch Normalization katmanlarının, modelin veri setindeki gürültüye karşı daha dirençli olmasını sağlayarak daha iyi genelleme yapmasına yardımcı olduğu düşünülmektedir.
Yüksek Hassasiyet, Düşük Duyarlılık (SimpleCNN): Khaiitmurod'un modeli, %83 gibi çok yüksek bir Precision değerine ulaşmıştır. Bu, modelin bir videoya "Sahte" dediğinde büyük olasılıkla doğru tahminde bulunduğunu, ancak emin olamadığı birçok sahte videoyu "Gerçek" olarak etiketleyerek "muhafazakar" davrandığını göstermektedir (Düşük Recall: 0.20).
Model Sapması / Bias Problemi (RescaledCNN): Abdumajid'in modeli, tüm sahte videoları doğru tahmin etmiş (Recall: 1.00) ancak tüm gerçek videoları da sahte olarak etiketlemiştir. Bu durum, modelin ayırt edici özellikleri öğrenmekte zorlandığını ve tüm girdileri "Sahte" olarak tahmin etme eğilimine (Mode Collapse) girdiğini göstermektedir. Bu, basit CNN mimarilerinin karmaşık deepfake manipülasyonlarını öğrenmedeki zorluğunu kanıtlamaktadır.
🚀 Gelecek Çalışmalar: Final Aşaması Planı
Vize aşamasında elde edilen temel model sonuçları, basit ve sığ CNN yapılarının bu problemde yetersiz kaldığını göstermiştir. Final projesinde, modelleri daha derinleştirmek ve önceden eğitilmiş (pre-trained) ağırlıkları kullanmak (Transfer Learning) zorunlu hale gelmiştir.
Geliştirici	Planlanan Gelişmiş Mimari	Seçim Nedeni
Khaiitmurod Khabibullayev	InceptionV3	Farklı boyutlardaki filtreleri paralel kullanarak görüntüdeki hem ince hem de kaba detayları aynı anda yakalayabilme yeteneği.
Abdumajid Abdulkhaev	ResNet50	Derin ağlardaki "kaybolan gradyan" problemini "Skip Connections" ile çözerek görsel özellikleri kaybetmeden derinlemesine analiz yapabilme.
Muhammed Ali Cüre	MobileNetV2	Düşük hesaplama maliyetiyle yüksek verimlilik sunması. Mobil veya gerçek zamanlı sistemler için hafif model ihtiyacını karşılama potansiyeli.
🛠️ Kullanılan Teknolojiler ve Kütüphaneler
<p align="left">
<a href="https://www.python.org" target="_blank"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="40" height="40"/> </a>
<a href="https://www.tensorflow.org" target="_blank"> <img src="https://www.vectorlogo.zone/logos/tensorflow/tensorflow-icon.svg" alt="tensorflow" width="40" height="40"/> </a>
<a href="https://keras.io/" target="_blank"> <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/ae/Keras_logo.svg/1200px-Keras_logo.svg.png" alt="keras" width="40" height="40"/> </a>
<a href="https://scikit-learn.org/" target="_blank"> <img src="https://upload.wikimedia.org/wikipedia/commons/0/05/Scikit_learn_logo_small.svg" alt="scikit_learn" width="40" height="40"/> </a>
<a href="https://opencv.org/" target="_blank"> <img src="https://www.vectorlogo.zone/logos/opencv/opencv-icon.svg" alt="opencv" width="40" height="40"/> </a>
<a href="https://pandas.pydata.org/" target="_blank"> <img src="https://raw.githubusercontent.com/devicons/devicon/2ae2a900d2f041da66e950e4d48052658d850630/icons/pandas/pandas-original.svg" alt="pandas" width="40" height="40"/> </a>
<a href="https://numpy.org/" target="_blank"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/numpy/numpy-original.svg" alt="numpy" width="40" height="40"/> </a>
<a href="https://matplotlib.org/" target="_blank"> <img src="https://matplotlib.org/_static/logo_dark.svg" alt="matplotlib" width="40" height="40"/> </a>
<a href="https://colab.research.google.com/" target="_blank"> <img src="https://www.vectorlogo.zone/logos/google_colab/google_colab-icon.svg" alt="colab" width="40" height="40"/> </a>
</p>
🚀 Kurulum ve Çalıştırma
Bu repoyu klonlayın:
code
Bash
git clone https://github.com/murat-khabibullayev/Deepfake-detection-project.git
Gerekli kütüphaneleri yükleyin. Notebook'un en başındaki !pip install komutlarını çalıştırmanız yeterlidir.
code
Bash
pip install tensorflow mtcnn scikit-learn pandas opencv-python matplotlib
Projeyi Deepfake_Detection.ipynb Jupyter Notebook dosyasını Google Colaboratory üzerinde açarak çalıştırın. Veri setinin ve modelin kaydedileceği yolların kendi Google Drive yapınızla uyumlu olduğundan emin olun.

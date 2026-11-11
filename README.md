# 🛸 Real-Time UAV Detection & Deep Learning Benchmark Platform (YOLOv8 • YOLOv9 • YOLOv10)

[![Live Demo](https://img.shields.io/badge/🚀_CANLI_WEB_PLATFORMU-Tıkla_ve_Canlı_Test_Et-4338CA?style=for-the-badge)](https://uav-detection-benchmark.streamlit.app/)
[![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://uav-detection-benchmark.streamlit.app/)
[![PyTorch](https://img.shields.io/badge/PyTorch-CUDA_RTX_4060-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)](https://uav-detection-benchmark.streamlit.app/)
[![Streamlit](https://img.shields.io/badge/Streamlit-Cloud_App-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)](https://uav-detection-benchmark.streamlit.app/)

Bu proje, **"UAV Detection Using Deep Learning Based Models"** başlıklı akademik araştırmanın bulgularını ve eğitilmiş derin öğrenme modellerini uçtan uca deneyimlemek amacıyla geliştirilmiş interaktif bir **Uygulamalı Yapay Zeka (Applied AI) Web Platformudur**.

### 🌐 Canlı Uygulama Linki (Kurulum Gerektirmez):
👉 **[https://uav-detection-benchmark.streamlit.app/](https://uav-detection-benchmark.streamlit.app/)**

---

## 🎯 Projenin Amacı ve Mühendislik Kapsamı

İnsansız Hava Araçlarının (İHA / Drone) sivil ve askeri güvenlik alanlarında oluşturduğu tehditleri gerçek zamanlı tespit edebilmek için **hız (FPS)** ve **doğruluk (mAP)** dengesini optimize eden **YOLOv8, YOLOv9 ve YOLOv10** mimarileri **15.311 görüntülük** genişletilmiş bir veri seti üzerinde eğitilmiş ve canlı bir web arayüzüne dönüştürülmüştür.

### ✨ Web Platformunun 3 Ana Modülü
1. **⚔️ Canlı İHA Tespit & Yan Yana A/B Model Yarıştırma Motoru:** Ziyaretçiler kendi bilgisayarlarında drone fotoğrafı aramadan sayfada yer alan **9 farklı hazır test senaryosu** (sabit kanatlı İHA, çim/gölge kamuflajı, şehir içi cam yansıması, uzak mesafe vb.) üzerinde tek tıkla test yapabilir veya kendi görüntüsünü yükleyebilir. **Canlı A/B Testi** modunda iki farklı YOLO modeli aynı görüntü üzerinde eşzamanlı çalıştırılarak çıkarım süreleri (`ms` / `FPS`), güven skorları (`Confidence`) ve tespit kutuları yan yana kıyaslanır.
2. **📊 Veri Bilimi & Akademik Benchmark Panosu:** Makaledeki tüm deneysel sonuçları (Hız-Doğruluk-Parametre balon grafiği, Eğitim maliyeti analizi, 1.359 görüntülük ön çalışmadaki Overfitting kanıtı, Confusion Matrix ısı haritaları ve Literatür kıyaslaması) **Plotly** tabanlı interaktif grafiklerle sunar.
3. **🗄️ Çift Katmanlı SQLite Veritabanı & Excel/CSV Raporlama:** Sitede gerçekleştirilen her tekli analiz ve yan yana A/B düellosu arka planda otomatik olarak ilişkisel **SQLite (`uav_detection_logs.db`)** veritabanına kaydedilir. Kullanıcılar geçmiş testleri filtreleyebilir ve tek tıkla **`.xlsx` (Excel)** veya **`.csv`** formatında indirebilir.

---

## 📊 Deneysel Sonuçlar Özeti (15.311 Görüntü - Final Çalışması)

Araştırma kapsamında Kaggle (*YOLO Drone Detection Dataset* - 1.359 görüntü) ve Roboflow üzerinden özel etiketlenen verilerin birleştirilmesiyle **15.311 görüntülük** (13.928 Eğitim / 1.383 Doğrulama) veri seti oluşturulmuştur. Eğitim ve FPS testleri **13. Nesil Intel® Core™ i7-13620H CPU**, **NVIDIA GeForce RTX 4060 (8GB VRAM) GPU** ve **48 GB RAM** donanımında gerçekleştirilmiştir:

| Model Mimarisi | Giriş Çözünürlüğü | Parametre (M) | mAP@50 (%) | mAP@50:95 (%) | Kesinlik / Precision (%) | Duyarlılık / Recall (%) | F1-Skoru (%) | Çıkarım Hızı (FPS) | Gecikme / Latency (ms) | Eğitim Süresi (Saat) | Öne Çıkan Mimari Özellik |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :--- |
| **YOLOv8m** | `1024×1024` | 25.9 M | **%97.7** | %66.5 | **%96.0** | **%96.5** | **%96.3** | 24.03 FPS | 41.61 ms | 38.65 sa | Yüksek Çözünürlük & En Düşük Yanlış Alarm (66 FP) |
| **YOLOv9t** | `640×640` | **2.0 M** | %97.1 | %65.4 | %95.2 | %95.4 | %95.3 | 188.60 FPS | 5.30 ms | 7.03 sa | **PGI & GELAN** ile 5.5x Büyük YOLOv8s'ten Üstün |
| **YOLOv10n** | `640×640` | 2.3 M | %96.9 | %66.0 | %94.9 | %93.9 | %94.4 | **344.80 FPS** | **2.90 ms** | 4.66 sa | **NMS-Free** Çift Etiket Atama ile Hız Rekoru |
| **YOLOv8s** | `640×640` | 11.1 M | %96.9 | **%66.6** | %95.8 | %95.9 | %95.8 | 108.84 FPS | 9.19 ms | **3.77 sa** | Anchor-Free Dengeli Baseline Mimari |

### 🔬 Öne Çıkan 3 Mühendislik Bulgusu
* **1. Çözünürlük ve Yakalama Hassasiyeti (`YOLOv8m`):** `1024×1024` piksel çözünürlükte eğitilen `YOLOv8m`, uzak ve kamufle olmuş İHA'larda piksel kaybını önleyerek **%97,7 mAP@50** ve **%96,5 Recall** ile "sıfıra yakın kaçırma" (*near-zero miss*) başarısı göstermiş; doğrulama setinde 1.452 doğru tespit (TP) ve yalnızca 66 yanlış alarm (FP) üretmiştir.
* **2. NMS-Free Mimarisi ve Gerçek Zamanlı Hız (`YOLOv10n`):** Geleneksel Non-Maximum Suppression (NMS) son işleme darboğazını ortadan kaldıran `YOLOv10n`, yalnızca **2,90 ms** gecikme süresiyle **344,8 FPS** hıza ulaşarak literatürdeki yüksek doğruluklu modelleri yaklaşık **2,5 kat** geride bırakmıştır.
* **3. "Büyük Model Her Zaman Daha İyi Değildir" (Overfitting Analizi):** Araştırmanın 1.359 görüntülük ilk aşamasında **43,6M parametreli `YOLOv8l` (%92,0 mAP@50)** modeli dar veri setinde aşırı öğrenmeye (*overfitting*) düşerek **3,0M parametreli küçük `YOLOv8n` (%93,4 mAP@50)** modelinin gerisinde kalmıştır.

---

## 🛠️ Teknoloji Yığını (Tech Stack)
* **Derin Öğrenme & Bilgisayarlı Görü:** Python 3.12, PyTorch (CUDA), Ultralytics YOLO (v8, v9, v10), OpenCV, Pillow
* **Web Arayüzü & Veri Görselleştirme:** Streamlit, Özel Çift Temalı CSS Motoru (*Warm AI Studio* & *Tactical Aerospace HUD*), Plotly Interactive Charts
* **Veritabanı & Raporlama:** SQLite3 (`ab_comparison_logs` & `detection_logs` ilişkisel tabloları), Pandas, OpenPyXL (`.xlsx` / `.csv` dışa aktarma)

---

## 🔒 Telif ve Model Ağırlıkları Bildirimi
Akademik çalışmanın özgünlüğünü ve 15.311 görüntülük veri seti üzerinde eğitilen özel `.pt` model ağırlık dosyalarını (`yolov8m.pt`, `yolov10n.pt`, `yolov9t.pt`, `yolov8s.pt`) korumak amacıyla kaynak kodlar ve model ağırlıkları **özel (Private) depoda** barındırılmakta olup, tüm fonksiyonlar **[Canlı Web Platformu](https://uav-detection-benchmark.streamlit.app/)** üzerinden interaktif olarak test edilebilmektedir.

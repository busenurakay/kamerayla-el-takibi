# Kamerayla El Takibi

OpenCV ve MediaPipe kullanılarak geliştirilen gerçek zamanlı el tespiti ve parmak sayma projesi.

Bu proje, webcam üzerinden alınan canlı görüntü üzerinde gerçek zamanlı el tespiti, 21 eklem noktasının (landmark) çizimi ve açık parmak sayısının hesaplanması amacıyla **OpenCV** ve **MediaPipe** kütüphaneleri kullanılarak geliştirilmiştir.

## Proje Özellikleri
- **Canlı Görüntü İşleme:** OpenCV ile kameradan anlık görüntü yakalama ve ayna görünümü.
- **El ve Eklem Tespiti:** MediaPipe `HandLandmarker` modeli ile el üzerindeki 21 temel eklem noktasının ve kemik bağlantılarının tespiti.
- **Parmak Sayma Algoritması:** Parmak uçları (`4, 8, 12, 16, 20`) ile alt eklem koordinatlarının karşılaştırılması yoluyla açık parmak sayısının (0–5) gerçek zamanlı ekrana yazdırılması.

## ekran görüntüleri

<img width="1920" height="1080" alt="Ekran görüntüsü 2026-11-13 225251" src="https://github.com/user-attachments/assets/d965180b-d53b-4796-91a5-592951898017" />
<img width="1920" height="1020" alt="Ekran görüntüsü 2026-11-13 225104" src="https://github.com/user-attachments/assets/fe355cde-ca05-40ab-b86c-0bb0e92d4fd5" />

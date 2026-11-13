import os
import urllib.request
import cv2
import mediapipe as mp
from mediapipe.tasks import python
from mediapipe.tasks.python import vision

model_yolu = "hand_landmarker.task"
if not os.path.exists(model_yolu):
    url = "https://storage.googleapis.com/mediapipe-models/hand_landmarker/hand_landmarker/float16/1/hand_landmarker.task"
    urllib.request.urlretrieve(url, model_yolu)

base_options = python.BaseOptions(model_asset_path=model_yolu)
options = vision.HandLandmarkerOptions(
    base_options=base_options,
    num_hands=1,
    min_hand_detection_confidence=0.7,
    min_tracking_confidence=0.7
)
detector = vision.HandLandmarker.create_from_options(options)

baglantilar = [
    (0, 1), (1, 2), (2, 3), (3, 4),
    (0, 5), (5, 6), (6, 7), (7, 8),
    (5, 9), (9, 10), (10, 11), (11, 12),
    (9, 13), (13, 14), (14, 15), (15, 16),
    (13, 17), (0, 17), (17, 18), (18, 19), (19, 20)
]
parmak_uclari = [4, 8, 12, 16, 20]

cap = cv2.VideoCapture(0)
print("Kamera açılıyor... Kapatmak için açılan kamera penceresine tıklayıp 'q' tuşuna basın.")

while True:
    basarili, kare = cap.read()
    if not basarili:
        print("Kameradan görüntü alınamadı!")
        break

    kare = cv2.flip(kare, 1)
    rgb_kare = cv2.cvtColor(kare, cv2.COLOR_BGR2RGB)
    mp_image = mp.Image(image_format=mp.ImageFormat.SRGB, data=rgb_kare)

    sonuc = detector.detect(mp_image)
    acik_parmak_sayisi = 0

    if sonuc.hand_landmarks:
        yukseklik, genislik, _ = kare.shape
        for el_noktalari in sonuc.hand_landmarks:
            nokta_listesi = []
            for id, lm in enumerate(el_noktalari):
                cx, cy = int(lm.x * genislik), int(lm.y * yukseklik)
                nokta_listesi.append((id, cx, cy))

            for baslangic, bitis in baglantilar:
                cv2.line(kare, (nokta_listesi[baslangic][1], nokta_listesi[baslangic][2]),
                         (nokta_listesi[bitis][1], nokta_listesi[bitis][2]), (255, 255, 255), 2)

            for _, cx, cy in nokta_listesi:
                cv2.circle(kare, (cx, cy), 5, (0, 0, 255), -1)

            parmaklar = []
            if nokta_listesi[5][1] < nokta_listesi[17][1]:
                parmaklar.append(1 if nokta_listesi[4][1] < nokta_listesi[3][1] else 0)
            else:
                parmaklar.append(1 if nokta_listesi[4][1] > nokta_listesi[3][1] else 0)

            for id in range(1, 5):
                if nokta_listesi[parmak_uclari[id]][2] < nokta_listesi[parmak_uclari[id] - 2][2]:
                    parmaklar.append(1)
                else:
                    parmaklar.append(0)

            acik_parmak_sayisi = sum(parmaklar)

    cv2.rectangle(kare, (15, 15), (320, 85), (0, 0, 0), -1)
    cv2.putText(kare, f"Acik Parmak: {acik_parmak_sayisi}", (25, 62),
                cv2.FONT_HERSHEY_SIMPLEX, 1.1, (0, 255, 0), 3)

    cv2.imshow("Kamerayla El Takibi - Cikis icin 'q'", kare)

    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()

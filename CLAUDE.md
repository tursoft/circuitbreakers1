# CircuitBreakers1 - Uzaktan Kumandalı Robot Projesi

## Proje Ozeti

Deneyap Kart 1A ile kontrol edilen, 4 tekerlekli ve servo tabanli robotik kollu bir robot. Uzaktan kumanda olarak Deneyap Kart Mini kullanilir. Iki kart arasindaki iletisim ESP-NOW protokolu ile saglanir.

### Tasarim Oncelikleri
- **Hafiflik:** Robot mumkun oldugunca hafif tutulmali. Bilesen secimlerinde agirlik oncelikli kriter olarak degerlendirilir. Agir bilesenllerden kacinilir (ornegin JGA25-370 yerine TT motor tercih edilir).
- **Hiz ve Ceviklik:** Robot hizli ve cevik olmali. Ani hizlanma, hizli donus ve duyarli kontrol onceliklidir. Motor seciminde RPM degeri yuksek tutulur.

## Sistem Mimarisi

### Robot (Alici) - Deneyap Kart 1A
- **Islemci:** ESP32-WROVER-E (Dual-core, 240 MHz) veya ESP32-S3 (v2)
- **Gorev:** Motor surucu kontrolu, servo kontrolu, ESP-NOW uzerinden komut alma
- **Baglantilar:**
  - 4x DC motor - Blue TT Motor 1:48 metal disli (L298N motor surucu uzerinden)
  - 3x Servo motor MG996R - metal disli (robotik kol: taban, omuz, dirsek)
  - 1x Servo motor MG90S - metal disli (tutucu)
  - ESP-NOW alici (WiFi radyo)

### Kumanda (Gonderici) - Deneyap Kart Mini
- **Islemci:** ESP32-S2 (Single-core, 240 MHz)
- **Gorev:** Kullanici girdilerini okuma, ESP-NOW ile robota gonderme
- **Baglantilar:**
  - 2x Joystick modulu (hareket + kol kontrolu)
  - Butonlar (tutucu ac/kapa, hiz modu, acil durdurma)

### Iletisim Protokolu: ESP-NOW
- **Neden ESP-NOW:** Deneyap Mini (ESP32-S2) Bluetooth desteklemiyor. ESP-NOW her iki kartta da WiFi radyosu uzerinden calisir.
- **Gecikme:** ~5-10 ms (gercek zamanli kontrol icin ideal)
- **Menzil:** ~200 m (acik alanda)
- **Paket boyutu:** Maks 250 byte (joystick verileri icin fazlasiyla yeterli)
- **Altyapi gerektirmez:** Router veya WiFi agi gerekmez

## Donanim Listesi

### Robot Tarafi
| Bilesen | Adet | Aciklama |
|---------|------|----------|
| Deneyap Kart 1A | 1 | Ana islem karti |
| L298N Motor Surucu | 2 | Her biri 2 DC motor surer (toplam 4 motor) |
| Blue TT Motor 1:48 Metal Disli | 4 | Teker hareketi (~30g, 3-6V, ~200 RPM @6V, 0.4 kg.cm tork, metal disli) |
| Servo Motor - Metal Disli (MG996R) | 3 | Robotik kol: taban, omuz, dirsek (metal disli, 10 kg.cm tork) |
| Servo Motor - Metal Disli (MG90S) | 1 | Tutucu (metal disli, kompakt, 2.2 kg.cm tork) |
| Li-Po Pil (7.4V 2S, 1500mAh, 25C) | 1 | Guc kaynagi (~85g, hafif, ~30 dk calisma suresi) |
| Voltaj regulatoru (5V) | 1 | Servo ve kart beslemesi |
| Robot sasesi (4WD) | 1 | Mekanik govde |

### Tahmini Agirlik Tablosu (Robot)
| Bilesen | Agirlik |
|---------|---------|
| 4x Blue TT Motor 1:48 | ~120g |
| 3x MG996R Servo | ~165g |
| 1x MG90S Servo | ~14g |
| 2x L298N Motor Surucu | ~60g |
| Deneyap Kart 1A | ~25g |
| Li-Po Pil (1500mAh 2S) | ~85g |
| Sase + tekerlekler | ~150-200g |
| Kablolar, vidalar, diger | ~50g |
| **Toplam (tahmini)** | **~670-720g** |

### Kumanda Tarafi
| Bilesen | Adet | Aciklama |
|---------|------|----------|
| Deneyap Kart Mini | 1 | Kumanda islem karti |
| Joystick modulu | 2 | X-Y analog eksen (hareket + kol) |
| Buton | 3 | Tutucu, hiz modu, acil durdurma |
| Li-Po Pil (3.7V) | 1 | Kumanda gucu |

## Yazilim Mimarisi

### Klasor Yapisi
```
circuitbreakers1/
  robot/
    robot.ino              # Ana robot kodu (alici)
    motor_control.h        # DC motor surucu fonksiyonlari
    motor_control.cpp
    arm_control.h          # Robotik kol servo fonksiyonlari
    arm_control.cpp
    comm_receiver.h        # ESP-NOW alici
    comm_receiver.cpp
    config.h               # Pin tanimlari, sabitler
  kumanda/
    kumanda.ino            # Ana kumanda kodu (gonderici)
    input_reader.h         # Joystick ve buton okuma
    input_reader.cpp
    comm_sender.h          # ESP-NOW gonderici
    comm_sender.cpp
    config.h               # Pin tanimlari, sabitler
  docs/
    pinout_robot.md        # Robot pin baglanti semasi
    pinout_kumanda.md      # Kumanda pin baglanti semasi
    wiring_diagram.md      # Kablolama talimatlari
  proje-tanimi.md
  CLAUDE.md
```

### Veri Paketi Yapisi (ESP-NOW)
```cpp
// Kumandadan robota gonderilen veri paketi
typedef struct {
  int8_t move_x;       // Sol joystick X: -100..+100 (saga/sola donus)
  int8_t move_y;       // Sol joystick Y: -100..+100 (ileri/geri)
  int8_t arm_x;        // Sag joystick X: -100..+100 (taban rotasyonu)
  int8_t arm_y;        // Sag joystick Y: -100..+100 (omuz/dirsek)
  uint8_t buttons;     // Bit alani: tutucu, hiz, durdurma
  uint8_t speed_mode;  // 0: yavas, 1: normal, 2: hizli
} ControlPacket;
```

## Kullanilan Teknolojiler

- **Dil:** C++ (Arduino framework)
- **IDE:** Arduino IDE 2.x
- **Platform:** ESP32 (Deneyap Kart ailesi)
- **Iletisim:** ESP-NOW (WiFi radyo tabanlı, Bluetooth DEGIL)

## Kutuphaneler

### Zorunlu
| Kutuphane | Kaynak | Amac |
|-----------|--------|------|
| `esp_now.h` | ESP-IDF (dahili) | ESP-NOW iletisim |
| `WiFi.h` | ESP-IDF (dahili) | WiFi radyo baslatma (ESP-NOW icin gerekli) |
| `ESP32Servo` | Arduino Library Manager | Servo motor kontrolu |

### Board Paketi Kurulumu (Arduino IDE)
1. File -> Preferences -> Additional Board Manager URLs:
   ```
   https://raw.githubusercontent.com/deneyapkart/deneyapkart-arduino-core/master/package_deneyapkart_index.json
   ```
2. Tools -> Board -> Boards Manager -> "Deneyap Gelistirme Kartlari" ara ve kur
3. Robot icin: Tools -> Board -> "Deneyap Kart 1A" sec
4. Kumanda icin: Tools -> Board -> "Deneyap Mini" sec

## Proje Ciktilari

1. **Robot firmware** (`robot/robot.ino`): ESP-NOW uzerinden komut alan, 4 motoru ve robotik kolu kontrol eden yazilim
2. **Kumanda firmware** (`kumanda/kumanda.ino`): Joystick/buton okuyan ve ESP-NOW ile robota gonderen yazilim
3. **Dokumantasyon** (`docs/`): Pin baglanti semalari ve kablolama talimatlari
4. **Calisir robot sistemi:** Kumandayla gercek zamanli kontrol edilen 4WD robot + robotik kol

## Gelistirme Kurallari

### Genel
- Her `.ino` dosyasi bagimsiz olarak derlenebilmeli (robot ve kumanda ayri projeler)
- `config.h` dosyalari tum pin tanimlari ve sabitleri icerir; magic number kullanilmaz
- Her fonksiyon tek bir sorumluluga sahip olmali
- Degisken ve fonksiyon isimleri Ingilizce, yorumlar Turkce yazilir

### Iletisim
- ESP-NOW MAC adresleri `config.h` icerisinde tanimlanir
- Veri paketi boyutu 250 byte sinirini asmamali
- Kumanda saniyede 50 paket gonderir (20 ms aralik)
- Robot tarafinda baglanti kopma tespiti yapilir (500 ms timeout -> motorlar durur)

### Motor Kontrolu
- PWM frekansi: 1000 Hz
- Motorlar yumusak baslatma/durdurma yapilir (ramping)
- Acil durdurma butonu ani olarak tum motorlari durdurur (ramping yok)

### Robotik Kol
- Servo acilari `config.h` icinde min/max sinirlarla tanimlanir
- Ani hareketler engellenir; servo pozisyonlari kademeli degisir
- Tutucu icin ayri bir buton kullanilir (toggle: ac/kapa)

### Guvenlik
- Kumanda sinyali kesilirse robot otomatik durur (failsafe)
- Motor PWM degerleri `config.h` icinde tanimli maksimum siniri asmaz
- Servo acilari fiziksel sinirlar disina cikmaz
- Li-Po pil voltaj kontrolu yapilir (dusuk voltajda uyari)

### Kod Stili
- Girinti: 2 bosluk
- Suslu parantez: ayni satirda acilir
- Header dosyalarinda include guard kullanilir (`#ifndef`)
- Global degiskenlerden kacinilir; gerektiginde `static` veya namespace kullanilir
- `Serial.begin(115200)` debug icin kullanilir; uretim kodunda `#ifdef DEBUG` ile korunur

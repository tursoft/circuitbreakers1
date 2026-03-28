# CircuitBreakers1 - Uzaktan Kumandalı Robot Projesi

## Proje Ozeti

Deneyap Kart 1A ile kontrol edilen, 4 tekerlekli ve servo tabanli robotik kollu bir robot. Uzaktan kumanda olarak Deneyap Kart Mini kullanilir. Iki kart arasindaki iletisim ESP-NOW protokolu ile saglanir.

### Tasarim Oncelikleri
- **Hafiflik:** Robot mumkun oldugunca hafif tutulmali. Bilesen secimlerinde agirlik oncelikli kriter olarak degerlendirilir. Agir bilesenllerden kacinilir (ornegin JGA25-370 yerine TT motor, L298N yerine TB6612FNG tercih edilir). Hafiflik zipline gorevinde kritik avantaj saglar.
- **Hiz ve Ceviklik:** Robot hizli ve cevik olmali. Ani hizlanma, hizli donus ve duyarli kontrol onceliklidir. Motor seciminde RPM degeri yuksek tutulur. Rakiple ayni anda sahada yarisildigi icin C bolgesine ilk ulasan avantajlidir.
- **Cok Gorevlilik:** Robot 4 farkli gorevi yerine getirmeli: koli tasima/dizme, kasis gecme, halka dizme, zipline gecisi. Mekanizmalar bu gorevlerin tamamina uygun tasarlanmali.
- **60x60x60cm Uyumluluk:** Tum mekanizmalar (kol, zipline kancasi vb.) baslangicta katlanmis halde bu kutunun icine sigmali. Gorev sirasinda acilabilir.

## TEKNOFEST Robolig 2026 - Yarisma Sartnamesi (Lise Kategorisi)

> Kaynak: `dokumantasyon/TEKNOFEST_Robolig_2026_Sartname_TR_v1_16.02.2026_cl2A6.pdf`

### Yarisma Takvimi
| Tarih | Aciklama |
|-------|----------|
| 28.02.2026 | Son basvuru tarihi |
| 23.03.2026 | ODR (On Degerlendirme Raporu) son teslim |
| 22.04.2026 | ODR sonuclari |
| 20.05.2026 | PDR (Proje Detay Raporu) son teslim |
| 19.06.2026 | PDR sonuclari + maddi destek |
| 24.07.2026 | Proje Tanitim Videosu son teslim |
| 07.08.2026 | Finalist takimlarin aciklanmasi |
| Agustos-Eylul 2026 | TEKNOFEST Final yarislari |

### Saha Bilgileri (Lise)
- **Saha boyutu:** 550cm x 350cm
- **3 bolge:** A (guvenli), B (guvenli), C (ortak rekabet alani)
- **Baslangic alani:** 60cm x 60cm (robot bu alana sigmak ZORUNDA)
- **Sure:** 10 dakika / mac
- **2 tur** oynanir (1. tur A'dan, 2. tur B'den baslanir), puanlar toplanir
- **Ayni anda 2 rakip robot** sahada yarisir

### Robot Boyut ve Agirlik Sinirlari (ZORUNLU)
- **Maksimum boyut (baslangic):** 60cm x 60cm x 60cm (yukseklik dahil)
- **Maksimum agirlik:** 20 kg (tum mekanik + elektronik + pil dahil)
- Gorev sirasinda kol vb. mekanizmalar 60cm yuksekligi asabilir
- Baslangicta tum hareketli parcalar kapali/tasinabilir durumda olmali

### Gorevler ve Puanlama (Lise)

#### Gorev 1: Koli Tasima (Guvenli Alan - A/B Bolgesi)
- **4 adet koli** dagitim merkezinde bulunur
- Koli boyutu: **9cm x 9cm x 9cm** (kup)
- Koli agirligi: **50-100 gr**
- Toplama merkezi: **12cm x 12cm** alan
- Koliler toplama merkezine **ust uste dizilmeli** (tasmadan)
- Her koli = **10 puan** (toplam **40 puan**)
- Dusen koliler hakem tarafindan dagitim merkezine geri konur
- **KRITIK: Koliler dizilmeden C bolgesi gorevlerine gecilemez!**

#### Gorev 2: Kasis Gecme (A/B -> C gecisi)
- Dagitim merkezinden C bolgesine gecerken yolda **kasis** bulunur
- Robotun kasis uzerinden gecmesi zorunlu
- Zipline alani ile kasis arasinda **50cm** mesafe var

#### Gorev 3: Enerji Halkasi Dizme (C Bolgesi - Ortak Alan)
- **7 adet enerji halkasi** C bolgesinde bulunur
- Halka ic capi: **9cm**, dis capi: **11cm**
- Halka agirligi: **30-100 gr**
- Enerji kulesi: **30cm uzunluk, 5cm cap** (dikey cubuk)
- Halkalar kuleye gecirilmeli
- Her halka = **5 puan** (toplam **35 puan**)
- **REKABET ALANI:** Rakip robot da ayni anda bu gorevde yarisir

#### Gorev 4: Zipline (C -> A/B donusu)
- Baslangic noktasi (X): yerden **90cm**
- Bitis noktasi (Y): yerden **70cm**
- Hat uzunlugu: **1 metre**
- Zipline hattina **tutunularak** gecilmeli (zeminden gecis puan vermez)
- Basarili gecis = **25 puan**

#### Puan Ozeti (Tek Tur)
| Gorev | Puan |
|-------|------|
| 4x Koli tasima | 40 |
| 7x Halka dizme | 35 |
| Zipline gecisi | 25 |
| **Toplam (maks/tur)** | **100** |

### Nihai Puanlama
- **Parkur yarisi:** %80 (2 turun toplami, 100luk sisteme cevrilerek)
- **Final sunumu:** %20 (juri degerlendirmesi)

### Teknik Zorunluluklar (Sartname Maddeleri)
1. **Deneyap Kart ZORUNLU:** En az bir Deneyap Kart (Kart 1A, Mini vb.) kullanilmali
2. **Acil durdurma butonu ZORUNLU:** Robot uzerinde en az 1 adet
3. **Kabuk/govde:** Tum donanim (sensor, kablo, kontrolcu) govde icinde olmali
4. **Elektriksel guvenlik:** Tum guc hatlari asiri akim/kisa devre korumali (sigorta vb.)
5. **Kablo yalitimi:** Acikta kablo veya elektriksel baglanti olmayacak
6. **Pil koruma:** Pil, darbe ve sivi temasina karsi korunakli bolmede olmali
7. **Yasak mekanizmalar:** Kesici, delici, alev, basinclı gaz, yuksek sicaklik yasak
8. **Yasak mudahale:** Rakip robota fiziksel/dijital saldiri (sinyal kesme vb.) yasak
9. **Guvenli alan ihlali:** Rakip bolgelerine girmek yasak -> o macin puanlari geçersiz

### Tasarima Etkisi - Stratejik Notlar
1. **Koli tasima:** Adaptive gripper ile 9x9x9cm kolileri kavra, 12x12cm alana ust uste diz (4 koli = 36cm). Hizli tasima icin kol hareket hizi optimize edilmeli.
2. **Kasis gecme:** 80mm+ tekerlekler ile yeterli ground clearance saglanir. TT motorlarin torku kasis icin yeterli.
3. **Halka dizme:** Ayni adaptive gripper ile 11cm halkalari kavra, 5cm cubuga gecir. Hassas pozisyonlama gerektirir - joystick kontrolu hassas modda olmali.
4. **Zipline:** MG996R tahrikli teleskopik direk + kanca sistemi. ~700g robot agirligi zipline icin ideal. Direk katlanir halde 60cm sinirinda kalmali.
5. **Hiz stratejisi:** Kolileri hizla bitirip C bolgesine ilk gecen takim halkalarda avantajli olur. Surus hizi ve kol hizi birlikte optimize edilmeli.
6. **60x60x60cm siniri:** Robotik kol ve zipline diregi baslangicta katlanmis durumda. Gorev basladiginda acilir.
7. **Puan onceligi:** Koli (40p) > Halka (35p) > Zipline (25p). Koliler bitmeden C'ye gecilemez, bu yuzden koli tasima hizi en kritik faktordur.

## Sistem Mimarisi

### Robot (Alici) - Deneyap Kart 1A
- **Islemci:** ESP32-WROVER-E (Dual-core, 240 MHz) veya ESP32-S3 (v2)
- **Gorev:** Motor surucu kontrolu, servo kontrolu, zipline mekanizmasi, ESP-NOW uzerinden komut alma
- **Alt Sistemler:**
  - **Surus:** 4x DC motor - Blue TT Motor 1:48 metal disli (TB6612FNG motor surucu uzerinden)
  - **Robotik Kol:** 2x MG996R (taban + omuz) + 1x MG90S (dirsek) + 1x MG90S (adaptive gripper)
  - **Zipline Mekanizmasi:** 1x MG996R (teleskopik direk + kanca/makara) - baslangicta katlanir, gorev sirasinda acilir
  - **Iletisim:** ESP-NOW alici (WiFi radyo)

### Kumanda (Gonderici) - Deneyap Kart Mini
- **Islemci:** ESP32-S2 (Single-core, 240 MHz)
- **Gorev:** Kullanici girdilerini okuma, ESP-NOW ile robota gonderme
- **Baglantilar:**
  - 2x Joystick modulu (hareket + kol kontrolu)
  - Butonlar (tutucu ac/kapa, hiz modu, zipline tetik, acil durdurma)

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
| TB6612FNG Motor Surucu | 2 | Her biri 2 DC motor surer (~3g, verimli, ~0.5V dusus) |
| Blue TT Motor 1:48 Metal Disli | 4 | Teker hareketi (~30g, 3-6V, ~200 RPM @6V, 0.4 kg.cm tork) |
| Servo Motor MG996R (metal disli) | 3 | Kol taban + omuz + zipline mekanizmasi (10 kg.cm tork) |
| Servo Motor MG90S (metal disli) | 2 | Kol dirsek + adaptive gripper (2.2 kg.cm tork) |
| Li-Po Pil (7.4V 2S, 1500mAh, 25C) | 1 | Guc kaynagi (~85g, hafif, ~30 dk calisma suresi) |
| Voltaj regulatoru (5V) | 1 | Servo ve kart beslemesi |
| Robot sasesi (4WD) | 1 | Mekanik govde, 80mm+ tekerlekler (ground clearance icin) |
| Zipline mekanizmasi | 1 | Teleskopik direk + kanca/makara sistemi |
| Acil durdurma butonu | 1 | ZORUNLU - sartname geregi |

### Robot Mekanizma Detaylari

#### Robotik Kol (4 DOF)
| Eklem | Servo | Tork | Gorev |
|-------|-------|------|-------|
| Taban (rotasyon) | MG996R | 10 kg.cm | Tum kolu yatay duzlemde dondurmek |
| Omuz (kaldirma) | MG996R | 10 kg.cm | Kolu yercekimine karsi kaldirmak (en agir yuk) |
| Dirsek (uzanma) | MG90S | 2.2 kg.cm | Kol ucunu konumlandirmak (hafif yuk yeterli) |
| Tutucu (gripper) | MG90S | 2.2 kg.cm | Scoop-Clamp Paddle Gripper - paralel plaka + L-dudak |

- Kol, yerden koli alip ~36cm yukseklige (4 koli ust uste) ulasabilmeli
- Kol, enerji kulesine (30cm) halka gecirebilecek hassasiyette olmali
- **Scoop-Clamp Paddle Gripper (V2):** Paralel hareket eden iki genis plaka + alt L-dudak
  - Rack-pinion mekanizmasiyla MG90S servo ile simetrik acilma/kapanma
  - Aciklik araligi: 0-13cm (9cm koli ve 11cm halka icin yeterli)
  - Her plakanin ic yuzeyinde 2mm silikon pad (kaymaz kavrama)
  - Her plakanin altinda 12mm iceri donuk L-dudak (nesneyi alttan destekler)
  - Koli: plakalar yanlari kavrar + dudaklar tabani destekler (3 yuzey temas)
  - Halka: plakalar dis yuzeyi kavrar + dudaklar alt kenari destekler
  - Halka birakma: kule uzerine pozisyonla, plakalar acilir, halka yercekimiyle cubuga duser
  - Kule capi 5cm < halka ic capi 9cm = 2cm tolerans (hassas hizalama gereksiz)
  - Tasarim dosyalari: `dokumantasyon/tasarim/v2/`

#### Zipline Mekanizmasi
- **Servo:** 1x MG996R (mekanizmayi yukari kaldirmak icin yuksek tork)
- **Yapi:** Teleskopik direk (katlanir halde ~30cm, acik halde ~90cm)
- **Kanca/Makara:** Direg ucunda zipline teline tutunacak kanca veya makara
- **Baslangic durumu:** Katlanmis, 60cm yukseklik siniri icinde
- **Calisma:** Servo ile direk yukari acilir -> kanca tele tutunur -> robot kayarak iner
- Robot agirligi ~700g, zipline teli uzerinde rahatca kayabilir

### Tahmini Agirlik Tablosu (Robot)
| Bilesen | Agirlik |
|---------|---------|
| 4x Blue TT Motor 1:48 | ~120g |
| 3x MG996R Servo (taban + omuz + zipline) | ~165g |
| 2x MG90S Servo (dirsek + gripper) | ~28g |
| 2x TB6612FNG Motor Surucu | ~6g |
| Deneyap Kart 1A | ~25g |
| Li-Po Pil (1500mAh 2S) | ~85g |
| Sase + tekerlekler (80mm) | ~160-200g |
| Zipline mekanizmasi (direk + kanca) | ~80-100g |
| Kablolar, vidalar, diger | ~50g |
| **Toplam (tahmini)** | **~720-780g** |

### Kumanda Tarafi
| Bilesen | Adet | Aciklama |
|---------|------|----------|
| Deneyap Kart Mini | 1 | Kumanda islem karti |
| Joystick modulu | 2 | X-Y analog eksen (hareket + kol) |
| Buton | 4 | Tutucu, hiz modu, zipline tetik, acil durdurma |
| Li-Po Pil (3.7V) | 1 | Kumanda gucu |

## Yazilim Mimarisi

### Klasor Yapisi
```
circuitbreakers1/
  robot/
    robot.ino              # Ana robot kodu (alici)
    motor_control.h        # DC motor surucu fonksiyonlari (TB6612FNG)
    motor_control.cpp
    arm_control.h          # Robotik kol servo fonksiyonlari (4 DOF)
    arm_control.cpp
    zipline_control.h      # Zipline mekanizmasi kontrolu
    zipline_control.cpp
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
  dokumantasyon/
    TEKNOFEST_Robolig_2026_Sartname_TR_v1_16.02.2026_cl2A6.pdf
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
  uint8_t buttons;     // Bit alani: tutucu, hiz, zipline, durdurma
  uint8_t speed_mode;  // 0: yavas, 1: normal, 2: hizli
} ControlPacket;
// buttons bit alani:
//   bit 0: tutucu ac/kapa (toggle)
//   bit 1: hiz modu degistir
//   bit 2: zipline mekanizmasi tetikle
//   bit 3: ACIL DURDURMA
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

1. **Robot firmware** (`robot/robot.ino`): ESP-NOW uzerinden komut alan, 4 motoru, robotik kolu ve zipline mekanizmasini kontrol eden yazilim
2. **Kumanda firmware** (`kumanda/kumanda.ino`): Joystick/buton okuyan ve ESP-NOW ile robota gonderen yazilim
3. **Dokumantasyon** (`dokumantasyon/`): Pin baglanti semalari, kablolama talimatlari, yarisma sartnamesi
4. **Calisir robot sistemi:** Kumandayla gercek zamanli kontrol edilen 4WD robot + robotik kol + zipline mekanizmasi

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
- Kol, 9x9x9cm koli ve 11cm capindaki halkayi tutabilecek adaptive gripper'a sahip olmali
- Kol erisilebilir yukseklik: yerden ~36cm (4 koli ust uste) ve ~30cm (enerji kulesi)

### Zipline Mekanizmasi
- Zipline servo ve direk `config.h` icinde acik/kapali aci degerleriyle tanimlanir
- Zipline tetikleme kumandadan buton ile yapilir (tek buton: ac/kapat toggle)
- Mekanizma acilmadan once robot hareket halinde OLMAMALI (guvenlik)
- Kanca/makara tele tutunduktan sonra surus motorlari devre disi birakilir

### Guvenlik
- Kumanda sinyali kesilirse robot otomatik durur (failsafe)
- Motor PWM degerleri `config.h` icinde tanimli maksimum siniri asmaz
- Servo acilari fiziksel sinirlar disina cikmaz
- Li-Po pil voltaj kontrolu yapilir (dusuk voltajda uyari)
- Robot uzerinde fiziksel ACIL DURDURMA butonu bulunmali (sartname zorunlu)
- Tum guc hatlari sigorta/akim sinirlamasi ile korumali (sartname zorunlu)
- Acikta kablo olmayacak, tum kablolar yalitimli (sartname zorunlu)
- Pil darbe ve siviya karsi korunakli bolmede (sartname zorunlu)

### Kod Stili
- Girinti: 2 bosluk
- Suslu parantez: ayni satirda acilir
- Header dosyalarinda include guard kullanilir (`#ifndef`)
- Global degiskenlerden kacinilir; gerektiginde `static` veya namespace kullanilir
- `Serial.begin(115200)` debug icin kullanilir; uretim kodunda `#ifdef DEBUG` ile korunur

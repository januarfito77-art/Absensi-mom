# 📡 Sistem Absensi Sidik Jari IoT dengan ESP32-S3

Sistem absensi cerdas berbasis Internet of Things (IoT) menggunakan mikrokontroler ESP32-S3. Alat ini mengintegrasikan pemindai sidik jari dengan penyimpanan ganda (SD Card lokal dan Firebase secara *online*), serta dilengkapi fitur notifikasi *real-time* melalui WhatsApp.



## ✨ Fitur Utama
* **Dual Logging:** Data absensi disimpan secara lokal di SD Card (format CSV) dan dikirim secara *online* ke Firebase Realtime Database.
* **Notifikasi WhatsApp:** Mengirim pesan otomatis ke nomor tujuan melalui Fonnte API setiap kali ada yang melakukan absensi.
* **Visualisasi Interaktif:** Menggunakan layar TFT LCD (ST7789) untuk menampilkan status *standby*, jam *real-time*, sukses/gagal absensi, dan nama pengguna.
* **Sinkronisasi Waktu Akurat:** Dilengkapi modul RTC DS3231 yang disinkronkan dengan NTP Server (saat terhubung WiFi).
* **Remote Management:** Pendaftaran dan penghapusan sidik jari dapat dikontrol melalui perintah dari Firebase.

## 🛠️ Perangkat Keras (Hardware)
* Mikrokontroler: ESP32-S3 (Board: Bos Kecil / setara)
* Sensor Sidik Jari: Optical Fingerprint Sensor (via UART)
* Layar: TFT LCD ST7789 (Komunikasi SPI)
* Modul Waktu: RTC DS3231 (Komunikasi I2C)
* Penyimpanan: MicroSD Card Module (Komunikasi SPI)
* Indikator: 2x LED (Status WiFi & Status Sukses)

## 📌 Konfigurasi Pin (Pinout)
| Komponen | Pin ESP32-S3 | Keterangan |
| :--- | :--- | :--- |
| **Layar TFT (ST7789)** | `CS: 21`, `RST: 48`, `DC: 47`, `MOSI/SDA: 6`, `SCLK/SCL: 7` | Software SPI |
| **MicroSD Card** | `CS: 10`, `MOSI: 11`, `MISO: 13`, `SCK: 12` | Hardware SPI |
| **Sensor Sidik Jari** | `RX: 18`, `TX: 17` | UART (Serial 1) |
| **RTC DS3231** | `SDA: 8`, `SCL: 9` | I2C |
| **LED Indikator** | `WIFI: 4`, `SUKSES: 5` | Output Digital |

## 💻 Library yang Dibutuhkan
Pastikan Anda sudah menginstal *library* berikut di Arduino IDE:
* `WiFi.h`, `HTTPClient.h`, `SPI.h`, `Wire.h`, `SD.h`, `FS.h` (Bawaan ESP32 Core)
* [Adafruit Fingerprint Sensor Library](https://github.com/adafruit/Adafruit-Fingerprint-Sensor-Library)
* [Adafruit GFX Library](https://github.com/adafruit/Adafruit-GFX-Library)
* [Adafruit ST7789 Library](https://github.com/adafruit/Adafruit-ST7735-Library)
* [RTClib](https://github.com/adafruit/RTClib) (Untuk RTC DS3231)
* [ArduinoJson](https://arduinojson.org/) (Untuk parsing data Firebase/Fonnte)

## 🚀 Cara Penggunaan & Instalasi
1. **Clone repositori ini:**
   ```bash
   git clone [https://github.com/UsernameAnda/NamaRepositoriAnda.git](https://github.com/UsernameAnda/NamaRepositoriAnda.git)

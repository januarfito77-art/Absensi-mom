# 📡 Smart Attendance System IoT (ESP32-S3 + Firebase)

![Status Project](https://img.shields.io/badge/Status-Active-success) ![Platform](https://img.shields.io/badge/Platform-ESP32-blue) ![License](https://img.shields.io/badge/License-MIT-green)

**Sistem Absensi Cerdas** berbasis Internet of Things (IoT) yang mengintegrasikan sensor sidik jari, penyimpanan ganda (SD Card & Firebase), dan notifikasi WhatsApp otomatis. Alat ini dirancang untuk mempermudah monitoring kehadiran secara *real-time* dan transparan.



## ✨ Fitur Utama

* **👆 Biometrik Presisi:** Menggunakan sensor sidik jari optik untuk identifikasi cepat.
* **💾 Dual Logging System:**
    * **Offline:** Menyimpan data CSV di MicroSD Card (aman saat internet mati).
    * **Online:** Sinkronisasi *real-time* ke Firebase Realtime Database.
* **📱 Notifikasi WhatsApp:** Mengirim pesan otomatis ke admin/orang tua saat absensi berhasil (via Fonnte API).
* **🖥️ Antarmuka Interaktif:** Layar TFT ST7789 menampilkan Jam, Tanggal, Nama, dan Status (Tepat Waktu/Terlambat).
* **⏰ Waktu Akurat:** Menggunakan RTC DS3231 yang disinkronkan otomatis dengan NTP Server.
* **☁️ Kontrol Jarak Jauh:** Pendaftaran (Enroll) dan Penghapusan data sidik jari dikendalikan melalui perintah web/database.

---

## 🛠️ Komponen & Skema Rangkaian

Berikut adalah daftar komponen dan koneksi pin ke **ESP32-S3 (Board: Bos Kecil / DevKit V1)**:

| Komponen | Pin ESP32 | Protokol | Catatan |
| :--- | :--- | :--- | :--- |
| **TFT LCD ST7789** | `CS:21`, `RST:48`, `DC:47`, `MOSI:6`, `SCK:7` | SPI (SW) | *Cek tegangan (biasanya 3.3V)* |
| **MicroSD Module** | `CS:10`, `MOSI:11`, `MISO:13`, `SCK:12` | SPI (HW) | *Format kartu ke FAT32* |
| **Fingerprint Sensor** | `RX:18`, `TX:17` | UART | *TX Sensor ke RX ESP, RX Sensor ke TX ESP* |
| **RTC DS3231** | `SDA:8`, `SCL:9` | I2C | *Baterai CMOS wajib terpasang* |
| **LED WiFi** | `GPIO 4` | Output | *Indikator koneksi internet* |
| **LED Sukses** | `GPIO 5` | Output | *Indikator absensi berhasil* |

---

## ⚙️ Instalasi & Konfigurasi

### 1. Persiapan Software
Pastikan Anda telah menginstal **Arduino IDE** dan library berikut:
* `Adafruit Fingerprint Sensor Library`
* `Adafruit GFX Library` & `Adafruit ST7789 Library`
* `RTClib` (by Adafruit)
* `ArduinoJson` (by Benoit Blanchon)
* `WiFi`, `HTTPClient`, `SPI`, `SD`, `Wire` (Bawaan ESP32)

### 2. Konfigurasi Kredensial
Buka file `.ino` dan sesuaikan bagian ini dengan data Anda:

```cpp
// Konfigurasi WiFi
#define WIFI_SSID "Nama_WiFi_Anda"
#define WIFI_PASSWORD "Password_WiFi_Anda"

// Konfigurasi Firebase (Realtime Database)
#define DATABASE_URL "[https://project-id-default-rtdb.firebaseio.com](https://project-id-default-rtdb.firebaseio.com)"
#define DATABASE_SECRET "Kode_Rahasia_Database_Anda"

// Konfigurasi WhatsApp (Fonnte)
#define FONNTE_TOKEN "Token_API_Fonnte_Anda" 
#define NOMOR_TUJUAN "08xxxxxxxxxx"

3. Setup Firebase
Buat database di Firebase dan pastikan strukturnya siap menerima data. Aturan (Rules) database sebaiknya diatur agar bisa dibaca/tulis oleh alat (atau gunakan Auth Secret seperti di kode).



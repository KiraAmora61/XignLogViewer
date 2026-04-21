# XIGNCODE Log Viewer v1.0

<div align="center">

## xigncode.log Dosyası Analiz Programı

**ChecLxhc → Checksum XOR Şifre Çözme Özellikli**

[![C++](https://img.shields.io/badge/C++-20-blue.svg)](https://en.cppreference.com/w/cpp/20)
[![ImGui](https://img.shields.io/badge/ImGui-1.90.6-brightgreen.svg)](https://github.com/ocornut/imgui)
[![Platform](https://img.shields.io/badge/Platform-Windows_x64-orange.svg)](https://microsoft.com/windows)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

</div>

---

## 📋 Bu Program Ne Yapar?

XIGNCODE anti-cheat sisteminin oluşturduğu `xigncode.log` dosyasını açar, içindeki şifreli verileri çözer ve size anlaşılır şekilde gösterir.

**Öne Çıkan Özellik:** `ChecLxhc` string'ini `Checksum` olarak çözen XOR şifre çözme algoritması.

---

## ✨ Özellikler

### 📁 Dosya Analizi
- **283,200 byte** log dosyasını blok blok analiz eder
- **885 blok × 320 byte** yapısını parçalar
- Her blok `mLxz4.R#` veya `mLxz4.O#` magic header ile başlar

### ⏰ Timestamp Çıkarma
- **9,771 adet** timestamp çıkarır
- Tarih aralığı: **2019-2038**
- Son 7 günden **6,016 timestamp**

### 🔐 String Şifre Çözme
- XOR şifreleme ile `"XIGNCODE"` anahtarı kullanarak string'leri çözer
- **8,471 toplam**, **4,184 benzersiz** string
- UTF-16LE encoded string'leri okur (`kernel32.dll` vb.)

### 🎯 Checksum Analizi
```
ChecLxhc XOR Key = Checksum
XOR Key: 00 00 00 00 27 0b 1d 0e
```

| Karakter | XOR | Sonuç |
|----------|-----|-------|
| C | 0x00 | C |
| h | 0x00 | h |
| e | 0x00 | e |
| c | 0x00 | c |
| L | 0x27 | k |
| x | 0x0b | s |
| h | 0x1d | u |
| c | 0x0e | m |

### 🖥️ GUI Arayüz
- ImGui tabanlı modern Windows arayüzü
- Direct3D 11 rendering
- Tab-based navigasyon
- String arama özelliği
- Detaylı blok görüntüleme

---

## 📊 Dosya Yapısı

```
┌─────────────────────────────────────────┐
│  Magic Header (8 bytes)                 │
│  mLxz4.R# veya mLxz4.O#                 │
├─────────────────────────────────────────┤
│  Reserved (24 bytes)                    │
├─────────────────────────────────────────┤
│  Data (288 bytes)                       │
│  - Timestamp'ler (DWORD)                │
│  - Şifreli string'ler                   │
│  - Diğer veriler                        │
└─────────────────────────────────────────┘
Toplam: 320 bytes (0x140)
```

Bu yapı **885** kere tekrarlanır.

---

## 🚀 Kullanım

### Console Uygulaması

```
XignLogViewer.exe
```

1. Program otomatik olarak `xigncode.log` dosyasını arar
2. Menüden istediğiniz işlemi seçin:

| Seçim | İşlem |
|-------|-------|
| **1** | Özet bilgileri görüntüle |
| **2** | İlk 30 log girdisini görüntüle |
| **3** | Tüm timestamp'ları görüntüle |
| **4** | Checksum analizi (ChecLxhc → Checksum) |
| **5** | Çözülmüş dosyayı kaydet |
| **6** | Çıkış |

### GUI Uygulaması

```
XignLogViewerGUI.exe
```

1. **"Open Log File"** butonuna tıklayarak `xigncode.log` dosyasını seçin
2. Tab'ler arası geçiş yapın:

| Tab | Açıklama |
|-----|----------|
| **Summary** | Dosya bilgileri, timestamp aralığı, checksum çözümü |
| **Blocks** | Tüm blokları görüntüle, detaylı inceleme |
| **Checksums** | Checksum içeren blokları listele |
| **Search** | String içinde arama yap |

---

## 🛠️ Teknik Bilgiler

| Özellik | Değer |
|---------|-------|
| **Programlama Dili** | C++20 |
| **GUI Framework** | ImGui v1.90.6 |
| **Rendering** | Direct3D 11 |
| **Platform** | Windows x64 |
| **Derleyici** | MSVC 2026 (v143) |
| **Subsystem** | Windows (GUI) / Console |

---

## 📈 Analiz Sonuçları

```
En Eski Timestamp:    2019-12-24
En Yeni Timestamp:    2038-01-18
Son 7 Gün Timestamp:  6,016 adet
Checksum Bulunan:     23 blok
UTF-16LE String:      kernel32.dll, ChecLxhc vb.
Toplam Blok:          885
Toplam Timestamp:     9,771
Toplam String:        8,471 (4,184 benzersiz)
```

---

## 📝 Önemli Notlar

> ⚠️ **Tam şifre çözme** için `.xem` dosyalarının reverse engineering edilmesi gerekir.

- XOR `"XIGNCODE"` anahtarı **kısmi çözümleme** sağlar
- Checksum XOR key'i **tam çözüm** sağlar: `00 00 00 00 27 0b 1d 0e`
- Dosya sonunda **plaintext metadata** bulunur (UTF-16LE)
- Bu program eğitim ve analiz amaçlıdır

---

## 🔗 İndirme

| Versiyon | Link |
|----------|------|
| **Console** | [XignLogViewer.exe](bin/x64/Release/XignLogViewer.exe) |

</div>

# auti-career-match2

## Konsep Aplikasi
Aplikasi ini membantu murid autisme menjawab soalan psikometrik minat kerjaya menggunakan **visual**, **audio**, dan **interaksi tanpa sentuhan** melalui kamera.

### Objektif
- Menilai kecenderungan minat kerjaya murid secara mesra-neurodiversiti.
- Kurangkan beban membaca dengan elemen gambar, ikon, dan suara.
- Benarkan murid menjawab menggunakan pergerakan kepala:
  - **Angguk (YES)**
  - **Geleng (NO)**
- Memetakan hasil kepada **Teori Kecerdasan Pelbagai Gardner**.

---

## Ciri Teras (MVP)

### 1) Soalan Psikometrik Berasaskan Gardner
Gunakan 8 domain kecerdasan:
1. Linguistik
2. Logik-Matematik
3. Visual-Ruang
4. Kinestetik
5. Muzik
6. Interpersonal
7. Intrapersonal
8. Naturalis

Setiap soalan dipaparkan dalam format:
- Teks ringkas (1 ayat sahaja)
- Ilustrasi/ikon aktiviti
- Audio bacaan automatik (BM)
- Butang besar: YES / NO (fallback jika kamera gagal)

### 2) Input Kamera (Head Gesture Detection)
- Aktifkan webcam dengan kebenaran pengguna.
- Jejak titik muka (face landmarks).
- Pengesanan:
  - **Nod/angguk** = YES
  - **Shake/geleng** = NO
- Tunjuk indikator masa nyata: `Mengesan...`, `YES dikesan`, `NO dikesan`.
- Simpan jawapan hanya selepas gesture stabil (contoh: 0.8–1.2 saat).

### 3) Mod Sensori Mesra Autisme
- Tema kontras lembut (kurang overstimulus).
- Satu soalan satu skrin.
- Transisi perlahan, tiada animasi berkelip.
- Kawalan volume audio.
- Butang `Ulang Audio` dan `Jeda`.

### 4) Keputusan & Cadangan Kerjaya
- Kira skor setiap domain Gardner.
- Papar 3 domain tertinggi.
- Peta domain → cadangan kerjaya awal (contoh):
  - Visual-Ruang → grafik, reka bentuk, CAD asas
  - Naturalis → nurseri, pertanian bandar, penjagaan haiwan
  - Kinestetik → teknikal tangan, kerja bengkel, logistik
- Papar dalam bentuk kad visual + audio ringkas.

---

## Cadangan Seni Bina Teknikal

### Frontend
- **React + Vite** (UI responsif dan pantas)
- **Tailwind CSS** (komponen mesra visual)
- **Web Speech API** / TTS enjin tempatan untuk audio soalan

### Kamera & Pengesanan Pergerakan
Pilihan praktikal:
- **MediaPipe Face Landmarker** (disyorkan)
- atau **TensorFlow.js Face Landmarks Detection**

Aliran logik ringkas:
1. Baca koordinat hidung + orientasi kepala setiap frame.
2. Simpan buffer 1–2 saat.
3. Jika pola menegak dominan → YES.
4. Jika pola mendatar dominan → NO.
5. Tapis noise dengan ambang minima pergerakan.

### Backend
- **Node.js (Express/Fastify)**
- API untuk:
  - set sesi murid
  - simpan jawapan
  - kira skor Gardner
  - jana ringkasan laporan

### Data
Contoh struktur item soalan:
```json
{
  "id": "G-VIS-01",
  "domain": "visual_spatial",
  "text_ms": "Saya suka menyusun blok atau puzzle.",
  "audio_url": "/audio/G-VIS-01.mp3",
  "image_url": "/images/puzzle.png",
  "expected_scale": "binary_yes_no"
}
```

---

## Skema Pemarkahan (Cadangan)
- YES = 1, NO = 0
- 10 item per domain (jumlah 80 item)
- Skor domain = jumlah YES domain / 10 × 100
- Ranking domain tertinggi untuk cadangan kerjaya

> Nota: Ini ialah instrumen saringan minat kerjaya, bukan diagnosis klinikal.

---

## Aliran Pengguna
1. Guru/penjaga pilih profil murid.
2. Sistem kalibrasi kamera 5–10 saat.
3. Murid jawab item satu-persatu (audio + visual).
4. Sistem kesan angguk/geleng dan sahkan jawapan.
5. Selesai sesi → dashboard keputusan Gardner + cadangan kerja.
6. Muat turun laporan PDF untuk guru/ibu bapa.

---

## Pelan Fasa Pembangunan

### Fasa 1: Prototype Interaksi
- UI 5–10 soalan contoh
- Audio BM
- Gesture detection asas YES/NO

### Fasa 2: Engine Psikometrik
- Bank item penuh berasaskan Gardner
- Pemarkahan automatik
- Paparan profil kecerdasan

### Fasa 3: Modul Kerjaya
- Pemetaan kecerdasan → kategori kerjaya
- Laporan guru + cadangan aktiviti intervensi

### Fasa 4: Pengesahan Lapangan
- Ujian dengan murid sebenar (bersama pakar pendidikan khas)
- Semak kebolehgunaan, sensitiviti sensor, dan bias item

---

## Keperluan Etika & Privasi
- Dapatkan persetujuan ibu bapa/penjaga sebelum guna kamera.
- Simpan data minimum (principle of least data).
- Enkripsi data murid ketika simpan/transit.
- Benarkan mod tanpa rakaman video (proses masa nyata sahaja).
- Patuh garis panduan PDPA (Malaysia).

---

## Cadangan Seterusnya
Jika anda setuju, langkah seterusnya ialah saya boleh bantu bina:
1. senarai 80 item soalan Gardner dalam Bahasa Melayu (mesra murid autisme),
2. rubrik pemarkahan,
3. prototaip skrin React untuk soalan + kamera,
4. pseudo-code pengesanan angguk/geleng.

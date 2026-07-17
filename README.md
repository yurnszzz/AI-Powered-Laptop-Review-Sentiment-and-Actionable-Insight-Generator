<div align="center">

<!-- Animated Header -->
<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=11,22,44&height=250&section=header&text=Tech-Audit%20AI&fontSize=70&fontAlignY=35&desc=Laptop%20Review%20Sentiment%20and%20Hidden%20Insight%20Analyzer&descSize=20&descAlignY=55&animation=twinkling&fontColor=ffffff" width="100%"/>

<br/>

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Langflow](https://img.shields.io/badge/Langflow-1.10+-FF4B4B?style=for-the-badge&logo=stream&logoColor=white)](https://github.com/langflow-ai/langflow)
[![Gemini API](https://img.shields.io/badge/Gemini--API-3.5--Flash-4285F4?style=for-the-badge&logo=google-gemini&logoColor=white)](https://ai.google.dev/)
[![IBM SkillsBuild](https://img.shields.io/badge/IBM%20SkillsBuild-University%20Education-blue?style=for-the-badge&logo=ibm&logoColor=white)](https://skillsbuild.org/)
[![Hacktiv8](https://img.shields.io/badge/Hacktiv8-Short%20Course-red?style=for-the-badge)](https://www.hacktiv8.com/)

<br/>

<img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=20&duration=3000&pause=1000&color=3498DB&center=true&vCenter=true&multiline=true&repeat=true&width=600&height=80&lines=Powered+by+Langflow+%26+Gemini+3.5+Flash;Bilateral+Action+Items+Extraction;Automated+Hidden+Insights+Discovery" alt="Typing SVG" />

</div>

---

## 📌 Deskripsi Proyek

**Tech-Audit AI** adalah AI Agent berbasis arsitektur *chaining* (perantaian model) yang dirancang untuk bertindak sebagai **Senior Data Analyst** bagi tim e-commerce dan vendor laptop. Sistem ini mampu mengklasifikasikan sentimen pelanggan (Positive, Neutral, Negative), membuat ringkasan naratif tanpa bullet point mengenai 4 aspek utama laptop, merumuskan rekomendasi aksi taktis (Action Items) bagi tim operasional toko dan tim evaluasi produk/vendor, serta mendeteksi celah tersembunyi (*hidden insights*) yang berpotensi merugikan bisnis.

### Mengapa Proyek Ini Dibuat?

Proses analisis ulasan pelanggan pada e-commerce seringkali tidak efisien:

- ❌ Ribuan ulasan pelanggan menumpuk tanpa sempat dibaca secara mendetail.
- ❌ Rekomendasi perbaikan operasional toko dan kontrol kualitas produk pabrik seringkali tercampur aduk.
- ❌ Celah keluhan kecil (misalnya masalah port USB atau warna tombol) sering terabaikan karena rating keseluruhan tinggi.
- ❌ API LLM sering mengalami overload atau timeout jika harus memproses data kotor yang terlalu besar.

**Solusi:** AI Agent dua tahap (dual-stage chaining) di Langflow yang otomatis memproses data ulasan yang telah dibersihkan, mengekstraksi sentimen/aspek ulasan, dan merumuskan langkah taktis bisnis secara otomatis untuk masing-masing pemangku kepentingan.

---

## 👤 Author

| Nama | Institusi |
|------|-----------|
| **Hasan Shofiyyur Rahman** | Mahasiswa Sistem Informasi, UPN Veteran Jakarta |

> **Konteks:** Capstone Project dari program *short course* **"Build an AI Agent"** yang diselenggarakan oleh **IBM SkillsBuild University Education** berkolaborasi dengan **Hacktiv8**.

---

## 🏗️ Alur Arsitektur & Pipeline (Langflow Chaining)

Proyek ini dibangun secara visual menggunakan **Langflow** dengan alur *sequential chaining* (perantaian berurutan):

```
📄 File (CSV Upload: laptop_online_review_sample.csv)
      ↓
📝 Prompt Template 1 (Role: Senior Data Analyst - Ringkasan Naratif & Sentimen)
      ↓
🧠 Language Model 1 (Google Gemini 3.5 Flash - Temp: 0.1)
      ↓
📝 Prompt Template 2 (Role: Senior Data Analyst - Bilateral Action Items & Hidden Insights)
      ↓
🧠 Language Model 2 (Google Gemini 3.5 Flash - Temp: 0.1)
      ↓
💬 Chat Output (Hasil Rekomendasi Terstruktur & Sentimen)
```

---

## 🛠️ Tech Stack

| Teknologi | Kegunaan |
|-----------|----------|
| **Langflow v1.10.0** | Platform visual untuk membangun dan menguji alur AI Agent |
| **Google Gemini 3.5 Flash** | Large Language Model (LLM) untuk pemrosesan teks analitis |
| **Google Gemini API** | API Key untuk mengakses model Gemini secara cloud |
| **Python** | Bahasa dasar untuk data cleaning, profiling, dan sampling dataset |

---

## 🌟 Fitur Utama

- 🤖 **Analisis Sentimen Akurat** — Mengklasifikasikan tone ulasan menjadi Positive, Neutral, atau Negative berdasarkan ulasan teks pelanggan.
- 📄 **Ringkasan Aspek Terfokus** — Menyusun ringkasan naratif (tanpa bullet point) pada 4 aspek utama: Performa Mesin, Daya Tahan Baterai, Kualitas Hardware (Layar, Audio, Fisik), dan Respons CS/Garansi.
- 📋 **Bilateral Action Items** — Membagi rekomendasi secara berimbang untuk **Tim Operasional Toko** (kemasan, kecepatan pengiriman, CS) dan **Tim Evaluasi Produk/Vendor** (QC pabrik, baterai, cacat hardware).
- 🔍 **Hidden Insights Discovery** — Menemukan celah keluhan kecil tersembunyi yang berpotensi merugikan bisnis jika diabaikan (misal: keyboard kurang kontras, port USB bermasalah).
- ⚡ **Data Pre-processing Teroptimasi** — Menghapus data noise (ulasan non-laptop) dan melakukan sampling data (154 ulasan bersih) untuk menghindari rate limit API.

---

## 📊 Pre-processing & Pembersihan Data

Sebelum data dimasukkan ke dalam AI Agent, dilakukan proses data profiling dan data cleaning untuk memastikan kualitas analisis.

### Dataset Schema
Dataset asli mengandung kolom berikut:
- `Unnamed: 0` → message_id (index baris)
- `Product_name` → Nama produk laptop beserta spesifikasi fisiknya
- `Review` → Isi teks ulasan dari pelanggan online
- `Rating` → Skala kepuasan numerik pelanggan (1-5)

### Masalah & Langkah Pembersihan:
1. **Identifikasi Noise:** Dari baris ke-157 ke bawah, dataset asli (`laptop_online_review.csv`) tercampur dengan noise berupa ulasan produk non-laptop seperti handphone (Samsung, Realme, Apple), Smart TV, dan kulkas.
2. **Pembersihan Data:** Menghapus seluruh data noise dari baris ke-157 ke bawah agar fokus analisis sentimen laptop tidak terdistorsi.
3. **Data Sampling:** Mengambil sampel sebanyak 154 ulasan laptop yang bersih (`laptop_online_review_sample.csv`) untuk menghindari batas kapasitas (Overload/Timeout) saat melakukan batch request pada API Gemini.

---

## 🧠 Inovasi Prompt Engineering (Nilai Jual Utama)

Proyek ini menggunakan teknik *prompt engineering* tingkat tinggi dengan pembagian dua tahap prompt yang saling terhubung untuk menghasilkan output analitis yang mendalam.

### 1. Prompt Tahap 1: Extraction & Sentiment (Senior Data Analyst)

Prompt ini berfokus untuk mengekstrak 4 aspek laptop dan menentukan sentimen keseluruhan. Model dilarang menggunakan bullet point agar menghasilkan laporan naratif yang mengalir.

```text
Anda adalah seorang Senior Data Analyst. Tugas Anda adalah menganalisis data ulasan produk dari dataset pelanggan pembeli laptop secara online. Sampaikan hasil analisis Anda dengan bahasa yang sangat jelas, sederhana, dan mudah dipahami oleh siapa saja, tanpa menghilangkan bobot profesionalitas.

Anda akan menerima data dengan kolom berikut:
* Unnamed: 0 → message_id
* Product_name → nama produk laptop
* Review → isi ulasan pelanggan
* Rating → rating numerik (1–5)

## Task 1: Ringkasan (Summarization)
Berdasarkan kolom “Review", buatlah ringkasan naratif dalam bentuk paragraf yang mengalir (TIDAK BOLEH MENGGUNAKAN BULLET POINT untuk bagian ringkasan ini). Bahasa harus formal namun disederhanakan agar mudah dicerna. 

Fokuskan ringkasan Anda secara tajam pada 4 aspek utama berikut:
1. Performa Mesin & Spesifikasi: Apakah laptop berjalan lancar atau sering lag?
2. Ketahanan Baterai & Umur Pakai: Bagaimana daya tahan baterai saat digunakan secara intensif?
3. Kualitas Hardware: Evaluasi pada layar (kejernihan, dead pixel), audio (kualitas suara), dan fisik/material body laptop.
4. Garansi & Respons CS: Bagaimana pengalaman pelanggan saat mengklaim garansi atau bertanya kepada Customer Service?

## Task 2: Analisis Sentimen
Tentukan sentimen keseluruhan berdasarkan tone umum pelanggan.
* Positive: Mayoritas ulasan berisi kepuasan, pujian pada performa/hardware.
* Neutral: Ulasan seimbang, informatif, atau sekadar memberikan bintang tanpa keluhan berarti.
* Negative: Ulasan didominasi kekecewaan pada cacat produk, baterai bocor, atau klaim garansi yang dipersulit.

Input Data Review:
{text}

Format Output Wajib:
* summary: Ringkasan naratif dalam paragraf berkelanjutan (sekali lagi, tanpa bullet point).
* sentiment: (Pilih salah satu: Positive / Neutral / Negative).
```

### 2. Prompt Tahap 2: Strategic Advisory & Hidden Insights

Prompt tahap kedua menerima output ringkasan dari model pertama, lalu merumuskan rekomendasi bisnis terpisah untuk tim operasional dan tim produk, serta mencari pola keluhan tersembunyi.

```text
Anda adalah Senior Data Analyst yang sedang memberikan presentasi kepada manajemen. Berdasarkan ringkasan analisis ulasan laptop berikut, buatlah rekomendasi taktis (Action Items) yang terstruktur, tajam, dan menggunakan bahasa yang mudah dipahami. 

Rekomendasi ini harus menyasar dua pihak sekaligus secara berimbang, serta mencoba mengungkap celah masalah yang mungkin tersembunyi dari ulasan.

### Panduan untuk Action Item:
1. Untuk Tim Operasional Toko: Berikan langkah konkret terkait perbaikan keamanan pengemasan (packing), kecepatan pengiriman, dan kemudahan layanan klaim garansi atau respons Customer Service.
2. Untuk Tim Evaluasi Produk/Vendor: Berikan langkah perbaikan terkait kontrol kualitas (QC) pabrik, seperti isu cacat hardware (layar, audio), ketahanan baterai, dan kesesuaian spesifikasi.
3. Hidden Insights (Celah Tersembunyi): Temukan setidaknya satu pola masalah tidak terduga atau celah dari ringkasan yang berpotensi merugikan bisnis jika dibiarkan (misalnya: rating tinggi tapi ada keluhan kecil berulang pada port USB).

### Ringkasan Input:
{summary}

Buat action item yang sangat spesifik, langsung pada intinya (to the point), dan mudah dieksekusi oleh kedua tim tersebut.

## Return Wajib:
* {summary}
* [action_item]
* [sentiment]
```

---

## 📂 Struktur Repositori

```
Tech-Audit AI/
│
├── Sentiment Analysis Laptop Online Review - Hasan.json    # File ekspor Langflow utama
├── Sentiment Analysis (STARTER).json                       # File ekspor Langflow starter pack
│
├── laptop_online_review.csv                                # Dataset mentah (raw)
├── laptop_online_review_sample.csv                         # Dataset bersih & disampling (154 baris)
│
├── .gitignore                                              # Pengaturan Gitignore
├── LICENSE                                                 # Berkas lisensi MIT
└── README.md                                               # Dokumentasi proyek (file ini)
```

---

## ⚙️ Cara Instalasi & Penggunaan

### Prasyarat

Sebelum memulai, pastikan Anda memiliki:
- ✅ Python 3.10 atau versi di atasnya
- ✅ API Key Google Gemini (dapat diperoleh gratis melalui [Google AI Studio](https://aistudio.google.com/))

### Langkah 1 — Instalasi Langflow
Pasang Langflow melalui terminal/command prompt:
```bash
pip install langflow
```

### Langkah 2 — Jalankan Langflow
Jalankan server lokal Langflow dengan perintah:
```bash
langflow run
```
Akses dashboard Langflow melalui browser di alamat default: `http://127.0.0.1:7860`

### Langkah 3 — Import Workflow
1. Di dashboard Langflow, pilih **New Project** → **Upload Flow / Import JSON**.
2. Pilih file **`Sentiment Analysis Laptop Online Review - Hasan.json`** dari repositori ini.
3. Alur pipeline analitis Tech-Audit AI akan otomatis dimuat di workspace Anda.

### Langkah 4 — Masukkan Google Gemini API Key
1. Temukan kedua komponen **Language Model** di dalam workflow.
2. Pada kolom input `api_key`, tempelkan **Google Gemini API Key** milik Anda.

### Langkah 5 — Upload Dataset Bersih
1. Klik pada komponen **Read File** (`File-A3oRD`).
2. Unggah file **`laptop_online_review_sample.csv`** dari folder repositori ini.

### Langkah 6 — Jalankan dan Amati Output
1. Buka fitur **Playground** (Chat Console) di pojok kanan bawah Langflow.
2. Jalankan alur data. Komponen **Chat Output** (`ChatOutput-myyRD`) akan menampilkan:
   - Ringkasan naratif (4 Aspek Laptop).
   - Klasifikasi Sentimen keseluruhan.
   - Rekomendasi taktis (Tim Operasional vs Tim Produk/Vendor).
   - *Hidden Insights* (Celah masalah tersembunyi).

---

## 🔧 Detail Konfigurasi Komponen

### Langflow Components
| Komponen | Tipe | Keterangan |
|----------|------|------------|
| **Read File** | Input | Membaca berkas CSV ulasan laptop |
| **Prompt Template 1** | Prompt | Template tahap pertama untuk ekstraksi aspek dan sentimen |
| **Language Model 1** | Model | Google Gemini 3.5 Flash (temperature: 0.1) untuk analisis aspek |
| **Prompt Template 2** | Prompt | Template tahap kedua untuk merumuskan action items & hidden insights |
| **Language Model 2** | Model | Google Gemini 3.5 Flash (temperature: 0.1) untuk perumusan taktis |
| **Chat Output** | I/O | Menampilkan hasil akhir analisis ke pengguna |

### Parameter Penting
| Parameter | Nilai | Keterangan |
|-----------|-------|------------|
| Temperature | 0.1 | Nilai rendah untuk menjaga jawaban tetap konsisten, akurat, dan tidak berhalusinasi |
| Stream | False | Dinonaktifkan untuk memproses seluruh teks sebelum mengirimkan output final |

---

## 📚 Referensi & Sumber

- **Langflow Documentation:** https://docs.langflow.org
- **Google Gemini API:** https://ai.google.dev
- **IBM SkillsBuild:** https://skillsbuild.org

---

## 📜 Lisensi

Proyek ini dilisensikan di bawah **[MIT License](LICENSE)**.

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=11,22,44&height=120&section=footer&animation=twinkling" width="100%"/>

<br/>

**Designed & Implemented by Hasan Shofiyyur Rahman — Tech-Audit AI 2026**<br/>
*IBM SkillsBuild University Education × Hacktiv8 — Build an AI Agent*

</div>

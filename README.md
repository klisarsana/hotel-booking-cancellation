# **Prediksi Pembatalan Hotel & Optimasi Kebijakan Deposit**

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-Latest-orange)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Wrangling-yellow)
![Status](https://img.shields.io/badge/Status-Completed-success)

## **Deskripsi Proyek**
Proyek ini bertujuan untuk menganalisis data pemesanan hotel dan membangun model *Machine Learning* untuk memprediksi probabilitas pembatalan pesanan (*hotel cancellation*). Tingkat pembatalan yang tinggi berdampak pada kerugian operasional dan hilangnya potensi pendapatan (*opportunity cost*). Melalui proyek ini, dilakukan analisis mendalam terhadap faktor-faktor yang memicu pembatalan seperti *lead time*, tipe deposit, dan musim liburan (*holiday season*). *Output* dari proyek ini berupa **Dynamic Cancellation Policy** yang dirancang untuk mengoptimalkan pendapatan hotel dan meminimalkan tingkat pembatalan.

Proyek ini merupakan bagian dari **Bootcamp Data Science 2026 – Devlaunch**.

---

## **Daftar Isi**
- [Tujuan Proyek (Goals)](#tujuan-proyek-goals)
- [Struktur Direktori](#struktur-direktori)
- [Tech Stack & Library](#tech-stack--library)
- [Instalasi dan Setup](#instalasi-dan-setup)
- [Metodologi Proyek](#metodologi-proyek)
- [Hasil dan Rekomendasi Bisnis](#hasil-dan-rekomendasi-bisnis)
- [Author](#author)

---

## **Tujuan Proyek (Goals)**
1. **Analisis Pola Pembatalan:** Mengidentifikasi pola *lead time* dan *deposit type* yang memicu tingginya angka pembatalan.
2. **Data Preparation:** Membersihkan *missing value* secara khusus pada fitur agen serta mengekstraksi riwayat preferensi kamar tamu.
3. **Predictive Modeling:** Membangun model klasifikasi (Random Forest/Algoritma lainnya) dengan target performa **F1-Score $\ge$ 82%**.
4. **Feature Engineering:** Melakukan ekstraksi fitur tanggal untuk menguji hipotesis lonjakan pembatalan pada musim liburan (*holiday season*).
5. **Actionable Insight:** Merancang **Dynamic Cancellation Policy** sebagai solusi bisnis strategis berdasarkan hasil prediksi model.

---

## **Struktur Direktori**
```text
project-akhir/
│
├── data/
│   ├── raw/                 # Dataset mentah sebelum dibersihkan (contoh: hotels.csv)
│   └── processed/           # Dataset bersih siap pakai (contoh: data_clean.csv)
│
├── notebooks/
│   └── final-project-classification.ipynb  # Notebook utama berisi proses EDA & Modeling
│
├── venv/                    # Virtual Environment Python
├── .gitignore               # Konfigurasi file yang diabaikan oleh Git
├── README.md                # Dokumentasi proyek (File ini)
└── requirements.txt         # Daftar dependency package Python
```

---

## **Tech Stack & Library**
- **Bahasa Pemrograman:** Python 3.8+
- **Data Manipulation:** Pandas, NumPy
- **Data Visualization:** Matplotlib, Seaborn
- **Machine Learning:** Scikit-Learn (Pipeline, ColumnTransformer, RandomForestClassifier)

---

## **Instalasi dan Setup**
Berikut adalah langkah-langkah untuk menjalankan proyek ini di mesin lokal (Local Environment):

1. **Clone repositori**
   ```bash
   git clone <URL_REPOSITORY>
   cd project-akhir
   ```

2. **Buat dan aktifkan Virtual Environment**
   * **Pengguna Windows:**
     ```powershell
     python -m venv venv
     .\venv\Scripts\activate
     ```
   * **Pengguna macOS/Linux:**
     ```bash
     python3 -m venv venv
     source venv/bin/activate
     ```

3. **Instal seluruh *dependencies***
   ```bash
   pip install -r requirements.txt
   ```

4. **Jalankan Jupyter Notebook**
   ```bash
   jupyter notebook
   ```
   Buka file `notebooks/final-project-classification.ipynb` di browser Anda untuk melihat dan mengeksekusi analisis.

---

## **Metodologi Proyek**
1. **Data Understanding:**
   - Memahami distribusi target (`is_canceled`), dengan rasio temuan awal **63% (Tidak Batal) : 37% (Batal)**.
   - Mengidentifikasi anomali, tipe data, dan *missing values*.

2. **Data Cleaning:**
   - Menangani *missing values* pada kolom `agent`, `country`, dan `children`.
   - Menghapus kolom redundan (`company`, `reservation_status`, `reservation_status_date`) untuk mencegah kebocoran data (*data leakage*).
   - Menambahkan kolom fitur baru seperti `room_changed` jika pesanan kamar awal tidak sesuai dengan yang ditetapkan.

3. **Feature Engineering:**
   - **Holiday Season Extraction:** Menambahkan fitur `is_holiday_season` (Bulan Juli, Agustus, Desember). Ditemukan bahwa musim ini menampung **~28%** dari total pesanan, yang kemudian diteliti lebih lanjut dampaknya terhadap persentase pembatalan.

4. **Exploratory Data Analysis (EDA):**
   - Menganalisis korelasi antara *lead time* yang lama dengan kemungkinan pembatalan.
   - Evaluasi efektivitas jenis deposit yang berlaku saat ini (*No Deposit, Non Refund, Refundable*).

5. **Data Preprocessing & Pipeline:**
   - Melakukan *scaling* (StandardScaler) pada data numerik.
   - Melakukan *encoding* (OneHotEncoder) pada data kategorikal dengan bantuan `ColumnTransformer` dan `Pipeline`.

6. **Modeling:**
   - Melatih model klasifikasi (fokus pada metode ensemble seperti **Random Forest**).
   - Mengevaluasi performa menggunakan metrik **Classification Report**, **Confusion Matrix**, dan metrik performa utama dengan target **F1-Score $\ge$ 82%**.

---

## **Hasil dan Rekomendasi Bisnis**
Dari hasil analisis dan model prediksi, dirumuskan strategi **Dynamic Cancellation Policy**:
- **Tier 1 (High Risk / Holiday Season):** Memberlakukan kebijakan *Non-Refundable Deposit* khusus untuk pemesanan pada bulan-bulan padat pengunjung (Juli, Agustus, Desember) guna menjaga *revenue* hotel saat tingkat permintaan tinggi.
- **Tier 2 (Long Lead Time):** Menerapkan aturan deposit bertahap (*Partial Deposit*) untuk tamu yang memesan dari jauh-jauh hari (*lead time* yang panjang), mengingat *lead time* yang tinggi umumnya berbanding lurus dengan probabilitas pembatalan.
- **Intervensi Agen/Channel:** Melakukan pendekatan atau perubahan aturan kerja sama (SLA) terhadap channel distribusi dengan tingkat batal yang sangat tinggi berdasarkan performa historis.

---

## **Author**
**Muchlis Ar Wicaksana**  
Data Scientist | *Bootcamp Data Science 2026 – Devlaunch*

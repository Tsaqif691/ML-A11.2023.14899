# Prediksi Kategori Hari Hujan Berdasarkan Curah Hujan dan Faktor Musiman

## 📘 Deskripsi Proyek

Proyek ini bertujuan untuk membangun model klasifikasi berbasis machine learning guna mengelompokkan jumlah **hari hujan bulanan** ke dalam tiga kategori:

- **Rendah**: ≤ 10 hari hujan per bulan
- **Sedang**: 11–20 hari hujan per bulan
- **Tinggi**: > 20 hari hujan per bulan

Dengan memanfaatkan data curah hujan bulanan dan fitur-fitur musiman lainnya, proyek ini diharapkan dapat memberikan insight serta prediksi yang akurat terhadap pola musim hujan di suatu wilayah.

## 🎯 Tujuan

- Memprediksi kategori jumlah hari hujan per bulan berdasarkan curah hujan dan fitur musiman
- Mengeksplorasi hubungan antara pola musim dan intensitas hujan
- Meningkatkan interpretabilitas model dengan analisis feature importance dan visualisasi data

---

## 📁 Struktur Dataset

Dataset terdiri dari data bulanan selama 3 tahun (2020–2022). Setiap baris mewakili satu bulan dengan atribut sebagai berikut:

| Kolom          | Deskripsi                                         |
|----------------|---------------------------------------------------|
| Bulan          | Nama bulan (Januari - Desember)                  |
| Bulan_Num      | Nomor bulan (1–12)                               |
| Tahun          | Tahun pengamatan (2020–2022)                     |
| Curah_Hujan    | Total curah hujan dalam milimeter (mm) per bulan |
| Hari_Hujan     | Jumlah hari hujan dalam sebulan                  |

### 🔧 Fitur Tambahan (Engineered Features):

| Kolom             | Deskripsi                                                   |
|-------------------|-------------------------------------------------------------|
| Label             | Kategori jumlah hari hujan (`Rendah`, `Sedang`, `Tinggi`)   |
| Kuartal           | Kuartal ke-1 s/d ke-4 berdasarkan nomor bulan               |
| Curah_per_Hari    | Rasio curah hujan dibagi jumlah hari hujan                 |
| sin_bulan         | Transformasi siklikal bulan (sine)                          |
| cos_bulan         | Transformasi siklikal bulan (cosine)                        |
| Musim_*           | Fitur one-hot encoding musim (`Hujan`, `Kemarau`, dll.)     |

---

## 🔍 Eksplorasi Data & Visualisasi

Visualisasi yang digunakan dalam proyek untuk memahami karakteristik dan distribusi data:

- **Distribusi Curah Hujan vs Kategori Hari Hujan** (Boxplot)
- **Distribusi Kategori Hari Hujan** (Countplot)
- **Total Curah Hujan & Hari Hujan per Tahun** (Barplot)
- **Heatmap Korelasi antar Fitur**
- **Feature Importance dari Random Forest**
- **Confusion Matrix**
- **Akurasi K-Fold CV per Fold (Lineplot)**

---

## 🧠 Model & Metodologi

### 1. Preprocessing:
- Transformasi fitur waktu menjadi informasi musiman dan siklikal
- Feature Engineering: `Curah_per_Hari`, `Kuartal`, `sin_bulan`, `cos_bulan`
- One-hot encoding untuk fitur `Musim`

### 2. Algoritma:
- Model utama: **RandomForestClassifier**
- Hyperparameter tuning dengan **GridSearchCV**
- Evaluasi performa menggunakan:
  - **Train-Test Split**
  - **StratifiedKFold Cross Validation (5-fold)**

### 3. Evaluasi:
- **Classification Report**: precision, recall, f1-score
- **Accuracy**: pada data uji dan cross-validation
- **Confusion Matrix**
- **Feature Importance Analysis**

---

## 🧪 Hasil Model

| Evaluasi                  | Nilai                            |
|---------------------------|----------------------------------|
| Akurasi Uji               | ~85% – 94%                       |
| Akurasi Rata-rata CV      | ~88% – 92%                       |
| Parameter Terbaik         | `{'n_estimators': 300, 'max_depth': 10}` |
| Fitur Paling Berpengaruh  | `Curah_Hujan`, `Curah_per_Hari`, `Hari_Hujan`, `Musim_Hujan`, `sin_bulan` |

### Contoh Output Classification Report:

              precision    recall  f1-score   support

      Rendah       1.00      1.00      1.00         2
      Sedang       1.00      1.00      1.00         4
      Tinggi       1.00      1.00      1.00         3

    accuracy                           1.00         9
   macro avg       1.00      1.00      1.00         9
weighted avg       1.00      1.00      1.00         9

Cross-Validation Akurasi:  0.9464
Semua Fold: [0.875      0.85714286 1.         1.         1.        ]

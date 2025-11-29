# KNN Playground – Heart Failure Clinical Records

Repository ini berisi project kecil untuk mencoba memahami bagaimana algoritma **K-Nearest Neighbors (KNN)** bekerja pada data klinis gagal jantung. Tujuan project ini lebih ke eksplorasi proses analisis data dan evaluasi model, bukan untuk membuat model prediksi medis yang siap pakai.

---

## Pendahuluan

Dataset yang digunakan adalah **Heart Failure Clinical Records** yang berisi 299 pasien dengan 13 variabel klinis seperti usia, tekanan darah, ejection fraction, serum creatinine, diabetes, kebiasaan merokok, dan lama follow-up. Target yang diprediksi adalah `DEATH_EVENT` (0 = bertahan hidup, 1 = meninggal).

Project ini mencakup proses lengkap mulai dari pembersihan data, eksplorasi, pemodelan menggunakan KNN, hingga evaluasi dengan 5-Fold Cross Validation.

---

## Alur Analisis

### 1. Load Data
- Dataset dibaca menggunakan pandas.
- Struktur data diperiksa menggunakan `df.info()`.
- Tiga kolom (`age`, `platelets`, `serum_creatinine`) awalnya terbaca sebagai object karena menggunakan koma sebagai desimal.

### 2. Preprocessing
- Mengganti koma menjadi titik pada kolom yang memiliki desimal.
- Mengonversi ketiga kolom tersebut menjadi numerik.
- Memastikan tidak ada missing value setelah proses konversi.
- Dataset siap digunakan untuk modelling.

### 3. Exploratory Data Analysis (EDA)
- Distribusi `DEATH_EVENT` tidak seimbang:
  - 203 pasien bertahan hidup
  - 96 pasien meninggal
- Korelasi fitur penting:
  - `serum_creatinine` memiliki korelasi positif tertinggi terhadap kematian.
  - `time` memiliki korelasi negatif terbesar, artinya semakin panjang follow-up, risiko kematian cenderung lebih rendah.

### 4. Modelling – KNN dengan Pipeline
- Pipeline terdiri dari:
  - `StandardScaler` untuk normalisasi fitur.
  - `KNeighborsClassifier` untuk pemodelan.
- Nilai K yang diuji: `3, 4, 5, 6, 7, 8, 9, 11, 13, 15`.
- Evaluasi dilakukan menggunakan **5-Fold Cross Validation**.

### 5. Hasil Modelling
- Nilai K terbaik adalah **K = 7**.
- Rata-rata akurasi dari cross validation adalah **74.57%**.
- Nilai accuracy antar fold relatif stabil.
- Evaluasi tambahan pada K = 7:
  - Precision cukup baik.
  - Recall rendah karena kelas meninggal jauh lebih sedikit (dataset imbalanced).
  - F1-score mengikuti tren recall yang rendah.

### 6. Insight dan Rekomendasi
- Faktor yang berkaitan dengan risiko kematian: usia, `serum_creatinine`, dan `time`.
- Model dengan K terlalu kecil cenderung overfitting, sementara K besar cenderung terlalu general.
- Disarankan:
  - Menggunakan metode penyeimbangan data seperti oversampling/SMOTE.
  - Menggunakan **Stratified K-Fold**.
  - Mencoba algoritma lain yang lebih cocok untuk data imbalanced.

### 7. Kesimpulan
- KNN dengan parameter terbaik K = 7 menghasilkan akurasi sekitar **74.6%**.
- Precision cukup baik, tetapi recall rendah sehingga model belum optimal untuk mendeteksi pasien berisiko tinggi.
- Dataset yang tidak seimbang berpengaruh signifikan terhadap performa model.
- Project ini berguna sebagai baseline awal untuk memahami alur analisis dan evaluasi model KNN pada data klinis.



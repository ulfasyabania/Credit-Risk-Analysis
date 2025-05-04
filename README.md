# Analisis Risiko Kredit: Proyek Analitik Prediktif di Bidang Keuangan

## 1. Domain Proyek

### Latar Belakang dan Relevansi

Analisis risiko kredit merupakan dasar dalam pengambilan keputusan keuangan. Institusi keuangan perlu menilai kelayakan kredit para peminjam untuk meminimalkan risiko gagal bayar sekaligus menyeimbangkan profitabilitas. Evaluasi risiko yang tidak akurat dapat mengakibatkan kerugian finansial yang signifikan atau peluang pendapatan yang terlewat. Penelitian dalam pemodelan risiko keuangan (misalnya, pedoman Basel III dan studi akademik di *Journal of Finance* dan *Risk Management*) menunjukkan bahwa model berbasis data dapat meningkatkan akurasi prediksi dan membantu mengoptimalkan portofolio kredit.

### Mengapa dan Bagaimana Masalah Harus Diselesaikan

- **Mengapa:**
  - **Mitigasi Risiko:** Penilaian risiko kredit yang akurat membantu bank meminimalkan kerugian terkait gagal bayar.
  - **Kepatuhan Regulasi:** Institusi keuangan harus mematuhi standar manajemen risiko yang ketat (misalnya, regulasi Basel).
  - **Optimasi Profit:** Penilaian risiko yang lebih baik mengarah pada pengambilan keputusan yang lebih baik dalam persetujuan pinjaman dan penetapan suku bunga yang menguntungkan.

- **Bagaimana:**
  - **Pemodelan Berbasis Data:** Memanfaatkan data historis peminjam yang mencakup fitur demografis, keuangan, dan perilaku.
  - **Analitik Prediktif:** Mengimplementasikan model pembelajaran mesin klasifikasi untuk memprediksi gagal bayar, sehingga memungkinkan pengambilan keputusan otomatis dan manajemen risiko yang efisien.

*Referensi: Basel Committee on Banking Supervision (2011); Saunders & Allen (2010), “Credit Risk Management In and Out of the Financial Crisis.”*

---

## 2. Pemahaman Bisnis

### Proses Klarifikasi Masalah

Dalam industri keuangan yang kompetitif, gagal bayar pinjaman merupakan risiko yang signifikan. Metode penilaian kredit tradisional terkadang terlalu kaku atau tertinggal dari perubahan pasar. Analitik data menawarkan kesempatan untuk menilai kembali risiko kredit berdasarkan data multidimensi terkini.

### Pernyataan Masalah

**Tujuan:**  
Membangun model prediktif untuk mengklasifikasikan peminjam sebagai "gagal bayar" atau "tidak gagal bayar" berdasarkan data historis keuangan dan perilaku.

### Tujuan dan Sasaran

- **Tujuan Utama:**  
  Mengembangkan dan memvalidasi model pembelajaran mesin yang secara akurat memprediksi kemungkinan gagal bayar pinjaman.

- **Sasaran yang Dapat Diukur:**  
  - Mencapai Receiver Operating Characteristic – Area Under Curve (ROC-AUC) lebih dari 0.85.
  - Mendapatkan F1-score di atas 0.80 untuk menyeimbangkan presisi dan recall dalam situasi kelas yang tidak seimbang.

### Pernyataan Solusi yang Diusulkan

1. **Pendekatan Dasar: Regresi Logistik**  
   - **Metode:** Mulai dengan model regresi logistik karena kesederhanaan dan kemampuannya untuk diinterpretasi.  
   - **Penyempurnaan:** Mengintegrasikan penalaan hyperparameter (kekuatan regularisasi, pemilihan solver) dan teknik seleksi fitur.  
   - **Evaluasi:** Menggunakan metrik klasifikasi seperti akurasi, presisi, recall, F1-score, dan ROC-AUC.

2. **Metode Ensemble Lanjutan: Random Forest dan XGBoost**  
   - **Metode:** Menggunakan model ensemble untuk menangkap hubungan non-linear yang kompleks antar fitur.  
   - **Penyempurnaan:** Memanfaatkan grid search untuk penalaan hyperparameter (jumlah pohon, kedalaman maksimum, learning rate untuk XGBoost).  
   - **Evaluasi:** Membandingkan efisiensi dan kinerja model dengan basis model dasar, memilih model terbaik berdasarkan hasil cross-validation.

Kedua strategi akan diuji, dan rekomendasi akhir akan didasarkan pada kinerja, interpretabilitas, dan kepatuhan terhadap langkah-langkah mitigasi risiko bisnis.

---

## 3. Pemahaman Data

### Tinjauan Dataset

- **Ukuran:**  
  Dataset ini mencakup lebih dari 5.000 catatan anonim peminjam pinjaman, memastikan bahwa sampel yang digunakan cukup robust secara statistik untuk pemodelan.

- **Kondisi Data:**  
  Dataset ini menyertakan berbagai fitur seperti data demografis peminjam, riwayat keuangan, skor kredit, rincian pekerjaan, dan informasi spesifik mengenai pinjaman.

- **Sumber Data:**  
  [Dataset Analisis Risiko Kredit (Link Unduhan)](https://example.com/credit-risk-dataset)

### Variabel dan Fitur

- **Informasi Demografis:**  
  Usia, jenis kelamin, status pernikahan, wilayah tempat tinggal.

- **Indikator Keuangan:**  
  Pendapatan tahunan, utang yang ada, skor kredit, jumlah pinjaman yang diminta, suku bunga.

- **Riwayat Pekerjaan dan Kredit:**  
  Status pekerjaan, lamanya bekerja di tempat yang sama, jumlah pinjaman sebelumnya, riwayat gagal bayar.

- **Variabel Target:**  
  Gagal bayar pinjaman (biner: 1 untuk gagal bayar, 0 untuk tidak gagal bayar).

### Analisis Data Eksplorasi (EDA)

- **Statistik Deskriptif:**  
  Statistik ringkasan (rata-rata, median, standar deviasi) untuk variabel kontinu.
- **Visualisasi:**  
  - Histogram dan boxplot untuk menggambarkan distribusi fitur serta mendeteksi nilai pencilan.
  - Matriks korelasi untuk mengidentifikasi saling ketergantungan antar variabel.
  - Diagram batang untuk variabel kategorikal guna mengamati ketidakseimbangan.
- **Wawasan Awal:**  
  - Variabel target tidak seimbang dengan jumlah gagal bayar yang lebih sedikit dibandingkan jumlah tidak gagal bayar.  
  - Beberapa fitur, seperti skor kredit dan utang yang ada, menunjukkan potensi prediksi yang kuat untuk gagal bayar.

---

## 4. Persiapan Data

### Pembersihan Data

- **Imputasi Nilai yang Hilang:**  
  - Variabel kontinu: Diimputasi menggunakan nilai median.  
  - Variabel kategorikal: Diimputasi menggunakan modus.
- **Penanganan Pencilan:**  
  - Mengidentifikasi dan menetapkan batas pada nilai ekstrim (misalnya, pendapatan atau utang yang sangat tinggi) guna mengurangi skewness.
- **Konsistensi Data:**  
  - Menstandarkan respons kategorikal (misalnya, pengkodean yang konsisten untuk status pekerjaan).

### Transformasi Data dan Rekayasa Fitur

- **Normalisasi dan Standarisasi:**  
  Men-scaling fitur numerik (misalnya, menggunakan StandardScaler) agar fitur dengan skala lebih besar tidak mendominasi model.
- **Pengkodean Variabel Kategorikal:**  
  Menggunakan one-hot encoding untuk variabel nominal (misalnya, status pernikahan, tipe pekerjaan).
- **Fitur Turunan:**  
  - Menghitung rasio seperti rasio utang terhadap pendapatan atau rasio pinjaman terhadap pendapatan.  
  - Menghasilkan indikator biner (misalnya, “pernah gagal bayar”) yang mungkin lebih baik menangkap profil risiko.

Setiap langkah pembersihan dan transformasi data dicatat menggunakan sel kode di Jupyter Notebook proyek, guna memastikan transparansi dan reproducibility.

---

## 5. Pemodelan

### Gambaran Umum Proses Pemodelan

Tahap pemodelan mengeksplorasi berbagai teknik klasifikasi, mulai dari metode sederhana hingga lanjutan, untuk memprediksi gagal bayar pinjaman. Dua jalur solusi utama dilaksanakan, dimulai dengan model dasar dan diikuti oleh metode ensemble.

#### 5.1 Model Dasar: Regresi Logistik

- **Tujuan:**  
  Menyediakan titik awal yang dapat diinterpretasi untuk memahami kontribusi masing-masing fitur.
- **Parameter:**  
  Parameter regularisasi (penalti L1, L2) disesuaikan untuk mengatasi masalah multikolinearitas.
- **Kelebihan & Kekurangan:**  
  - *Kelebihan:* Mudah diimplementasikan, cepat, dan dapat diinterpretasikan.  
  - *Kekurangan:* Mungkin kesulitan dalam menangani hubungan non-linear dan interaksi kompleks.

#### 5.2 Model Lanjutan: Random Forest dan XGBoost

- **Random Forest:**  
  - *Kelebihan:* Tahan terhadap overfitting, mampu memodelkan interaksi non-linear, dan menyediakan informasi mengenai kepentingan fitur.  
  - *Kekurangan:* Interpretabilitasnya lebih rendah dibandingkan model linear.
- **XGBoost:**  
  - *Kelebihan:* Kinerja tinggi, secara otomatis menangani nilai yang hilang, dan efektif dalam menangkap pola-pola kompleks.  
  - *Kekurangan:* Lebih memerlukan sumber daya dan membutuhkan penyesuaian parameter yang hati-hati.

### Contoh Penalaan Hyperparameter

Berikut adalah contoh potongan kode yang menggunakan grid search untuk model Random Forest:

```python
from sklearn.model_selection import GridSearchCV
from sklearn.ensemble import RandomForestClassifier

# Definisikan parameter grid untuk Random Forest
param_grid = {
    'n_estimators': [100, 200],
    'max_depth': [None, 10, 20],
    'min_samples_split': [2, 5]
}

# Inisialisasi classifier
rf_model = RandomForestClassifier(random_state=42)

# Lakukan grid search dengan validasi silang 5-fold
grid_search = GridSearchCV(estimator=rf_model, param_grid=param_grid, cv=5, scoring='roc_auc')
grid_search.fit(X_train, y_train)

print("Parameter terbaik ditemukan: ", grid_search.best_params_)
```

---

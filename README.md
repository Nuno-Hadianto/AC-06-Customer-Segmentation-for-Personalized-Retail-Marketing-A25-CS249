# AC-06-Customer-Segmentation-for-Personalized-Retail-Marketing-A25-CS249

```markdown
# Segmentasi Pelanggan Menggunakan RFM dan K-Means Clustering

## Pendahuluan
Proyek ini bertujuan untuk melakukan segmentasi pelanggan pada dataset retail online menggunakan
analisis RFM (Recency, Frequency, Monetary) dan algoritma K-Means Clustering. Tujuannya adalah
untuk mengidentifikasi kelompok pelanggan yang berbeda berdasarkan perilaku pembelian mereka,
sehingga perusahaan dapat mengembangkan strategi pemasaran yang lebih personal dan efektif.

## Dataset
Dataset yang digunakan adalah **Online Retail Data Set** yang umumnya tersedia di Kaggle. Dataset ini
berisi transaksi retail dari tanggal 01/12/2010 hingga 09/12/2011 untuk retail online yang berbasis di
Inggris.

## Metodologi
Proyek ini dibagi menjadi beberapa tahapan utama:

### 1. Pemuatan dan Pembersihan Data
*   Memuat dataset dari file CSV (`Online Retail Data Set.csv`).
*   Menangani nilai hilang (`CustomerID` dihapus karena krusial untuk analisis RFM, `Description` diabaikan).
*   Mengubah tipe data `CustomerID` menjadi integer.
*   Membersihkan transaksi yang tidak valid (`Quantity <= 0` dan `UnitPrice <= 0`).
*   Mengubah tipe data `InvoiceDate` menjadi format datetime.

### 2. Perhitungan Nilai RFM
*   Menghitung `TotalPrice` (`Quantity * UnitPrice`) untuk setiap transaksi.
*   Menentukan tanggal referensi (`reference_date`) sebagai satu hari setelah transaksi terakhir dalam dataset.
*   Mengelompokkan data berdasarkan `CustomerID` untuk menghitung:
    *   **Recency**: Hari sejak pembelian terakhir pelanggan.
    *   **Frequency**: Jumlah transaksi unik pelanggan.
    *   **Monetary**: Total pengeluaran pelanggan.

### 3. Normalisasi Data
*   Menggunakan `StandardScaler` dari `sklearn.preprocessing` untuk menormalisasi metrik RFM (`Recency`, `Frequency`, `Monetary
`). Ini penting agar setiap fitur berkontribusi secara proporsional dalam proses clustering.

### 4. Menentukan Jumlah Cluster Optimal (K)
*   **Metode Elbow**: Menganalisis plot _inertia_ terhadap berbagai nilai K untuk mencari 'siku' yang menunjukkan titik optimal.
*   **Analisis Siluet**: Menghitung _silhouette score_ untuk berbagai nilai K untuk mengukur seberapa baik objek dikelompokkan
dalam clusternya sendiri dibandingkan dengan cluster lain.
*   Berdasarkan analisis kedua metode, **K=4** dipilih sebagai jumlah cluster optimal.

### 5. Menerapkan K-Means Clustering
*   Menerapkan algoritma K-Means dengan `n_clusters=4` pada data RFM yang telah dinormalisasi.
*   Menambahkan label cluster (`Cluster`) ke DataFrame RFM asli.

### 6. Visualisasi Hasil Clustering
*   Menghitung rata-rata RFM untuk setiap cluster untuk memahami karakteristiknya.
*   Membuat *scatter plot* 2D (Recency vs Frequency, Recency vs Monetary, Frequency vs Monetary) untuk memvisualisasikan
sebaran cluster.
*   Membuat *scatter plot* 3D untuk melihat ketiga dimensi RFM secara bersamaan.
*   Membuat *heatmap* dari rata-rata RFM per cluster dan *bar chart* distribusi pelanggan per cluster.

### 7. Interpretasi dan Insight Bisnis
*   Setiap cluster dianalisis berdasarkan rata-rata RFM dan diberi nama deskriptif:
    *   **Cluster 0: Loyal Customers** (Recency sedang, Frequency sedang, Monetary sedang)
    *   **Cluster 1: At-Risk** (Recency sangat tinggi, Frequency rendah, Monetary rendah)
    *   **Cluster 2: Best Spenders** (Recency sangat rendah, Frequency sangat tinggi, Monetary sangat tinggi)
    *   **Cluster 3: Big Spenders** (Recency rendah, Frequency tinggi, Monetary sangat tinggi)
*   Diberikan rekomendasi strategi pemasaran yang spesifik untuk setiap segmen pelanggan.
*   **Validasi Cluster Lanjutan**: Melakukan uji ANOVA untuk Recency, Frequency, dan Monetary untuk memvalidasi bahwa
perbedaan rata-rata antar cluster adalah signifikan secara statistik.

## Cara Mereplikasi
Untuk mereplikasi analisis ini, ikuti langkah-langkah berikut:

### Prasyarat
*   Python 3.x
*   Pustaka Python: `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`, `scipy`.

### Instalasi Pustaka
```bash
pip install pandas numpy scikit-learn matplotlib seaborn scipy
```

### Dataset
Unduh dataset `Online Retail Data Set.csv` dari sumber seperti Kaggle dan letakkan di direktori yang sama dengan notebook atau sesuaikan path dalam kode.

### Menjalankan Notebook
1.  Buka lingkungan pengembangan Python Anda (misalnya, Jupyter Notebook, Google Colab).
2.  Unggah atau buka file notebook yang berisi kode ini.
3.  Jalankan setiap sel secara berurutan.

## Hasil dan Rekomendasi
Proyek ini berhasil mengidentifikasi empat segmen pelanggan utama dengan karakteristik yang berbeda. Dengan memahami segmen-segmen ini, bisnis dapat:
*   Mengalokasikan sumber daya pemasaran secara lebih efisien.
*   Merancang kampanye yang ditargetkan untuk setiap kelompok pelanggan.
*   Meningkatkan retensi pelanggan dan nilai seumur hidup pelanggan (CLV).

Rekomendasi strategi pemasaran yang diberikan untuk setiap cluster bertujuan untuk memaksimalkan potensi setiap segmen, mulai dari mempertahankan 'Best Spenders' hingga mereaktivasi 'At-Risk'.

## Kesimpulan
Segmentasi pelanggan menggunakan RFM dan K-Means Clustering adalah alat yang ampuh untuk memahami perilaku pelanggan dan mendorong pertumbuhan bisnis melalui strategi pemasaran yang didukung data.
```

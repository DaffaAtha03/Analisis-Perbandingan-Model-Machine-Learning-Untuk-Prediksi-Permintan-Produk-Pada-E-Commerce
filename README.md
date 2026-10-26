# Analisis Perbandingan Model Machine Learning untuk Prediksi Permintaan Produk pada E-Commerce

Perbandingan tiga algoritma regresi (**Random Forest**, **XGBoost**, dan **Stacking Ensemble**) untuk memprediksi permintaan produk E-Commerce dari data penjualan historis, dengan kerangka kerja **CRISP-DM** dan dasbor analitik interaktif sebagai hasil akhirnya.

> Penelitian ini disusun di Jurusan Informatika, Fakultas Teknologi Industri, Universitas Gunadarma.
> Penulis: **Muhammad Daffa Atha Rizq** · Pembimbing: Dini Triasanti, ST., MMSI.

## Ringkasan

Ketidakpastian permintaan menyebabkan *overstock* (kelebihan persediaan) dan *stockout* (kehabisan stok). Proyek ini membandingkan tiga model Machine Learning untuk memperkirakan permintaan secara lebih akurat, lalu menerapkan model terbaik pada dasbor yang menampilkan tren penjualan, pola musiman, dan performa per toko serta kategori.

**Hasil utama:** XGBoost memberikan performa terbaik pada ketiga metrik (RMSE 0,626; MAE 0,293; R² 0,630).

## Hasil

Evaluasi dilakukan pada data uji berdasarkan urutan waktu.

| No | Model | RMSE | MAE | R² |
|----|-------|------|-----|----|
| 1 | **XGBoost** | **0,626** | **0,293** | **0,630** |
| 2 | Stacking Ensemble | 0,634 | 0,297 | 0,621 |
| 3 | Random Forest | 0,642 | 0,303 | 0,611 |

Catatan interpretasi:
- Selisih antar model kecil. XGBoost unggul tipis tetapi konsisten pada ketiga metrik.
- Stacking Ensemble tidak mengungguli XGBoost tunggal. Penelitian menduga penyebabnya adalah konfigurasi *meta-learner* yang belum optimal serta kompleksitas model yang bertambah tanpa kenaikan akurasi yang sebanding.
- Nilai R² sebesar 0,63 berarti model menjelaskan sebagian, bukan seluruh, variasi penjualan.

## Data

- **Sumber:** dataset publik *Predict Future Sales* dari Kaggle ([halaman kompetisi](https://www.kaggle.com/competitions/competitive-data-science-predict-future-sales)).
- **Cakupan:** penjualan harian Januari 2013 sampai Oktober 2015, yang diagregasi menjadi data **bulanan** (34 bulan) per kombinasi toko, produk, dan periode.
- **Berkas dataset:** transaksi harian, data produk, kategori produk, dan identitas toko.
- **Pembagian data (berurutan waktu):** data latih Januari 2013 sampai September 2015, data uji Oktober 2015.
- **Ukuran data latih:** 2.018.633 baris dan 11 fitur; data validasi 73.185 baris.

> Data mentah **tidak disertakan** di repositori ini. Unduh dari Kaggle dan letakkan di folder `data/`.

## Metodologi (CRISP-DM)

1. **Business Understanding:** perumusan tujuan prediksi permintaan untuk pengelolaan persediaan.
2. **Data Understanding:** eksplorasi awal; ditemukan *outlier* pada harga dan jumlah penjualan, serta entri toko yang terindikasi duplikat.
3. **Data Preparation:**
   - penghapusan harga negatif, volume penjualan tidak realistis, dan duplikat identitas toko;
   - penggabungan data toko dan kategori;
   - agregasi data harian menjadi bulanan per toko-produk;
   - rekayasa fitur: fitur *lag* penjualan, fitur temporal (bulan dan tahun), dan *encoding* variabel kategorikal.
4. **Modeling:** Random Forest Regressor, XGBoost, dan Stacking Ensemble, semuanya dilatih pada dataset latih yang sama agar perbandingan konsisten.
5. **Evaluation:** RMSE, MAE, dan R².
6. **Deployment:** model terbaik dipakai untuk menghasilkan prediksi yang divisualisasikan pada dasbor interaktif.

## Dasbor

Dasbor menyajikan:
- tren penjualan bulanan dibandingkan tren jangka panjang (rata-rata bergerak 6 bulan);
- kinerja penjualan per toko dan per kategori produk;
- *heatmap* penjualan bulanan per tahun;
- siklus hidup 5 produk terlaris.

Temuan dari eksplorasi: pola musiman konsisten dengan puncak pada Desember, tren jangka panjang cenderung menurun dari 2013 ke 2015, dan penjualan terkonsentrasi pada sebagian kecil toko serta kategori (game, film, musik).

<!-- ISI: tambahkan tangkapan layar dasbor, mis. ![Dasbor](docs/dasbor.png) -->

## Teknologi

Python, pandas, scikit-learn, XGBoost.
<!-- ISI: tambahkan pustaka/dasbor yang Anda pakai (mis. matplotlib, seaborn, Streamlit) dan versi Python -->

## Struktur repositori

<!-- ISI: sesuaikan dengan isi repo Anda yang sebenarnya, mis.
.
├── data/               (tidak disertakan; unduh dari Kaggle)
├── notebooks/          notebook analisis dan pemodelan
├── dashboard/          kode dasbor
├── docs/               tangkapan layar dan makalah (PDF)
├── requirements.txt
└── README.md
-->

## Cara menjalankan

<!-- ISI: langkah nyata dari proyek Anda, mis.
1. git clone https://github.com/DaffaAtha03/<nama-repo>.git
2. pip install -r requirements.txt
3. Unduh data dari Kaggle ke folder data/
4. Jalankan notebook / perintah dasbor
-->

## Keterbatasan

- Data berasal dari satu dataset publik (1C Company, 2013 sampai 2015), jadi hasil belum tentu berlaku pada toko atau periode lain.
- Selisih performa antar model kecil, dan *tuning* hiperparameter serta *meta-learner* pada Stacking belum dioptimalkan.
- Evaluasi memakai satu periode uji (Oktober 2015); validasi berulang pada beberapa periode akan lebih kuat.

## Makalah

Naskah lengkap penelitian: *Analisis Perbandingan Model Machine Learning untuk Prediksi Permintaan Produk pada E-Commerce*.
<!-- ISI: tautan ke PDF di repo, mis. [Unduh makalah](docs/makalah.pdf) -->

## Kontak

Muhammad Daffa Atha Rizq · daffathr3@gmail.com · [GitHub](https://github.com/DaffaAtha03) · [Portofolio](https://daffaatha03.github.io/Portofolio-Daffa-Atha/)

---

## English summary

This project compares three regression models (Random Forest, XGBoost, and Stacking Ensemble) for e-commerce demand forecasting under the CRISP-DM framework. Using the public Kaggle *Predict Future Sales* dataset (34 months of aggregated monthly sales), **XGBoost performed best** (RMSE 0.626, MAE 0.293, R² 0.630). The model was applied to an interactive analytics dashboard showing sales trends, seasonality, and store and category performance.

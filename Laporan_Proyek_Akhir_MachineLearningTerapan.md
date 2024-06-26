# Laporan Proyek Machine Learning - Book Recommendation System with Content-Based Filtering

## Project Overview

Dalam era digital yang terus berkembang, di mana akses terhadap berbagai macam bahan bacaan semakin mudah, pembuatan sistem rekomendasi buku menjadi semakin penting. Sistem ini tidak hanya membantu pengguna menavigasi melalui sejumlah besar buku yang tersedia, tetapi juga memungkinkan pengguna menemukan bahan bacaan yang sesuai dengan minat dan preferensi mereka dengan lebih efisien. Dengan menyediakan rekomendasi yang personal dan relevan, sistem rekomendasi buku tidak hanya meningkatkan pengalaman membaca pengguna, tetapi juga memperluas cakupan literasi dan pengetahuan masyarakat secara keseluruhan. Melalui penelitian yang dilakukan oleh berbagai lembaga dan publikasi, telah terbukti bahwa implementasi sistem rekomendasi yang efektif dapat meningkatkan penjualan buku, meningkatkan keterlibatan pengguna, dan mempromosikan diversitas dalam bacaan. Oleh karena itu, proyek ini memiliki dampak yang signifikan dalam meningkatkan akses terhadap informasi, meningkatkan kepuasan pengguna, dan mendukung pertumbuhan industri penerbitan serta literasi masyarakat secara keseluruhan.

## Business Understanding
### Problem Statements
- Bagaimana membantu pengguna menemukan buku yang sesuai dengan minat dan preferensinya di tengah banyaknya pilihan bacaan yang tersedia?

### Goals
- Mengembangkan sistem rekomendasi buku yang efektif untuk membantu pengguna menemukan bahan bacaan yang sesuai dengan minat dan preferensinya dengan lebih mudah.

### Solution Approach
- Content-based filtering

Pendekatan ini akan menggunakan fitur-fitur dari buku itu sendiri, seperti judul, penulis, genre, dan deskripsi, untuk membuat profil pengguna dan buku. Sistem akan merekomendasikan buku yang memiliki fitur serupa dengan buku yang disukai pengguna sebelumnya. Misalnya, jika seorang pengguna menyukai buku dengan genre "fiksi ilmiah" dan penulis "Isaac Asimov", sistem akan merekomendasikan buku-buku dengan genre serupa dan penulis yang mirip.

## Data Understanding
Data yang akan digunakan pada proyek ini adalah dataset Books dataset yang diambil dari Kaggle. Dataset berisi 1000 baris data record tanpa missing values. Terdapat 10 kolom dalam dataset, yaitu index (yang nantinya digunakan sebagai book_id) dengan tipe data integer, title dengan tipe data object, category dengan tipe data object, price dengan tipe data float, price after tax dengan tipe data float, tax amount dengan tipe data float, avilability dengan tipe data integer, number of reviews dengan tipe data integer, book description dengan tipe data object, image link dengan tipe data object, dan stars dengan tipe data integer.

Sumber dataset: https://www.kaggle.com/datasets/jalota/books-dataset

### Statistik Deskriptif Data
|       |     book_id |      Price | Price_After_Tax | Tax_amount | Avilability | Number_of_reviews |       Stars |
|-------|------------:|-----------:|----------------:|-----------:|------------:|------------------:|------------:|
| count | 1000.000000 | 1000.00000 |      1000.00000 |     1000.0 | 1000.000000 |            1000.0 | 1000.000000 |
|  mean |  499.500000 |   35.07035 |        35.07035 |        0.0 |    8.585000 |               0.0 |    2.923000 |
|  std  |  288.819436 |   14.44669 |        14.44669 |        0.0 |    5.654622 |               0.0 |    1.434967 |
|  min  |    0.000000 |   10.00000 |        10.00000 |        0.0 |    1.000000 |               0.0 |    1.000000 |
|  25%  |  249.750000 |   22.10750 |        22.10750 |        0.0 |    3.000000 |               0.0 |    2.000000 |
|  50%  |  499.500000 |   35.98000 |        35.98000 |        0.0 |    7.000000 |               0.0 |    3.000000 |
|  75%  |  749.250000 |   47.45750 |        47.45750 |        0.0 |   14.000000 |               0.0 |    4.000000 |
|  max  |  999.000000 |   59.99000 |        59.99000 |        0.0 |   22.000000 |               0.0 |    5.000000 |

### Variabel/fitur pada Books dataset adalah sebagai berikut:
- Title: judul buku.
- Category: kategori buku.
- Price: harga buku
- Price After tax: harga buku setelah pajak.
- Tax amount: pajak.
- Availability: stok yang tersedia
- Number of reviews: jumlah review.
- Book Description: deskripsi buku.
- Image Link: tautan untuk melihat gambar buku.
- Stars: rating untuk setiap buku dengan nilai 1-5 bintang.

## Data Preparation
1. Penanganan Missing Values:
- Nilai null atau missing values dapat mengganggu konsistensi dan akurasi analisis data. Oleh karena itu, langkah-langkah penanganan nilai null penting untuk memastikan kualitas data sebelum dilakukan pemodelan.
Pada proyek ini, teknik yang digunakan untuk menangani nilai null adalah dengan melakukan penghitungan nilai null untuk setiap kolom dan kemudian mengatasi nilai null tersebut dengan cara yang sesuai, seperti imputasi atau penghapusan baris/kolom.
2. Penghapusan Duplikat (drop_duplicates):
- Duplikasi data bisa menyebabkan bias dalam analisis dan pemodelan. Oleh karena itu, langkah penghapusan duplikat dilakukan untuk memastikan bahwa setiap entitas dalam dataset hanya direpresentasikan sekali, sehingga hasil analisis lebih akurat dan konsisten.
Pada proyek ini, teknik yang digunakan adalah dengan menggunakan metode drop_duplicates() untuk menghapus baris yang memiliki nilai yang sama untuk semua kolom.
3. Konversi Data Series Menjadi List:
- Dalam beberapa kasus, terutama ketika bekerja dengan beberapa metode atau library yang memerlukan input berupa list, mengonversi data series menjadi list diperlukan agar data dapat diproses dengan benar.
- Pada proyek ini, teknik yang digunakan adalah dengan menggunakan metode tolist() untuk mengonversi data series menjadi list pada kolom-kolom tertentu seperti book_id, title, dan category.
4. Pembuatan Dictionary dan DataFrame Baru:
- Membuat dictionary untuk menentukan pasangan key-value pada data book_id, title, dan category memungkinkan representasi yang lebih terstruktur dan mudah dimanipulasi. Selain itu, mengonversi dictionary menjadi dataframe baru memudahkan dalam pemrosesan data dan mempersiapkan data untuk pemodelan.
- Pada proyek ini, teknik yang digunakan adalah dengan membuat dictionary dari data book_id, title, dan category, kemudian mengonversinya menjadi dataframe baru yang akan digunakan dalam pemodelan.

## Modeling
Sistem rekomendasi dengan content-based filtering adalah salah satu pendekatan dalam sistem rekomendasi yang menggunakan fitur-fitur intrinsik dari item yang direkomendasikan untuk membuat rekomendasi kepada pengguna. Dalam konteks pembuatan sistem rekomendasi buku, content-based filtering memanfaatkan atribut-atribut buku seperti judul, penulis, genre, deskripsi, dan fitur lainnya untuk menentukan kesamaan antara buku-buku yang ada dan preferensi pengguna.

### Kelebihan Content-Based Filtering
- Personalisasi yang Tinggi

Content-based filtering memberikan rekomendasi yang sangat personal karena rekomendasi didasarkan pada preferensi individu pengguna dan karakteristik buku yang telah disukai sebelumnya.
- Tidak Memerlukan Data Pengguna Eksternal

Pendekatan ini tidak memerlukan informasi tentang pengguna lain, sehingga tidak perlu mengandalkan data pengguna eksternal seperti data riwayat pembelian atau penilaian pengguna.
- Keterbukaan terhadap Item Baru

Content-based filtering dapat dengan mudah menyesuaikan diri dengan item-item baru yang ditambahkan ke dalam sistem, karena rekomendasi didasarkan pada fitur intrinsik dari item tersebut.
- Mampu Menangani Long Tail

Content-based filtering efektif dalam menangani long tail, yaitu item-item yang kurang populer atau tidak sering dicari oleh pengguna, karena sistem dapat merekomendasikan item berdasarkan kesamaan fitur, bukan popularitasnya.

### Kekurangan Content-Based Filtering
- Keterbatasan dalam Penemuan Item Baru

Content-based filtering cenderung menghasilkan rekomendasi yang kurang variasi karena hanya merekomendasikan item yang memiliki fitur serupa dengan item yang telah disukai pengguna sebelumnya.
- Keterbatasan dalam Menangani Perubahan Preferensi

Pendekatan ini tidak efektif dalam menangani perubahan preferensi pengguna karena rekomendasi hanya didasarkan pada fitur-fitur buku yang telah disukai sebelumnya, tanpa mempertimbangkan perubahan preferensi pengguna.
- Ketergantungan pada Kualitas Ekstraksi Fitur

Kualitas rekomendasi dalam content-based filtering sangat bergantung pada kualitas ekstraksi fitur dari buku. Jika ekstraksi fitur tidak akurat, rekomendasi yang dihasilkan juga tidak akurat.
- Tidak Mampu Menangani Filter Bubble

Content-based filtering cenderung memperkuat filter bubble, yaitu kondisi di mana pengguna hanya menerima rekomendasi yang sesuai dengan preferensi yang sudah ada, tanpa diperkenalkan pada konten yang berbeda atau diversifikasi bacaan.

### Uji Top-n Recommendation
|   |                                             title |              category |
|---|--------------------------------------------------:|----------------------:|
| 0 |                               While You Were Mine |    Historical Fiction |
| 1 |                             The House by the Lake |    Historical Fiction |
| 2 |                            Between Shades of Gray |    Historical Fiction |
| 3 |   World Without End (The Pillars of the Earth #2) |    Historical Fiction |
| 4 |                             Girl in the Blue Coat |    Historical Fiction |
| 5 |                                      Mrs. Houdini |    Historical Fiction |
| 6 | The Guernsey Literary and Potato Peel Pie Society |    Historical Fiction |
| 7 |           A Flight of Arrows (The Pathfinders #2) |    Historical Fiction |
| 8 |                                 The Secret Healer |    Historical Fiction |
| 9 |                         Girl With a Pearl Earring | Historical Fiction    |

## Evaluation
Pada proyek ini, metrik evaluasi yang digunakan adalah precision. Metrik evaluasi "precision" dalam konteks sistem rekomendasi mengukur seberapa banyak item yang direkomendasikan kepada pengguna yang relevan dengan preferensi atau minat mereka. Dalam sistem rekomendasi yang menggunakan content-based filtering, precision akan memberikan gambaran tentang seberapa baik sistem dalam merekomendasikan buku yang sesuai dengan karakteristik atau konten yang disukai pengguna.

Precision mengukur proporsi item yang relevan yang diprediksi secara benar dari semua item yang diprediksi. Dalam sistem rekomendasi, ini berarti menghitung berapa banyak buku yang relevan dengan preferensi pengguna yang direkomendasikan oleh sistem dibandingkan dengan total buku yang direkomendasikan.

Berikut adalah formula dari Recommender System Precision.

$$Precision = \frac{number of recommendation that are relevant}{number of item recommended} x 100%$$

Keterangan:
- number of recommendation that are relevant adalah jumlah item yang relevan yang diprediksi secara benar oleh sistem.
- number of item recommended adalah jumlah item yang direkomendasikan.

Dalam proyek ini, sistem rekomendasi diuji untuk memberikan top 10 rekomendasi buku yang relevan dengan buku yang di-input. Hasilnya menunjukkan semua buku yang direkomendasikan relevan/memiliki kategori yang sama dengan buku yang di-input sehingga dapat dikatakan sistem rekomendasi dalam proyek ini memiliki nilai precision sebesar 100%. Hal ini didapat dari perhitungan jumlah rekomendasi relevan berjumlah 10 dan jumlah rekomendasi berjumlah 10 buah. Artinya perhitungannya menjadi (10/10)x100%. Oleh karena itu, nilai precision dari sistem rekomendasi yang dibuat adalah 100%.

Berdasarkan hasil evaluasi ini, maka dapat disimpulkan bahwa sistem rekomendasi dapat memberikan rekomendasi buku yang relevan untuk membantu pengguna mengeksplorasi dan menemukan buku yang sesuai minat dan preferensinya.

# Laporan Proyek Machine Learning - Azhar Rizki Zulma

## Project Overview
Domain proyek yang dipilih dalam proyek _machine learning_ ini adalah mengenai hiburan dengan judul proyek _"Movie Recommendation System"_.

**Latar Belakang**

Hiburan merupakan kebutuhan terbelakang manusia, mengapa demikian? Karena hiburan bukanlah sebuah kebutuhan pokok yang wajib dipenuhi oleh setiap manusia, begitulah pikir orang terdahulu. Seiring berjalannya waktu orang-orang mulai menganggap hiburan merupakan sebuah kebutuhan yang wajib dipenuhi oleh setiap orang. Terutama semenjak memasuki abad 21, di mana terjadi perkembangan yang pesat pada dunia hiburan. Khususnya pada dunia pertelevisian dan film. Dari era televisi hitam putih, hingga menginjak ke era warna-warni. Bahkan mulai bermunculan televisi hologram dan layanan _streaming_ yang disesuaikan dengan kesukaan pengguna. Penggunaan layanan _streaming_ saat ini meningkat cukup pesat. Dan baru-baru ini pun semakin meningkat akibat pandemi yang berkepanjangan ini.

Dari latar belakang itulah penulis mengambil topik ini sebagai domain proyek _machine learning_ yang penulis kerjakan. Selain dari latar belakang diatas, tujuan lain dibuatnya proyek _machine learning_ ini ialah membuat sebuah model untuk proyek aplikasi yang sedang penulis kembangkan. Diharapkan model ini nantinya akan berguna pada aplikasi yang penulis kembangkan dan mendapatkan hasil keluaran berupa aplikasi yang berkualitas sesuai dengan yang penulis harapkan.

## Business Understanding
Sistem rekomendasi adalah suatu aplikasi yang digunakan untuk memberikan rekomendasi dalam membuat suatu keputusan yang diinginkan pengguna. Untuk meningkatkan _user experience_ dalam menemukan judul film yang menarik dan yang sesuai dengan yang pengguna inginkan, maka sistem rekomendasi adalah pilihan yang tepat untuk diterapkan. Dengan adanya sistem rekomendasi, _user experience_ tentu akan lebih baik karena pengguna bisa mendapatkan rekomendasi judul film yang ingin diharapkan.

### Problem Statement
Berdasarkan pada latar belakang di atas, permasalahan yang dapat diselesaikan pada proyek ini adalah sebagai berikut:
-   Bagaimana cara melakukan pengolahan data yang baik sehingga dapat digunakan untuk membuat model sistem rekomendasi yang baik?
-   Bagaimana cara membangun model _machine learning_ untuk merekomendasikan sebuah film yang mungkin disukai pengguna?

### Goal
Tujuan dibuatnya proyek ini adalah sebagai berikut:
-   Melakukan pengolahan data yang baik agar dapat digunakan dalam membangun model sistem rekomendasi yang baik.
-   Membangun model _machine learning_ untuk merekomendasikan sebuah film yang kemungkinan disukai pengguna.


### Solution
Untuk menyelesaikan masalah ini, penulis akan menggunakan 2 solusi algoritma yaitu _content-based filtering_ dan _collaborative filtering_. Berikut adalah penjelasan teknik-teknik yang akan digunakan untuk masalah ini:
* _Content-Based Filtering_ merupakan cara untuk memberi rekomendasi bedasarkan genre atau fitur pada item yang disukai oleh pengguna. _Content-based filtering_ mempelajari profil minat pengguna baru berdasarkan data dari objek yang telah dinilai pengguna.
* _Collaborative Filtering_ merupakan cara untuk memberi rekomendasi bedasarkan penilaian komunitas pengguna atau biasa disebut dengan *rating*. _Collaborative filtering_ tidak memerlukan atribut untuk setiap itemnya seperti pada sistem berbasis konten.

## Data Understanding

- **Informasi Dataset**
  <br> Dataset yang digunakan pada proyek ini yaitu dataset film lengkap dengan genre dan rating, informasi lebih lanjut mengenai dataset tersebut dapat lihat pada tabel berikut:

  | Jenis                   | Keterangan                                                                              |
  | ----------------------- | --------------------------------------------------------------------------------------- |
  | Sumber                  | Dataset: [Kaggle](https://www.kaggle.com/sunilgautam/movielens) |
  | Dataset Owner           | Sunil Gautam                                                                           |
  | Lisensi                 | -                                                                                       |
  | Kategori                | Movies & TV Shows                                                                     |
  | Usability               | 5.3                                                                                       |
  | Jenis dan Ukuran Berkas | ZIP (3.3 MB)                                                                           |
  | Jumlah File Dataset     | 4 File (CSV)                                                                           |

  <br> Berikut ini file dataset
  * links.csv
  * ratings.csv
  * movies.csv
  * tags.csv

  Pada proyek ini penulis hanya menggunakan 2 file dataset yaitu:
  1. *movies.csv*
      <br> *Jumlah Data 9742, dan memiliki 3 kolom*
      <br> Untuk penjelasan mengenai variabel-variabel pada dataset dapat dilihat pada poin-poin berikut ini:
      * `movieId`: ID dari film
        <br>movieId memiliki 9742 data unik.
      * `title`: Judul dari film
        <br>title memiliki 9737 data unik.
      * `genres`: Genre dari film
        <br>genres memiliki 951 data unik.

  2. *ratings.csv*
      <br> *Jumlah Data 100836, dan memiliki 4 kolom*
      <br> Untuk penjelasan mengenai variabel-variabel pada dataset dapat dilihat pada poin-poin berikut ini:
      * `userId`: ID pengguna pemberi rating
        <br>userId  memiliki 610 data unik.   
      * `movieId`: ID film yang di rating
        <br>movieId memiliki 9724 data unik.
      * `rating`: Rating dari film
        <br>rating memiliki 10 data unik. dengan range 0 - 5 dan skala 0.5
      * `timestamp` = Waktu rating terekam
        <br>timestamp memiliki 85043 data unik.
      
- **Sebaran atau Distribusi Data pada Fitur yang Digunakan**

  Berikut merupakan visualisasi data yang menunjukkan sebaran/distribusi data pada beberapa variabel yang akan penulis gunakan nanti:
  
  Distribusi tahun rilis film:

  ![Distribusi Tahun Rilis](https://github.com/AzharRizky/Movie-Recommendation-System/blob/main/images/tahun_rilis.png?raw=true)

  Dapat dilihat pada grafik di atas rata-rata rilis sebuah film berkisar antara tahun 1990-2000 ke atas, distribusi terbanyak terjadi di atas tahun 2000, di mana distribusi film cenderung mengalami kenaikan secara signifikan setiap berjalannya waktu.

  Distribusi total jumlah genre:

  ![Distribusi Genre](https://raw.githubusercontent.com/AzharRizky/Movie-Recommendation-System/main/images/genre.png)

  Terlihat pada gambar di atas ada 20 kategori atau genre di dalam data ini. genre `Drama` yang paling banyak dan diikuti oleh genre `Comedy` lalu ada beberapa film yang tidak memiliki genre `no genres listed`
  
  10 film yang memiliki _rating_ tertinggi:

  ![Top Rating](https://raw.githubusercontent.com/AzharRizky/Movie-Recommendation-System/main/images/top_ten.png)

  Terlihat pada grafik, bahwa film yang memiliki _rating_ tertinggi adalah **Forrest Gump** yang rilis pada tahun 1994

## Data Preparation
Data preparation diperlukan untuk mempersiapkan data agar ketika nanti dilakukan proses pengembangan model diharapkan akurasi model akan semakin baik dan meminimalisir terjadinya bias pada data. Berikut ini merupakan tahapan-tahapan dalam melakukan pra-pemrosesan data:
 - **Melakukan Penanganan _Missing Value_**
    <br> Penanganan yang penulis lakukan pada _missing value_ yaitu dengan melakukan drop data. Tetapi karena dataset yang digunakan cukup bersih, _missing value_ hanya terdapat ketika proses penggabungan dataset.
 
 - **Melakukan _Sorting_ Data Rating berdasarkan ID Pengguna**
    <br> Melakukan pengurutan data _rating_ berdasarkan ID Pengguna agar mempermudah dalam melakukan penghapusan data duplikat nantinya.

 - **Menghapus Data Duplikat**
    <br> Melakukan penghapusan data duplikat agar tidak terjadi bias pada data nantinya.

 - **Melakukan penggabungan Data**
    <br> Melakukan penggabungan data yang sudah diolah sebelumnya untuk membangun model. lalu menghapus data yang memiliki _missing value_ pada variabel genre dan melihat jumlah data setelah digabungkan, terlihat data memiliki 100830 baris dengan 5 kolom.

## Modeling and Result
Pada proyek ini, Proses modeling dalam proyek ini menggunakan metode *Neural Network* dan *Cosine Similarity*. Model *Deep Learning* akan penulis gunakan untuk Sistem Rekomendasi berbasis `Collaborative Filtering` yang mana model ini akan menghasilkan rekomendasi untuk satu pengguna. *Cosine Similarity* akan penulis gunakan untuk Sistem Rekomendasi berbasis `Content-Based Filtering` yang akan menghitung kemiripan antara satu film dengan lainnya berdasarkan fitur yang terdapat pada satu film. Berikut penjelasan tahapannya:

### Content Based Filtering
Pada modeling `Content Based Filtering`, langkah pertama yang dilakukan ialah penulis menggunakan TF-IDF Vectorizer untuk menemukan representasi fitur penting dari setiap genre film. Fungsi yang penulis gunakan adalah tfidfvectorizer() dari library sklearn. Selanjutnya penulis melakukan fit dan transformasi ke dalam bentuk matriks. Keluarannya adalah matriks berukuran (9737, 23). Nilai 9737 merupakan ukuran data dan 23 merupakan matriks genre film.

Untuk menghitung derajat kesamaan (_similarity degree_) antar movie, penulis menggunakan teknik _cosine similarity_ dengan fungsi _cosine_similarity_ dari _library_ sklearn. Berikut dibawah ini adalah rumusnya:

![Rumus Cosine Similarity](https://i0.wp.com/hendroprasetyo.com/wp-content/uploads/2020/04/image-3.png?resize=407%2C110&ssl=1)

Langkah selanjutnya yaitu menggunakan _argpartition_ untuk mengambil sejumlah nilai k tertinggi dari _similarity_ data kemudian mengambil data dari bobot (tingkat kesamaan) tertinggi ke terendah. Kemudian menguji akurasi dari sistem rekomendasi ini untuk menemukan rekomendasi movies yang mirip dari film yang ingin dicari.

- Kelebihan
  - Semakin banyak informasi yang diberikan pengguna, semakin baik akurasi sistem rekomendasi.

- Kekurangan
  - Hanya dapat digunakan untuk fitur yang sesuai, seperti film, dan buku.
  - Tidak mampu menentukan profil dari user baru.


### Collaborative Filtering
Pada modeling `Collaborative Filtering` penulis menggunakan data hasil gabungan dari dua datasets yaitu *movies.csv* & *ratings.csv*. Langkah pertama adalah melakukan _encode_ data `userId` & `movieId` setelah di _encode_ lakukan _mapping_ ke dalam data yang digunakan dan juga mengubah nilai _rating_ menjadi _float_. Selanjutnya ialah membagi data untuk _training_ sebesar 80% dan validasi sebesar 20%.

Lakukan proses _embedding_ terhadap data film dan pengguna. Lalu lakukan operasi perkalian _dot product_ antara _embedding_ pengguna dan film. Selain itu, penulis juga menambahkan bias untuk setiap pengguna dan film. Skor kecocokan ditetapkan dalam skala [0,1] dengan fungsi aktivasi _sigmoid_. Untuk mendapatkan rekomendasi film, penulis mengambil sampel user secara acak dan mendefinisikan variabel _movie_not_watched_ yang merupakan daftar film yang belum pernah ditonton oleh pengguna.

- Kelebihan
  - Tidak memerlukan atribut untuk setiap itemnya.
  - Dapat membuat rekomendasi tanpa harus selalu menggunakan dataset yang lengkap.
  - Unggul dari segi kecepatan dan skalabilitas.
  - Rekomendasi tetap akan berkerja dalam keadaan dimana konten sulit dianalisi sekalipun

- Kekurangan
  - Membutuhkan parameter rating, sehingga jika ada item baru sistem tidak akan merekomendasikan item tersebut.

## Evaluation
Pada tahap ini, penulis menggunakan _Mean Absolute Error (MAE)_ dan _Root Mean Squared Error (RMSE)_ sebagai metrik evaluasi. Berikut penjelasannya:

1. _Mean Absolute Error (MAE)_ mengukur besarnya rata-rata kesalahan dalam serangkaian prediksi yang sudah dilatih kepada data yang akan dites, tanpa mempertimbangkan arahnya. Semakin rendah nilai MAE (_Mean Absolute Error_) maka semakin baik dan akurat model yang dibuat.

    Berikut ini adalah rumus MAE:

    ![MAE](https://gisgeography.com/wp-content/uploads/2014/08/mae-formula.png)

    Berikut visualisasi dari _fitting_ menggunakan metrik MAE:

    ![Plot MAE](https://raw.githubusercontent.com/AzharRizky/Movie-Recommendation-System/main/images/mae.png)

    Berdasarkan hasil _fitting_ nilai konvergen metrik MAE berada pada 0.1319 untuk training dan 0.1450 untuk validasi.

2. _Root Mean Squared Error (RMSE)_ adalah aturan penilaian kuadrat yang juga mengukur besarnya rata-rata kesalahan. Sama seperti MAE, semakin rendahnya nilai _root mean square error_ juga menandakan semakin baik model tersebut dalam melakukan prediksi.

    Berikut ini adalah rumus RMSE:

    ![RMSE](https://1.bp.blogspot.com/-MM7g3UQjW9s/X8JzKPlxfQI/AAAAAAAACX0/zNDQCP4CJWANa1Bh_zBoLBCCOuUnCXKigCPcBGAYYCw/s16000/Rumus%2BRMSE.jpg)

    Berikut visualisasi dari _fitting_ menggunakan metrik RMSE:

    ![Plot RMSE](https://raw.githubusercontent.com/AzharRizky/Movie-Recommendation-System/main/images/rmse.png)

    Berdasarkan hasil _fitting_ nilai konvergen metrik RMSE berada pada 0.1718 untuk training dan 0.1881 untuk validasi.

    Untuk menghasilkan nilai yang konvergen proses `fitting` memerlukan 15 _epoch_. Dari hasil perhitungan kedua metrik diatas dapat disimpulkan bahwa model ini memiliki tingkat eror di bawah 20%.

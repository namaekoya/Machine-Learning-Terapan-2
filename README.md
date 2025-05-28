# Laporan Proyek Machine Learning - Eko Prabowo

## Project Overview

### Latar belakang

Pertumbuhan industri perfilman, baik di kancah internasional maupun nasional, menunjukkan perkembangan yang semakin menjanjikan. Hal ini tercermin dari peningkatan jumlah penonton bioskop setiap tahunnya. Pada tahun 2018, jumlah penonton bioskop di Indonesia tercatat telah melampaui angka 50 juta, dengan total produksi film, baik dari dalam maupun luar negeri mencapai hampir 200 judul yang telah diputar di seluruh wilayah Indonesia (Tren Positif Film Indonesia | Indonesia.go.id, 2019).

Banyaknya jumlah film yang dirilis menimbulkan tantangan tersendiri bagi calon penonton dalam menentukan pilihan film yang ingin mereka tonton. Proses pencarian film dapat memakan waktu, dan film yang telah dipilih pun belum tentu sesuai dengan preferensi penonton setelah ditonton, sehingga berpotensi menyebabkan pemborosan waktu. Selain itu, menonton film melalui berbagai media seperti bioskop, platform layanan streaming, maupun pembelian dan penyewaan DVD memerlukan biaya. Apabila film yang ditonton tidak sesuai ekspektasi, maka biaya tersebut akan terbuang percuma.

Sebagian individu yang mengalami kesulitan dalam memilih film umumnya mengandalkan situs-situs seperti suggestmemovie.com, yang menyediakan saran film kepada pengguna, atau platform StayIn app yang menggunakan kuesioner untuk mengidentifikasi suasana hati pengguna melalui beberapa pertanyaan. Meskipun demikian, para pengguna situs-situs tersebut mengaku seringkali harus mencoba berkali-kali hingga menemukan film yang dirasa cocok (Mihir, 2019).

Netflix, sebagai salah satu platform layanan streaming digital terbesar saat ini, juga menghadapi tantangan serupa. Banyaknya pilihan film dan serial seringkali membuat pengguna bingung. Untuk mengatasi hal tersebut, Netflix menghadirkan fitur shuffle play yang secara otomatis memutar film atau serial berdasarkan pilihan sistem, sebagai upaya memberikan solusi atas permasalahan tersebut.

Dalam proses pencarian kemiripan antar dokumen, metode cosine similarity menjadi salah satu pendekatan yang efektif. Metode ini telah digunakan dalam penelitian mengenai sistem temu kembali buku berbahasa Arab oleh Fauzi, Arifin, dan Yuniarti (2017). Pendekatan tersebut mengombinasikan frekuensi kata, inverse document frequency, inverse class frequency, dan inverse book frequency sebagai dasar perhitungan pembobotan term. Nilai pembobotan ini kemudian dianalisis kemiripannya menggunakan metode cosine similarity.

Proyek yang dirancang dalam konteks ini bertujuan untuk mengembangkan sistem rekomendasi judul film berbasis genre, dengan memanfaatkan data metadata movies yang diperoleh dari platform Kaggle. Sistem ini dirancang guna memberikan solusi atas permasalahan yang dihadapi pengguna dalam memilih film, serta memudahkan pengguna untuk memperoleh rekomendasi film berdasarkan genre yang sesuai dengan judul film yang dicari atau telah diinput sebelumnya. Adapun metode yang digunakan dalam pengembangan sistem ini adalah content-based filtering.

## Business Understanding
### Problem Statements

- Bagaimana cara melakukan pra-pemrosesan pada data movie recomendation yang akan digunakan agar dapat membuat model yang baik menggunakan teknik content-base filtering?
- Bagaimana memberikan rekomendasi judul film berdasarkan genre pada setiap judul film yang pelanggan input sehingga dapat memberikan preferensi yang sesuai pelanggan inginkan?

### Goals

- Melakukan pra-pemrosesan dengan baik agar dapat digunakan dalam pembuatan model.
- Membuat pelanggan lebih mudah menemukan judul film yang tepat dengan bantuan sistem rekomendasi judul film berdasarkan genre yang dibuat.

    ### Solution statements
    Solusi yang dapat dilakukan untuk memenuhi tujuan dari proyek ini diantaranya :
    - Untuk pra-pemrosesan data dapat dilakukan beberapa teknik, diantaranya :
        Mengecek masalah data yang kosong dengan melakukan pengecekan terlebih dahulu.
        Menghitung besar/panjang data pada dataset terlebih dahulu kemudian mencoba untuk menguraikan jenis-jenis fitur pada kolom genre
        Mengurutkan data movieId dan menghapus data yg sama
        Membuang judul film yg duplikat dengan method 
    - Metode yang digunakan pada projek ini adalah Content Based Filtering. Content Based Filtering adalah rekomendasi berbasis konten yang merekomendasikan item yang memiliki kemiripan dengan item yang disukai/diinput pengguna sebelumnya. Content-based filtering mempelajari profil minat pengguna baru berdasarkan data dari objek yang telah dinilai pengguna [[6](http://103.23.20.161/index.php/semnasif/article/view/1148)]. Metode ini bekerja dengan menyarankan item serupa yang pernah disukai sebelumnya atau sedang dilihat sekarang kepada pengguna berdasrakan kategori tertentu dari item yang dinilai oleh pengguna. Kelebihan dan Kekurangan dari Content-based Filtering adalah sebagai berikut:
        * Kelebihan
            * User Independence: Tidak bergantung kepada user lain dalam memberikan rekomendasi yang ada. New Item Mampu merekomendasikan item yang belum dinilai oleh setiap pengguna.
        * Kekurangan
            * New User: Sistem tidak dapat memberikan rekomendasi yang dapat diandalkan pada pengguna baru, karena membutuhkan penelusuran terlebih dahulu pada preferensi pengguna

## Data Understanding

Data pada project ini menggunakan data yang bersumber pada sebuah situs kaggle, dimana fokus pada data tersebut menyajikan data-data daftar film dari yg terlama hingga ke yg terbaru serta memberikan korelasi dengan data rating yg disediakan pada dataset (tidak terlalu banyak digunakan pada studi kasus projek ini).
Informasi dataset dapat dilihat pada tabel dibawah ini :
Jenis | Keterangan
--- | ---
Sumber | [Kaggle Dataset : Movie recomendation pjct](https://www.kaggle.com/datasets/sayan0211/movie-recomendation-pjct)
Lisensi | Unknown
Kategori | Movies, TV Shows, Recomendations movie Dataset
Jenis dan Ukuran Berkas | Zip (866 kB)

Pada berkas yang diunduh yakni movies.csv berisi 9742 rows × 3 columns. Untuk penjelasan mengenai variabel-variable pada dataset movies recomendation ini dapat dilihat sebagai berikut:
- **movieId** merupakan parameter bernilai unique. Parameter ini digunakan untuk mengindetifikasi daftar tiap-tiap film.
- **genre** merupakan parameter yg menyimpan tiap-tiap kategori film
- **title** merupakan parameter yg menyimpan judul masing-masing film

Berikut beberapa tahapan Data Understanding diantaranya sebagai berikut:

### Meload Dataset ke dalam sebuah Dataframe menggunakan pandas, data yang ditampilkan sebagai berikut:

|      | movieId |                                     title |                                          genres |   |
|-----:|--------:|------------------------------------------:|------------------------------------------------:|---|
|   0  |       1 |                          Toy Story (1995) | Adventure\|Animation\|Children\|Comedy\|Fantasy |   |
|   1  |       2 |                            Jumanji (1995) |                    Adventure\|Children\|Fantasy |   |
|   2  |       3 |                   Grumpier Old Men (1995) |                                 Comedy\|Romance |   |
|   3  |       4 |                  Waiting to Exhale (1995) |                          Comedy\|Drama\|Romance |   |
|   4  |       5 |        Father of the Bride Part II (1995) |                                          Comedy |   |
|  ... |     ... |                                       ... |                                             ... |   |
| 9737 |  193581 | Black Butler: Book of the Atlantic (2017) |              Action\|Animation\|Comedy\|Fantasy |   |
| 9738 |  193583 |              No Game No Life: Zero (2017) |                      Animation\|Comedy\|Fantasy |   |
| 9739 |  193585 |                              Flint (2017) |                                           Drama |   |
| 9740 |  193587 |       Bungo Stray Dogs: Dead Apple (2018) |                               Action\|Animation |   |
| 9741 |  193609 |       Andrew Dice Clay: Dice Rules (1991) |                                          Comedy |   |

Terdapat 9741 baris dengan 3 kolom dari data yang akan ditampilkan

### Menampilkan keterangan jumlah/panjang data unique daftar film dan data pengguna/user

Banyak Data movies ID:  9742

### Menampilkan informasi dataset & cek kondisi data

![Screenshot 2025-05-24 143309](https://github.com/user-attachments/assets/12c344e2-37dd-4883-8eb6-886e2a56b6ad)

Memuat informasi dataframe movies_meta_data dan melihat missing value dan duplicate, seperti yang ditampilkan tidak ada missing value maupun duplicate pada semua data.

### Menampilkan Daftar Genre pada dataset

![Screenshot 2025-05-20 151441](https://github.com/user-attachments/assets/318cf42e-0ff7-4511-9a82-fa2b2b4fd978)

### Menghitung besar/panjang data genre secara unique

Jumlah data genre:  951

Menghitung jumlah data genre data pada file movie.csv secara uniqe. Hasil menunjukkan bahwa terdapat 951 data yang uniqe

### Memuat deskripsi setiap kolom dataframe untuk perhitungan count, rata-rata, minimal value dan maximal value

|       |       movieId |   |   |   |
|------:|--------------:|--:|--:|---|
| count |   9742.000000 |   |   |   |
|  mean |  42200.353623 |   |   |   |
|  std  |  52160.494854 |   |   |   |
|  min  |      1.000000 |   |   |   |
|  25%  |   3248.250000 |   |   |   |
|  50%  |   7300.000000 |   |   |   |
|  75%  |  76232.000000 |   |   |   |
|  max  | 193609.000000 |   |   |   |

|         | 0 |   |   |   |
|--------:|--:|--:|--:|---|
| movieId | 0 |   |   |   |
|  title  | 0 |   |   |   |
|  genres | 0 |   |   |   |

Berdasarkan data tersebut jumlah data ialah 9742 dengan mean 42200 dan nilai min 1 dan max 193609. Selain itu Standar Deviasi pada data senilai 52160. Selanjutnya mengecek data yang kosong, data menunjukkan tidak ada data yang kosong

### Memuat dataset ke dalam variable baru

|      | movieId |                                     title |                                          genres |   |
|-----:|--------:|------------------------------------------:|------------------------------------------------:|---|
|   0  |       1 |                          Toy Story (1995) | Adventure\|Animation\|Children\|Comedy\|Fantasy |   |
|   1  |       2 |                            Jumanji (1995) |                    Adventure\|Children\|Fantasy |   |
|   2  |       3 |                   Grumpier Old Men (1995) |                                 Comedy\|Romance |   |
|   3  |       4 |                  Waiting to Exhale (1995) |                          Comedy\|Drama\|Romance |   |
|   4  |       5 |        Father of the Bride Part II (1995) |                                          Comedy |   |
|  ... |     ... |                                       ... |                                             ... |   |
| 9737 |  193581 | Black Butler: Book of the Atlantic (2017) |              Action\|Animation\|Comedy\|Fantasy |   |
| 9738 |  193583 |              No Game No Life: Zero (2017) |                      Animation\|Comedy\|Fantasy |   |
| 9739 |  193585 |                              Flint (2017) |                                           Drama |   |
| 9740 |  193587 |       Bungo Stray Dogs: Dead Apple (2018) |                               Action\|Animation |   |
| 9741 |  193609 |       Andrew Dice Clay: Dice Rules (1991) |                                          Comedy |   |

Data menunjukkan terdapat 9742 baris dengan 3 kolom

### Menampilkan kata paling banyak

![image](https://github.com/user-attachments/assets/d0c5973f-faab-4d54-8d10-9a7d836a284d)

Menampilkan kata dengan frekuensi terbanyak pada kolom genre. Data menunjukkan kata "Drama" dan "Comedy" memiliki jumlah kata paling banyak

## Data Preparation

Berikut adalah tahapan-tahapan dalam melakukan Persiapan data:

### Memilih kolom berdasarkan data yang dibutuhkan untuk melakukan content based learning berdasarkan genre yaitu judul dan genre

9742

Memilih kolom berdasarkan data, terlihat masing-masing menampilkan 9742 data. Dengan demikian tidak ada missing value.

### Membuat data menjadi dalam bentuk dataframe sehingga mudah untuk dipersiapkan

|      |                                     judul |                                           genre |   |   |
|-----:|------------------------------------------:|------------------------------------------------:|--:|---|
|   0  |                          Toy Story (1995) | Adventure\|Animation\|Children\|Comedy\|Fantasy |   |   |
|   1  |                            Jumanji (1995) |                    Adventure\|Children\|Fantasy |   |   |
|   2  |                   Grumpier Old Men (1995) |                                 Comedy\|Romance |   |   |
|   3  |                  Waiting to Exhale (1995) |                          Comedy\|Drama\|Romance |   |   |
|   4  |        Father of the Bride Part II (1995) |                                          Comedy |   |   |
|  ... |                                       ... |                                             ... |   |   |
| 9737 | Black Butler: Book of the Atlantic (2017) |              Action\|Animation\|Comedy\|Fantasy |   |   |
| 9738 |              No Game No Life: Zero (2017) |                      Animation\|Comedy\|Fantasy |   |   |
| 9739 |                              Flint (2017) |                                           Drama |   |   |
| 9740 |       Bungo Stray Dogs: Dead Apple (2018) |                               Action\|Animation |   |   |
| 9741 |       Andrew Dice Clay: Dice Rules (1991) |                                          Comedy |   |   |

![Screenshot 2025-05-20 153426](https://github.com/user-attachments/assets/6c4813ed-f642-43e2-9cd8-e362fce21707)

Melihat informasi kolom pada data, terlihat data type yaitu object tanpa missing value. Dengan demikian, data tersebut tidak perlu dilakukan penangangan lebih lanjut.

### Memuat banyak data dari setiap unique value berdasarkan genre

|     |                                         genre | count |   |   |
|----:|----------------------------------------------:|------:|--:|---|
|  0  |                                         Drama |  1053 |   |   |
|  1  |                                        Comedy |   946 |   |   |
|  2  |                                 Comedy\|Drama |   435 |   |   |
|  3  |                               Comedy\|Romance |   363 |   |   |
|  4  |                                Drama\|Romance |   349 |   |   |
| ... |                                           ... |   ... |   |   |
| 946 |                      Children\|Drama\|Musical |     1 |   |   |
| 947 |   Adventure\|Drama\|Horror\|Mystery\|Thriller |     1 |   |   |
| 948 | Adventure\|Children\|Comedy\|Fantasy\|Mystery |     1 |   |   |
| 949 |       Adventure\|Animation\|Children\|Western |     1 |   |   |
| 950 |            Comedy\|Mystery\|Romance\|Thriller |     1 |   |   |

Data menunjukkan 951 data uniqe dengan dua kolom. Drama memiliki jumlah tertinggi dengan 1053 dan disusul Comedy dengan 946 data.

### Menambahkan tanda strip

Membuat tanda '-' pada variabel data dihapus

#### Melihat Jenis-Jenis Genre yang terdapat pada data

![Screenshot 2025-05-20 154041](https://github.com/user-attachments/assets/9cfbaf8c-e240-44f7-8e9c-5ad73ab21ea6)

#### Melakukan drop pada judul film yg double, dan berhasil menghapus beberapa judul

Melakukan penghapusan pada data yang mengalami duplikat, seterlah dilakukan penghapusan data duplikat maka data yang tersisa menjadi 9737 baris.

### Melakukan indeks ulang pada data agar penomoran dilakukan berurutan

![Screenshot 2025-05-20 154259](https://github.com/user-attachments/assets/f6212467-89c1-4505-bd26-27fc249d7122)

### Memasukkan nilai data masing-masing kolom ke dalam variabel baru berdasarkan genre

![Screenshot 2025-05-20 154432](https://github.com/user-attachments/assets/e7875848-8d5e-4e31-a475-13cfc92136d6)

Mengecek ulang data yg dimasukkan ke dalam variable baru dengan perintah '''to list''' ke kolom judul dan dilanjutkan pada kolom genre.

### Proses Data

#### Membangun sistem rekomendasi berdasarkan genre yang ada pada setiap movies.

"array(['action', 'adventure', 'animation', 'children', 'comedy', 'crime',
       'documentary', 'drama', 'fantasy', 'fi', 'film', 'genres',
       'horror', 'imax', 'listed', 'musical', 'mystery', 'no', 'noir',
       'romance', 'sci', 'thriller', 'war', 'western'], dtype=object) "

Melakukan sistem rekomendasi pada genre pada setiap movies yang ada seperti yang ditampilkan di atas.

#### Melakukan Proses fit dan melihat jumlah ukuran matrix

Menghasilkan data sebagai berikut: (9737, 24)

#### Mengubah vektor ke dalam bentuk matrix

![Screenshot 2025-05-26 211407](https://github.com/user-attachments/assets/7e3cc843-9ebb-485f-9b44-f641edd70105)


Melakukan tranformasi vektor ke dalam bentuk matriks seperti data yang ditampilkan.

#### Melihat Daftar jumlah film berdasarkan genre dan melihat korelasi nya yg diperlihatkan dalam bentuk matrix

|                                judul | listed |  romance | musical |    drama | film | thriller |   action |       fi |  mystery | crime | ... | documentary | genres | western | war |      sci |   comedy | imax | noir | fantasy | children |   |
|-------------------------------------:|-------:|---------:|--------:|---------:|-----:|---------:|---------:|---------:|---------:|------:|----:|------------:|-------:|--------:|----:|---------:|---------:|-----:|-----:|--------:|---------:|---|
|       Conspiracy Theory (1997)       |    0.0 | 0.490731 |     0.0 | 0.314993 |  0.0 | 0.460705 | 0.000000 | 0.000000 | 0.669114 |   0.0 | ... |         0.0 |    0.0 |     0.0 | 0.0 | 0.000000 | 0.000000 |  0.0 |  0.0 |     0.0 | 0.000000 |   |
|         28 Days Later (2002)         |    0.0 | 0.000000 |     0.0 | 0.000000 |  0.0 | 0.000000 | 0.423884 | 0.522916 | 0.000000 |   0.0 | ... |         0.0 |    0.0 |     0.0 | 0.0 | 0.522916 | 0.000000 |  0.0 |  0.0 |     0.0 | 0.000000 |   |
|             Speed (1994)             |    0.0 | 0.599087 |     0.0 | 0.000000 |  0.0 | 0.562432 | 0.569882 | 0.000000 | 0.000000 |   0.0 | ... |         0.0 |    0.0 |     0.0 | 0.0 | 0.000000 | 0.000000 |  0.0 |  0.0 |     0.0 | 0.000000 |   |
|       Conversation, The (1974)       |    0.0 | 0.000000 |     0.0 | 0.425925 |  0.0 | 0.000000 | 0.000000 | 0.000000 | 0.904758 |   0.0 | ... |         0.0 |    0.0 |     0.0 | 0.0 | 0.000000 | 0.000000 |  0.0 |  0.0 |     0.0 | 0.000000 |   |
|            Jason X (2002)            |    0.0 | 0.000000 |     0.0 | 0.000000 |  0.0 | 0.419322 | 0.000000 | 0.524140 | 0.000000 |   0.0 | ... |         0.0 |    0.0 |     0.0 | 0.0 | 0.524140 | 0.000000 |  0.0 |  0.0 |     0.0 | 0.000000 |   |
|          Now and Then (1995)         |    0.0 | 0.000000 |     0.0 | 0.439701 |  0.0 | 0.000000 | 0.000000 | 0.000000 | 0.000000 |   0.0 | ... |         0.0 |    0.0 |     0.0 | 0.0 | 0.000000 | 0.000000 |  0.0 |  0.0 |     0.0 | 0.898144 |   |
|           Speechless (1994)          |    0.0 | 0.821173 |     0.0 | 0.000000 |  0.0 | 0.000000 | 0.000000 | 0.000000 | 0.000000 |   0.0 | ... |         0.0 |    0.0 |     0.0 | 0.0 | 0.000000 | 0.570679 |  0.0 |  0.0 |     0.0 | 0.000000 |   |
| How to Make an American Quilt (1995) |    0.0 | 0.841550 |     0.0 | 0.540179 |  0.0 | 0.000000 | 0.000000 | 0.000000 | 0.000000 |   0.0 | ... |         0.0 |    0.0 |     0.0 | 0.0 | 0.000000 | 0.000000 |  0.0 |  0.0 |     0.0 | 0.000000 |   |
|       Play Misty for Me (1971)       |    0.0 | 0.000000 |     0.0 | 0.564407 |  0.0 | 0.825496 | 0.000000 | 0.000000 | 0.000000 |   0.0 | ... |         0.0 |    0.0 |     0.0 | 0.0 | 0.000000 | 0.000000 |  0.0 |  0.0 |     0.0 | 0.000000 |   |
|           Road Trip (2000)           |    0.0 | 0.000000 |     0.0 | 0.000000 |  0.0 | 0.000000 | 0.000000 | 0.000000 | 0.000000 |   0.0 | ... |         0.0 |    0.0 |     0.0 | 0.0 | 0.000000 | 1.000000 |  0.0 |  0.0 |     0.0 | 0.000000 |   |

Data menunjukkan terdapat 10 baris dengan 22 kolom. Dari data tersebut menunjukkan bahwa korelasi 1 berarti memiliki kemipiran yang tinggi dibanding korelasi 0.

## Modeling

Setelah dilakukan pra-pemrosesan pada dataset, langkah selanjutnya adalah *modeling* terhadap data. Pada tahap ini Model machine learning yang digunakan pada sistem rekomendasi ini adalah model _content-based filtering_ dengan _simlarty measure_ yang digunakan adalah _Cosine Similarity_.

Model _content-based filtering_ ini bekerja dengan mempelajari profil minat pengguna baru berdasarkan data dari objek yang telah dinilai pengguna. Metode ini bekerja dengan menyarankan item serupa yang pernah disukai sebelumnya atau sedang dilihat sekarang kepada pengguna berdasrakan kategori tertentu dari item yang dinilai oleh pengguna dengan menggunakan _similarity_ tertentu.

Sedangkan _cosine similarity_ adalah salah satu teknik mengukur kesamaan yang bekerja dengan mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama dengan menghitung sudut cosinus antara dua vektor. Semakin kecil sudut cosinus, semakin besar nilai _cosine similarity_.

Cara kerja dari fungsi *cosine similiraty* yaitu dengan melakukan perhitungan yang sering digunakan untuk menghitung kemiripan diantara item-item [[7]](https://jurnal.uns.ac.id/itsmart/article/download/35008/27748). Secara umum, fungsi similarity adalah fungsi yang menerima dua buah obyek berupa bilangan riil (0 dan 1) dan mengembalikan nilai kemiripan (similarity) antara kedua obyek tersebut berupa bilangan riil. Cosine similarity merupakan salah satu metode pengukuran kemiripan yang populer. Metode ini digunakan untuk menghitung nilai kosinus sudut antara dua vektor dan biasanya digunakan untuk mengukur kemiripan antara dua teks/dokumen. Fungsi cosine similarity antara item A dan item B ditunjukkan sebagai berikut [[8]](https://jurnal.uns.ac.id/itsmart/article/download/35008/27748).

![Screenshot 2025-05-20 161116](https://github.com/user-attachments/assets/efa32249-1d46-4a16-ae05-acf1f263512a)


Keterangan:
```
𝑠𝑖𝑚(𝐴, 𝐵) = nilai similaritas dari item A dan item B
𝑛(𝐴) = banyaknya fitur konten item A 
𝑛(𝐵) = banyaknya fitur konten item B 
𝑛(𝐴 ∩ 𝐵)  = banyaknya fitur konten yang terdapat pada item A dan juga terdapat pada item B
```
Jika kedua objek memiliki nilai similaritas 1, maka kedua objek dikatakan identik dan sebaliknya. Semakin besar hasil dari fungsi similarity, maka kedua objek yang dievaluasi dianggap semakin mirip dan sebaliknya. 

Tahapan yang dilakukan pada fungsi tersebut ialah sebagai berikut:

###  Melatih Model dengan cosine similarity

![Screenshot 2025-05-26 211947](https://github.com/user-attachments/assets/822732b5-2ab8-4e56-ac23-cefbac480bab)

### Menampilkan Matriks Kesamaan

|                                         judul | Children\|Comedy\|Drama | Documentary | Action\|Adventure\|Children\|Comedy\|Fantasy |    Drama | Drama\|Horror\|Mystery\|Thriller | Drama\|Fantasy\|Mystery\|Sci-Fi | Drama\|Horror | Drama\|Fantasy\|Sci-Fi |   Comedy | Adventure\|Drama |
|----------------------------------------------:|------------------------:|------------:|---------------------------------------------:|---------:|---------------------------------:|--------------------------------:|--------------:|-----------------------:|---------:|-----------------:|
|           3 Ninjas Knuckle Up (1995)          |                0.656385 |         0.0 |                                     0.669600 | 0.000000 |                         0.000000 |                        0.000000 |      0.000000 |               0.000000 | 0.000000 |         0.000000 |
|                Beautiful (2000)               |                0.585127 |         0.0 |                                     0.211031 | 0.678501 |                         0.204634 |                        0.169542 |      0.325605 |               0.200049 | 0.734599 |         0.346050 |
| Looking for Comedy in the Muslim World (2005) |                0.429834 |         0.0 |                                     0.287274 | 0.000000 |                         0.000000 |                        0.000000 |      0.000000 |               0.000000 | 1.000000 |         0.000000 |
|           Night of the Lepus (1972)           |                0.000000 |         0.0 |                                     0.000000 | 0.000000 |                         0.473967 |                        0.478879 |      0.459843 |               0.565049 | 0.000000 |         0.000000 |
|     Broken Wings (Knafayim Shvurot) (2002)    |                0.397010 |         0.0 |                                     0.000000 | 1.000000 |                         0.301597 |                        0.249877 |      0.479889 |               0.294840 | 0.000000 |         0.510021 |
|        Desperately Seeking Susan (1985)       |                0.402119 |         0.0 |                                     0.145028 | 0.466289 |                         0.140631 |                        0.116515 |      0.223767 |               0.137481 | 0.504842 |         0.237817 |
|                  Logan (2017)                 |                0.000000 |         0.0 |                                     0.195544 | 0.000000 |                         0.000000 |                        0.560499 |      0.000000 |               0.661355 | 0.000000 |         0.000000 |
|               Used People (1992)              |                0.585127 |         0.0 |                                     0.211031 | 0.678501 |                         0.204634 |                        0.169542 |      0.325605 |               0.200049 | 0.734599 |         0.346050 |
|                Blue Ruin (2013)               |                0.000000 |         0.0 |                                     0.000000 | 0.000000 |                         0.441113 |                        0.000000 |      0.000000 |               0.000000 | 0.000000 |         0.000000 |

### Menampilkan hasil rekomendasi modelling

|    |                                                    judul |         genre |
|---:|---------------------------------------------------------:|--------------:|
|  0 |                                         Big Bully (1996) | Comedy\|Drama |
|  1 |                          Antonia's Line (Antonia) (1995) | Comedy\|Drama |
|  2 |                            In the Bleak Midwinter (1995) | Comedy\|Drama |
|  3 |               Nobody Loves Me (Keiner liebt mich) (1994) | Comedy\|Drama |
|  4 |                                  Blue in the Face (1995) | Comedy\|Drama |
|  5 |                                           Jeffrey (1995) | Comedy\|Drama |
|  6 |                              Love & Human Remains (1993) | Comedy\|Drama |
|  7 |                                             Smoke (1995) | Comedy\|Drama |
|  8 |                                   Unstrung Heroes (1995) | Comedy\|Drama |
|  9 |                                  Boys on the Side (1995) | Comedy\|Drama |
| 10 |                                           Ed Wood (1994) | Comedy\|Drama |
| 11 |                       Madness of King George, The (1994) | Comedy\|Drama |
| 12 |                                         Roommates (1995) | Comedy\|Drama |
| 13 |          Three Colors: White (Trzy kolory: Bialy) (1994) | Comedy\|Drama |
| 14 |                              Swimming with Sharks (1995) | Comedy\|Drama |
| 15 |                                    Sum of Us, The (1994) | Comedy\|Drama |
| 16 | Adventures of Priscilla, Queen of the Desert, The (1994) | Comedy\|Drama |
| 17 |                                          Crooklyn (1994) | Comedy\|Drama |
| 18 |                                        Paper, The (1994) | Comedy\|Drama |

Berdasarkan modelling yang telah dibuat maka ditampilkan rekomendasi dari film berjudul Letter to Three Wives, A (1949) seperti di atas.

## Evaluation

### Mengindikasi dan memperlihatkan judul film berdasarkan urutan dari data

![Screenshot 2025-05-26 212422](https://github.com/user-attachments/assets/6c63f2b0-c589-45e7-9964-49aae6435f86)

Berdasarkan data tersebut terdapat urutan data dimulai dari Toy Story (1995), Jumanji (1995), Grumpier Old Men (1995), Waiting to Exhale (1995), Father of the Bride Part II (1995)

### Membuat fungsi untuk memanggil 20 rekomendasi film berdasarkan judul yang di input

![Screenshot 2025-05-26 212648](https://github.com/user-attachments/assets/1e0585ea-c1d7-4c70-8eec-07c4bfdd4859)

### Menampilkan 19 rekomendasi film dari judul yang telah di input menggunakan fungsi movie_recomendations

|    |                                          judul | genre |
|---:|-----------------------------------------------:|------:|
|  0 |                                 Othello (1995) | Drama |
|  1 |                         Dangerous Minds (1995) | Drama |
|  2 |                Cry, the Beloved Country (1995) | Drama |
|  3 |                             Restoration (1995) | Drama |
|  4 |                                 Georgia (1995) | Drama |
|  5 |                   Home for the Holidays (1995) | Drama |
|  6 |                      Mr. Holland's Opus (1995) | Drama |
|  7 |                Boys of St. Vincent, The (1992) | Drama |
|  8 |                 Basketball Diaries, The (1995) | Drama |
|  9 |               Awfully Big Adventure, An (1995) | Drama |
| 10 |       Beauty of the Day (Belle de jour) (1967) | Drama |
| 11 |                                    Kids (1995) | Drama |
| 12 |                                   Nadja (1994) | Drama |
| 13 |                               Showgirls (1995) | Drama |
| 14 |                      White Man's Burden (1995) | Drama |
| 15 |                   Browning Version, The (1994) | Drama |
| 16 | Burnt by the Sun (Utomlyonnye solntsem) (1994) | Drama |
| 17 |                               Cure, The (1995) | Drama |
| 18 |                                 Exotica (1994) | Drama |

Dengan hasil yang diberikan di atas berdasarkan judul film "Lost and Delirious (2001)" dengan genre Drama maka didapatkan 19 rekomendasi judul film dengan genre yang serupa ataupun mirip.

### Menghitung banyaknya data genre pada hasil rekomendasi

![Screenshot 2025-05-26 213057](https://github.com/user-attachments/assets/e542c294-e283-4de8-9790-53c0ea5ef2fb)

### Melakukan perhitungan dengan menggunakan metrik

100%
Precision@10: 1.0000
Recall@10: 0.0095
Average Precision: 0.0180
Mean Average Precision (MAP): 0.4097

Dalam studi kasus film Lost and Delirious (2001), sistem rekomendasi menunjukkan kinerja yang sangat tinggi dalam hal ketepatan, ditunjukkan oleh Precision@10 sebesar 1.0000, yang berarti seluruh 10 film yang direkomendasikan dianggap relevan. Namun, sistem memiliki kelemahan signifikan dalam hal cakupan, dengan Recall@10 hanya 0.0095, yang menunjukkan bahwa dari semua film relevan yang mungkin tersedia, hanya sebagian kecil yang berhasil direkomendasikan. 

Selain itu, Average Precision sebesar 0.0180 mengindikasikan bahwa urutan kemunculan film relevan dalam daftar rekomendasi belum optimal, meskipun akurasinya tinggi. Secara keseluruhan, Mean Average Precision (MAP) sebesar 0.4097 mencerminkan bahwa sistem memiliki performa menengah dalam memberikan dan mengurutkan rekomendasi secara umum. Dengan demikian, sistem ini sangat selektif dan tepat dalam memberikan rekomendasi, tetapi masih perlu ditingkatkan dalam menjangkau lebih banyak item relevan dan menyusun urutan rekomendasi yang lebih baik.

## Referensi

[[1]](https://j-ptiik.ub.ac.id/index.php/j-ptiik/article/download/9163/4159/) Tren Positif Film Indonesia | Indonesia.go.id (2019). Available at: https://indonesia.go.id/ragam/seni/sosial/tren-positif-film-indonesia (Accessed: 28 August 2020).
[[2, 4]](https://j-ptiik.ub.ac.id/index.php/j-ptiik/article/download/9163/4159/)  Fajriansyah, Muhammad, Putra Pandu Adikara, & Agus Wahyu Widodo. " Sistem Rekomendasi Film Menggunakan Content Based Filtering." Jurnal Pengembangan Teknologi Informasi dan Ilmu Komputer [Online], 5.6 (2021): 2188-2199. Web. 9 Mei. 2022
https://j-ptiik.ub.ac.id/index.php/j-ptiik/article/download/9163/4159/
[[3]](https://www.makeuseof.com/tag/fastest%20-ways-good-movie-film-watching/) Mihir, P. (2019) 5 Fastest Ways to Find a Good Movie or Film Worth Watching, makeuseof.com. Available at: https://www.makeuseof.com/tag/fastest -ways-good-movie-film-watching/ (Accessed: 22 December 2020).
[[5]](https://pdfs.semanticscholar.org/4cba/7c655cf843fe703211f385259ac082cb2b00.pdf) Fauzi, M. A., Arifin, A. Z. and Yuniarti, A. (2017) ‘Arabic book retrieval using class and book index based term weighting’, International Journal of Electrical and Computer Engineering, 7(6), pp. 3705–3710. doi: 10.11591/ijece.v7i6.pp3705-3711. 
[[6]](http://103.23.20.161/index.php/semnasif/article/view/1148) Badriyah, T., Fernando, R., & Syarif, I. (2018). Sistem Rekomendasi Content Based Filtering Menggunakan Algoritma Apriori. Konferensi Nasional Sistem Informasi (KNSI) 2018.
http://103.23.20.161/index.php/semnasif/article/view/1148
[[7]](https://jurnal.uns.ac.id/itsmart/article/download/35008/27748) D. Jannach, M. Zanker, A. Felfernig, and G. Friedrich, Recommender systems: an introduction, vol. 40. 2011. 
[[8]](https://jurnal.uns.ac.id/itsmart/article/download/35008/27748) L. Djumiroh and R. Saptono, “Penerapan Metode Collaborative Filtering Menggunakan Rating Implisit pada Sistem Perekomendasi Pemilihan Film di Rental VCD,” J. ITSMART, vol. 1, no. 2, pp. 54–59, 2012. 

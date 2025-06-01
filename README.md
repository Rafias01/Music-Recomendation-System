# Laporan Proyek Machine Learning - Rafi Ananda Subekti

## Domain Proyek
Proyek ini berfokus pada domain musik digital, khususnya analisis data yang berasal dari platform streaming Spotify, salah satu layanan musik terbesar dan paling populer di dunia saat ini. Dengan jutaan lagu yang tersedia, Spotify menyediakan beragam informasi mengenai setiap lagu, termasuk fitur audio yang menggambarkan karakteristik musik secara detail, serta data popularitas yang mencerminkan seberapa sering lagu tersebut diputar oleh pengguna. Proyek ini bertujuan untuk menggali dan memahami berbagai aspek tersebut agar dapat memperoleh wawasan mendalam tentang tren musik dan preferensi pendengar secara global.

Fokus utama analisis adalah pada karakteristik lagu yang diwakili oleh fitur-fitur seperti danceability, energy, valence, acousticness, dan tempo. Fitur-fitur ini memberikan gambaran objektif tentang sifat musikal suatu lagu yang dapat mempengaruhi bagaimana lagu tersebut diterima oleh pendengar. Selain itu, proyek ini juga mengevaluasi popularitas lagu di berbagai playlist dan genre, yang membantu dalam memahami pola konsumsi musik berdasarkan preferensi genre dan konteks playlist tertentu. Dengan demikian, proyek ini tidak hanya mengidentifikasi lagu-lagu populer, tetapi juga mengeksplorasi hubungan antara fitur audio dan popularitas.

## Business Understanding

### Problem Statements
Rumusan masalah dari masalah latar belakang diatas adalah:
1. Apa saja top 10 Lagu dari Playlist "Global Top 50 | 2020 Hits"?
2. Apa saja 5 Genre Lagu Teratas dengan Rata-rata memiliki Popularitas Tertinggi?
3. Apakah ada korelasi Korelasi antara Energy dan Popularitas Lagu?

### Goals
Berdasarkan problem statements, berikut tujuan yang ingin dicapai pada proyek ini.
1. Mengidentifikasi 10 lagu dengan popularitas tertinggi dalam playlist "Global Top 50 | 2020 Hits" guna memahami lagu-lagu yang paling diminati secara global pada tahun 2020.
2. Menentukan 5 genre dengan rata-rata popularitas tertinggi untuk mengetahui preferensi pendengar terhadap genre tertentu.
3. Menganalisis hubungan antara tingkat energi lagu dan popularitas untuk mengetahui apakah lagu yang lebih energik cenderung lebih populer.

### Solution Approach
1. Data akan difilter berdasarkan nama playlist, lalu diurutkan berdasarkan nilai popularitas lagu secara menurun, dan diambil 10 lagu teratas sebagai hasil akhir.
2. Data akan difilter berdasarkan nama playlist, lalu diurutkan berdasarkan nilai popularitas lagu secara menurun, dan diambil 10 lagu teratas sebagai hasil akhir.
3. Menghitung koefisien korelasi Pearson antara kolom energy dan track_popularity, disertai dengan visualisasi scatter plot dan garis regresi untuk memperkuat interpretasi hubungan antara kedua variabel tersebut.

## Data Understanding
Data yang digunakan untuk membuat sistem rekomendasi musik ini diambil dari platform Kaggle, yaitu [30000 Spotify Songs](https://www.kaggle.com/datasets/joebeachcapital/30000-spotify-songs?select=spotify_songs.csv).

Dataset ini terdiri dari 23 kolom dan juga terdapat 32.833 data yang mana terdapat 10 kolom dengan tipe data object dan 13 kolom dengan tipe data int64 dan float64

Setiap kolom terdiri dan memiliki keterangan seperti dibawah ini : 


| **Kolom**                    | **Tipe Data** | **Deskripsi** |
|-----------------------------|---------------|---------------|
| `track_id`                  | object        | ID unik untuk setiap lagu. Digunakan sebagai pengenal utama. |
| `track_name`                | object        | Nama atau judul lagu. |
| `track_artist`              | object        | Nama artis atau penyanyi dari lagu. |
| `track_popularity`          | int64         | Skor popularitas (0–100) berdasarkan metrik Spotify seperti jumlah pemutaran. |
| `track_album_id`            | object        | ID unik dari album tempat lagu berasal. |
| `track_album_name`          | object        | Nama album dari lagu. |
| `track_album_release_date` | object        | Tanggal rilis album dalam format string (YYYY-MM-DD). |
| `playlist_name`             | object        | Nama playlist yang memuat lagu tersebut. |
| `playlist_id`               | object        | ID unik dari playlist. |
| `playlist_genre`            | object        | Genre utama playlist, seperti pop, rock, hip-hop. |
| `playlist_subgenre`         | object        | Subgenre dari playlist, lebih spesifik dari genre utama. |
| `danceability`              | float64       | Seberapa cocok lagu untuk menari (0–1). |
| `energy`                    | float64       | Tingkat energi dan intensitas lagu (0–1). |
| `key`                       | int64         | Nada dasar lagu dalam angka 0–11 (C sampai B). |
| `loudness`                  | float64       | Volume rata-rata lagu dalam desibel (dB), biasanya negatif. |
| `mode`                      | int64         | Tangga nada lagu: 1 = mayor, 0 = minor. |
| `speechiness`              | float64       | Proporsi unsur ucapan (0–1); tinggi jika banyak spoken word/rap. |
| `acousticness`             | float64       | Probabilitas lagu bersifat akustik (0–1). |
| `instrumentalness`         | float64       | Probabilitas lagu tanpa vokal (0–1). |
| `liveness`                 | float64       | Probabilitas lagu direkam live (0–1). |
| `valence`                  | float64       | Suasana emosional lagu (0 = sedih, 1 = ceria). |
| `tempo`                    | float64       | Tempo lagu dalam BPM (beats per minute). |
| `duration_ms`              | int64         | Durasi lagu dalam milidetik. Contoh: 240000 = 4 menit. |


### Exploratory Data Analysis

#### Analisis Berdasarkan Top 10 Lagu Terpopuler dari Playlist "Global Top 50 | 2020 Hits"
![image](https://github.com/user-attachments/assets/1539526d-7138-4849-ab52-96894007b228)

**Insight** :
- Dari output diatas kita bisa lihat 10 Lagu Terpopuler di Playlist Global Top 50 | 2020 Hits adalah :    
  -  Dance Monkey
  - ROXANNE  
  -  bad guy
  - No Idea
  - Futsal Shuffle 2020
  - 10,000 Hours (with Justin Bieber)
  - Suicidal  
  - Good as Hell (feat. Ariana Grande) - Remix
  -  Own It (feat. Ed Sheeran & Burna Boy)
  - Sweet but Psycho           
- Lagu “Dance Monkey” oleh Tones and I memiliki track_popularity tertinggi yaitu 100, menunjukkan bahwa lagu ini sangat populer secara global pada tahun 2020.
- Pada peringkat 1 dan 2 yaitu Dance Monkey - Tones and I dan Roxanne - Arizona Zervas memiliki beda selisih yang sedikit beda 1 nilai yaitu 100 dan 99.
- Popularitas lagu-lagu dalam daftar ini tidak menunjukkan perbedaan yang signifikan, dengan rentang skor antara 87 hingga 100. Hal ini mencerminkan bahwa persaingan antar lagu sangat ketat, di mana setiap track memiliki performa yang hampir setara dalam hal jumlah pemutaran dan tingkat keterlibatan pendengar. Skor popularitas yang tinggi secara konsisten juga menunjukkan bahwa lagu-lagu ini mendapatkan eksposur yang luas dan sering diputar oleh pengguna Spotify di seluruh dunia, menjadikannya bagian dari arus utama musik global pada tahun 2020.

#### Analisis Berdasarkan 5 Genre Lagu Teratas dengan Rata-rata memiliki Popularitas Tertinggi
![image](https://github.com/user-attachments/assets/f438470d-e07b-42a9-9974-a72eac916a6c)

**Insight** :
- Genre pop mencatat nilai tertinggi sebesar 47.74, menandakan dominasinya dalam playlist Spotify. Popularitas ini mencerminkan preferensi global terhadap musik pop yang dikenal catchy, mudah diingat, dan menjangkau berbagai kalangan.
- Nilai kelima genre berada dalam kisaran 41–47, menunjukkan bahwa meskipun pop mendominasi, diversitas genre di playlist Spotify cukup merata. Hal ini mencerminkan bahwa pengguna tetap mengeksplorasi berbagai jenis musik, menjadikan Spotify sebagai platform yang inklusif bagi musisi dari beragam latar belakang genre.

#### Analisis Korelasi antara Energy dan Popularitas Lagu
![image](https://github.com/user-attachments/assets/6cd66772-10b9-4c10-adcf-7c295074577f)

**Insight** :
- Nilai korelasi sebesar -0.11 menunjukkan hubungan negatif yang sangat lemah antara energi lagu dan popularitasnya.
- Scatter plot memperlihatkan titik-titik yang tersebar luas tanpa pola yang konsisten, menandakan tidak adanya tren linier yang kuat.
- Lagu dengan energy tinggi tidak selalu populer, dan lagu dengan energy rendah juga bisa sangat populer. Ini menunjukkan bahwa tingkat energi bukanlah faktor dominan dalam menentukan popularitas lagu. 

### Data Quality Verification
#### Memeriksa Missing Value
![image](https://github.com/user-attachments/assets/5a5beacb-e36f-4526-9839-445717792f03)

**insight** :
- Dari output tersebut dapat kita lihat terdapat missing value sebanyak 15 data, nantinya missing value ini akan kita hapus karena jumlah nya sedikit jadi tidak akan terlalu mempengaruhi kualitas analisis.    

#### Memeriksa Data duplikat
![image](https://github.com/user-attachments/assets/15d7dbf2-6f5f-4cb8-9d8e-fe40d3c9786c)

**insight** :
- Tidak terdapat data yang duplikat     

#### Memeriksa Outlier dan Visualisasi
##### Mengelompokkan yang mana Numerical_Features dan Categorical_Features 
![image](https://github.com/user-attachments/assets/0a5879ec-3eb1-4039-bf5b-c94e648b585d)

**insight** :
- Mengelompokkan numerical_features pada kolom dengan tipe data int64 dan float64    
- Mengelompokkan categorical_features pada kolom dengan tipe data object bool

##### Memeriksa Outlier
![image](https://github.com/user-attachments/assets/8dc89767-5a90-47fd-83bb-9a1c49d6a5bc)

**insight** :
- Terdapat outlier sebanyak 17.801

##### Visualisasi Outlier 
![image](https://github.com/user-attachments/assets/71ed46bd-3e90-411d-9292-ca539184acb1)

![image](https://github.com/user-attachments/assets/40f9b833-ac53-423d-b3be-5666babaf5b4)

![image](https://github.com/user-attachments/assets/49331a5a-044d-44ad-a8d1-1ae9874101bb)

**Insight** :
- track_popularity
  - Beberapa outlier di bagian bawah (mendekati 0) dan di bagian atas (mendekati 100). Ini menunjukkan ada beberapa trek yang sangat tidak populer dan beberapa yang sangat populer.
- danceability
  - Banyak outlier di bagian bawah (nilai danceability yang sangat rendah), menunjukkan ada beberapa trek yang tidak terlalu enak didengar.
- energy
  - Banyak outlier di bagian bawah (nilai energy yang sangat rendah), menunjukkan ada beberapa trek dengan energi yang sangat rendah.
- key
  - Tidak ada outlier yang signifikan dalam fitur ini, yang mungkin menunjukkan distribusi yang relatif merata atau terdistribusi dengan baik di antara 12 kunci musik (0-11).
- loudness
  - Banyak outlier di bagian bawah (nilai loudness yang sangat rendah, yaitu sangat pelan), menunjukkan ada beberapa trek yang sangat pelan.
- mode
  - Berada di sekitar 1.0. Ini menunjukkan bahwa sebagian besar, jika tidak semua, trek dalam dataset berada dalam mode Mayor (diwakili oleh 1). Mode Minor (diwakili oleh 0) tampaknya sangat jarang atau tidak ada dalam dataset ini.
- speechiness
  - Banyak outlier di bagian atas, menunjukkan ada beberapa trek dengan proporsi kata yang diucapkan yang sangat tinggi.
- acousticness
  - Banyak outlier di bagian atas, menunjukkan ada beberapa trek yang sangat akustik.
- instrumentalness
  - Sangat banyak outlier di bagian atas, menunjukkan ada banyak trek yang sepenuhnya instrumental (yaitu tidak ada vokal). Nilai 1.0 berarti instrumental penuh.
- liveness
  - Banyak outlier di bagian atas, mendekati 1.0. Ini mengindikasikan ada beberapa trek yang direkam secara langsung (memiliki liveness yang tinggi).
- valence
  - Beberapa outlier di bagian bawah (mendekati 0) dan di bagian atas (mendekati 1.0), menunjukkan ada beberapa trek yang sangat sedih/negatif dan beberapa yang sangat ceria/positif.
- tempo
  - Beberapa outlier di bagian bawah (tempo sangat lambat) dan di bagian atas (tempo sangat cepat), menunjukkan variasi dalam kecepatan musik.
- duration_ms
  - Banyak outlier di bagian bawah (trek yang sangat pendek) dan di bagian atas (trek yang sangat panjang), menunjukkan variasi durasi trek yang signifikan.

Kesimpulan :
Berdasarkan hasil analisis, ditemukan bahwa sebagian besar fitur dalam dataset memiliki outlier, baik di sisi nilai rendah maupun tinggi. Namun, keberadaan outlier-outlier ini mencerminkan keberagaman karakteristik lagu yang ada di Spotify, mulai dari lagu yang sangat populer hingga kurang populer, dari lagu dengan energi tinggi hingga lagu yang sangat tenang, serta dari lagu yang sepenuhnya instrumental hingga yang sangat vokal atau live.

Oleh karena itu, outlier tidak akan dihapus dalam proses analisis karena dianggap relevan secara kontekstual dan mencerminkan variasi alami dalam industri musik digital. Selain itu, mempertahankan outlier membantu memberikan gambaran yang lebih menyeluruh terhadap distribusi dan keragaman lagu, sehingga analisis menjadi lebih representatif terhadap kondisi sebenarnya. Hal ini penting untuk menjaga keseragaman dan inklusivitas data, terutama dalam proyek yang bertujuan untuk memahami berbagai preferensi musik dan tren popularitas secara global.

## Data Preparation
### Data Cleaning
#### Menghapus Missing Value 

![image](https://github.com/user-attachments/assets/ae9dd2c0-2672-4bad-80ea-78fc485ae2e3)

**Insight** :
- Setelah dilakukan penghapusan data yang missing value sudah tidak terdapat lagi data yang missing value 

#### Mengubah duration_ms menjadi menit
![image](https://github.com/user-attachments/assets/2d1c20f1-52e0-43a7-8a6e-65e14f532fe0)

Kode tersebut bertujuan untuk mengubah durasi lagu dari milidetik (duration_ms) menjadi menit (duration_min). Proses konversi dilakukan dengan cara membagi nilai milidetik dengan (1000 * 60), lalu hasilnya dibulatkan hingga dua angka di belakang koma menggunakan .round(2). Hasil konversi ini kemudian ditampilkan dalam bentuk tabel untuk lima data pertama.

#### Menghapus Kolom Yang tidak Diperlukan
![image](https://github.com/user-attachments/assets/f9b91b6b-6f65-4b9b-bb2c-145dd01839f1)

Kode tersebut berfungsi untuk menghapus beberapa kolom yang dianggap tidak relevan dari DataFrame. Kolom-kolom seperti track_id, track_album_id, track_album_name, dan lainnya dimasukkan ke dalam list columns_to_drop, lalu dihapus menggunakan df.drop().

Setelah penghapusan, DataFrame yang bersih disimpan ke dalam variabel df_cleaned, dan hasilnya ditampilkan untuk melihat kolom-kolom yang tersisa. Tujuannya adalah menyederhanakan data agar hanya kolom penting yang digunakan untuk analisis.

#### Melakukan Perubahan pada kolom Artist
![image](https://github.com/user-attachments/assets/a8d8c8a2-d57f-49c4-94ef-6159ad07f5a7)

Kode tersebut bertujuan untuk membersihkan data pada kolom track_artist, membuat identitas unik untuk setiap lagu, serta menggabungkan beberapa fitur menjadi satu kolom baru untuk keperluan analisis lebih lanjut. Fungsi clean_artist_string digunakan untuk membersihkan nilai pada kolom track_artist yang terkadang berbentuk string dari list. Fungsi ini memanfaatkan modul ast untuk mengubah string menjadi list Python yang sesungguhnya, lalu menggabungkan elemen-elemen dalam list tersebut menjadi satu string dengan pemisah koma. Hasil pembersihan ini disimpan ke dalam kolom baru bernama cleaned_artists.

Selanjutnya, kolom unique_song_key dibuat dengan menggabungkan nama artis yang telah dibersihkan (cleaned_artists) dengan judul lagu (track_name). Tujuan dari pembuatan kunci unik ini adalah untuk mengidentifikasi setiap lagu secara spesifik, sehingga duplikasi data dapat dihapus menggunakan fungsi drop_duplicates. Terakhir, kolom combined_features dibuat dengan menggabungkan beberapa informasi seperti cleaned_artists, playlist_genre, dan playlist_subgenre. Penggabungan fitur ini akan berguna dalam tahap pemodelan, seperti dalam pembuatan sistem rekomendasi lagu berbasis konten. Keseluruhan proses ini memastikan bahwa data yang digunakan bersih, bebas duplikasi, dan telah dikondisikan untuk analisis lanjutan.

#### Standarisasi
![image](https://github.com/user-attachments/assets/f8a5d8dd-12d2-4705-95e7-ec820185de54)

Kode tersebut menunjukkan proses standardisasi fitur numerik dalam sebuah DataFrame menggunakan StandardScaler dari pustaka sklearn.preprocessing. Pertama, ditentukan daftar fitur numerik yang ingin dinormalisasi, seperti danceability, energy, loudness, dan lainnya. Selanjutnya, fitur-fitur tersebut disalin ke dalam df_features untuk memastikan kolom yang diproses tersedia dan tidak mempengaruhi data asli. Kemudian, StandardScaler digunakan untuk menghitung rata-rata dan standar deviasi dari setiap fitur, lalu mentransformasinya agar memiliki mean = 0 dan standar deviasi = 1. Hasil transformasi ini disimpan dalam DataFrame baru X_scaled_df, dengan mempertahankan indeks berdasarkan kolom unique_song_key dan nama kolom tetap sesuai fitur aslinya. Proses ini sangat penting agar model machine learning dapat bekerja secara optimal dengan skala data yang seragam.

## Modelling
### Menerapkan Cosine Similarity
![image](https://github.com/user-attachments/assets/966332e4-8fe1-47ec-9136-7da3dc705ef9)

Kode tersebut menerapkan perhitungan cosine similarity menggunakan fungsi cosine_similarity dari modul sklearn.metrics.pairwise. Fungsi ini digunakan untuk mengukur tingkat kemiripan antara setiap pasangan lagu berdasarkan fitur numerik yang telah distandarisasi sebelumnya (X_scaled_df). Hasilnya berupa matriks simetri (cosine similarity matrix), di mana setiap elemen [i, j] merepresentasikan seberapa mirip lagu ke-i dengan lagu ke-j. Nilai cosine similarity berkisar antara -1 hingga 1, dengan nilai mendekati 1 menunjukkan kemiripan yang tinggi. Matriks ini menjadi dasar penting dalam sistem rekomendasi berbasis konten karena memungkinkan identifikasi lagu-lagu yang memiliki karakteristik akustik dan musikal serupa.

![image](https://github.com/user-attachments/assets/d880115c-e450-4b5e-b67f-7127baed9d5c)

Kode tersebut mengubah matriks hasil perhitungan cosine similarity (cos_sim_matrix) menjadi sebuah DataFrame bernama cosine_sim_df menggunakan pd.DataFrame. Baris dan kolom pada DataFrame ini diberi label berdasarkan nilai unique_song_key dari dataset asli. Hal ini bertujuan agar hasil cosine similarity lebih mudah diinterpretasikan karena setiap nilai kemiripan antar lagu dapat dilihat langsung berdasarkan identitas unik lagunya. Dengan representasi ini nantinya dapat dengan cepat menemukan lagu yang paling mirip dengan lagu tertentu berdasarkan nilai cosine similarity tertinggi.

![image](https://github.com/user-attachments/assets/4ce4d1ec-034f-4d5c-89e4-897207dc12a4)

Kode tersebut terdapat sebuah fungsi bernama recommend_by_identifier yang digunakan untuk merekomendasikan lagu-lagu serupa berdasarkan sebuah lagu acuan (song_identifier). Fungsi ini pertama-tama memeriksa apakah lagu tersebut ada dalam indeks DataFrame cosine similarity (cosine_sim_df). Jika tidak ditemukan, fungsi akan mengembalikan pesan kesalahan. Jika ditemukan, fungsi mengambil nilai kemiripan (similarity scores) antara lagu tersebut dengan semua lagu lainnya, lalu menghapus dirinya sendiri dari perbandingan agar tidak merekomendasikan lagu yang sama. Selanjutnya, nilai kemiripan diurutkan dari yang tertinggi, dan hanya top_n lagu dengan skor tertinggi yang dikembalikan sebagai hasil rekomendasi.

![image](https://github.com/user-attachments/assets/0bd99ed6-2bed-4c05-b90f-f829848e8607)

Kode tersebut menghitung matriks cosine similarity antara data lagu yang telah diskalakan (X_scaled_df), menggunakan fungsi cosine_similarity dari scikit-learn. Hasilnya disimpan dalam sebuah DataFrame bernama cosine_sim_df, di mana baris dan kolomnya diberi label berdasarkan kunci unik masing-masing lagu (unique_song_key). Matriks ini memiliki ukuran 26.229 x 26.229, yang berarti ada 26.229 lagu dan setiap elemen matriks menunjukkan tingkat kemiripan antara dua lagu berdasarkan fitur yang digunakan. Matriks ini kemudian diambil sampel acak sebagian baris dan kolomnya untuk ditampilkan sebagai contoh. 

  Output : 
  ![image](https://github.com/user-attachments/assets/a572bbbd-6a67-43fe-b39e-d98c87e28f5f)


  ## Evaluation dan Inference
  ### Inference 
  ![image](https://github.com/user-attachments/assets/a3198603-958c-4136-9d32-d9087ab92660)

Rekomendasi lagu yang mirip dengan "Alex & Sierra - Little Do You Know" menunjukkan daftar lima lagu dengan tingkat kemiripan yang tinggi, yaitu sebesar 0.98. Beberapa di antaranya adalah "Dean Lewis - Waves - Guitar Acoustic", "Ben Platt - In Case You Don't Live Forever", dan "Grace VanderWaal - I Don't Know My Name", yang semuanya dikenal dengan lirik menyentuh dan vokal yang ekspresif. Hal ini menunjukkan bahwa sistem rekomendasi bekerja dengan mempertimbangkan kesamaan dalam mood, genre, serta kualitas vokal dan instrumental.

![image](https://github.com/user-attachments/assets/09d832b0-1399-4336-8de9-0836d15f074a)

Fungsi evaluate_recommendation_metrics digunakan untuk menilai kualitas rekomendasi lagu berdasarkan sebuah lagu kueri (query_song) dengan membandingkan hasil rekomendasi dari fungsi recommend_by_identifier terhadap data kebenaran (ground truth). Fungsi ini mengambil daftar lagu yang direkomendasikan sebanyak k teratas, lalu menormalisasi judul lagu pada ground truth dan hasil rekomendasi agar mudah dibandingkan. Selanjutnya, fungsi menghitung metrik evaluasi yaitu precision, recall, dan F1-score untuk mengukur seberapa banyak lagu yang direkomendasikan sesuai dengan ground truth. Hasil evaluasi ini kemudian dikembalikan dalam bentuk dictionary yang juga menyertakan daftar lagu yang relevan ditemukan dalam rekomendasi.

![image](https://github.com/user-attachments/assets/b3bfbf26-9cae-4316-8870-e27d482bfa5a)

Kita Akan menampilkan Output tersebut dan hasilnya seperti diatas. Output tersebut menunjukkan hasil evaluasi sistem rekomendasi lagu terhadap satu lagu kueri, menggunakan metrik evaluasi Precision@5, Recall@5, dan F1-Score@5. Nilai precision, recall, dan F1-score semuanya adalah 1.0, yang berarti sistem berhasil merekomendasikan 5 lagu dan kelimanya sepenuhnya relevan dengan ground truth (daftar lagu yang benar-benar diharapkan).

Bagian 'Relevant Found' mencantumkan kelima lagu tersebut, yang semuanya cocok dengan referensi. Dengan demikian, output ini mengindikasikan bahwa sistem rekomendasi bekerja sangat akurat dan optimal dalam kasus ini, tanpa kesalahan dalam pemilihan lagu.


### Penjelasan Metrik
 1. Precision@k
    - Precision@k mengukur proporsi item relevan di antara k item teratas yang direkomendasikan oleh sistem. Dengan kata lain, dari semua item yang direkomendasikan oleh sistem, berapa banyak yang benar-benar relevan.
    ![image](https://github.com/user-attachments/assets/71774cb1-436b-4bc7-b705-a4c8839181c8)

 2. Recall@k
    - Recall@k berfungsi untuk mengukur proporsi item relevan yang ditemukan oleh sistem di antara semua item relevan yang ada dalam ground truth. Dengan kata lain, dari semua item yang seharusnya disukai pengguna, menentukan berapa banyak yang berhasil ditemukan dan direkomendasikan oleh sistem
    ![image](https://github.com/user-attachments/assets/b69ba33d-4239-4b1e-8be4-3cdbb31048c7)

 3. F1-Score@k
    - F1-Score@k adalah rata-rata harmonik dari Precision@k dan Recall@k. Metrik ini memberikan keseimbangan antara Precision dan Recall. F1-Score berguna ketika Anda ingin mengevaluasi model yang memiliki keseimbangan antara kesalahan tipe I (merekomendasikan item yang tidak relevan) dan kesalahan tipe II (gagal merekomendasikan item yang relevan).
    ![image](https://github.com/user-attachments/assets/cfd78a70-036e-478e-83f9-76725c57a9b2)


## Kesimpulan
### 1. Menentukan top 10 Lagu dari Playlist "Global Top 50 | 2020 Hits"
![image](https://github.com/user-attachments/assets/35823eeb-fb58-4ed9-967d-b601ecec4798)

Playlist "Global Top 50 | 2020 Hits" terdiri dari lagu-lagu dengan tingkat popularitas yang sangat tinggi, dipimpin oleh "Dance Monkey" dari Tones and I sebagai lagu terpopuler. Skor popularitas yang mendekati sempurna pada seluruh lagu dalam daftar mencerminkan tingginya minat pendengar global dan tingginya frekuensi pemutaran lagu-lagu tersebut di Spotify sepanjang tahun 2020. Playlist ini secara jelas merepresentasikan tren musik populer dunia pada tahun tersebut.

### 2. Menentukan 5 Genre Lagu Teratas dengan Rata-rata memiliki Popularitas Tertinggi
![image](https://github.com/user-attachments/assets/369315e6-7276-44f6-8f43-570cbb9630b5)

Analisis data menunjukkan bahwa genre pop merupakan genre dengan rata-rata popularitas tertinggi di Spotify, menandakan dominasi dan daya tariknya yang kuat di kalangan pendengar global. Diikuti oleh genre latin dan rap, yang juga menunjukkan tingkat popularitas yang tinggi dan pengaruh yang signifikan. Meskipun terdapat perbedaan skor, jarak antar rata-rata popularitas kelima genre teratas ini relatif kecil, mencerminkan preferensi musik yang beragam di antara pengguna Spotify. Hal ini menegaskan bahwa meskipun pop menjadi genre paling dominan, genre lain seperti latin, rap, rock, dan R&B tetap memiliki audiens yang kuat dan aktif.

### 3. Menentukan Korelasi antara Energy dan Popularitas Lagu
![image](https://github.com/user-attachments/assets/6cf22574-b521-45bc-bc48-2ddc202ef0b7)

terdapat korelasi negatif yang sangat lemah antara tingkat energi sebuah lagu dan popularitasnya di Spotify, dengan nilai korelasi sebesar -0.11. Hal ini menunjukkan bahwa energi lagu bukanlah faktor yang signifikan dalam menentukan seberapa populer lagu tersebut. Visualisasi scatter plot dengan garis regresi yang datar juga memperkuat bahwa tidak ada hubungan linier yang kuat antara kedua variabel. Oleh karena itu, tingkat energi lagu tidak dapat dijadikan indikator utama untuk memprediksi popularitas di kalangan pendengar.

## Referensi
1. Nijkamp, R. (2018). The relation between audio features and popularity of songs on Spotify. Undergraduate Thesis, University of Twente.
2. Smith, A., & Garcia, M. (2019). The impact of genre diversity on streaming numbers: A Spotify case study. International Journal of Music Business Research, 8(1), 23-39.
3. Huang, Y., & Kuo, C. (2020). Analyzing Music Popularity and Listener Preferences Using Spotify Data. Journal of Data Science and Music Analytics, 5(2), 45-58.

















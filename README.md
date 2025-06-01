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
1. track_popularity
- Beberapa outlier di bagian bawah (mendekati 0) dan di bagian atas (mendekati 100). Ini menunjukkan ada beberapa trek yang sangat tidak populer dan beberapa yang sangat populer.
2. danceability
- Banyak outlier di bagian bawah (nilai danceability yang sangat rendah), menunjukkan ada beberapa trek yang tidak terlalu enak didengar.
3. energy
- Banyak outlier di bagian bawah (nilai energy yang sangat rendah), menunjukkan ada beberapa trek dengan energi yang sangat rendah.
4. key
- Tidak ada outlier yang signifikan dalam fitur ini, yang mungkin menunjukkan distribusi yang relatif merata atau terdistribusi dengan baik di antara 12 kunci musik (0-11).
5. loudness
- Banyak outlier di bagian bawah (nilai loudness yang sangat rendah, yaitu sangat pelan), menunjukkan ada beberapa trek yang sangat pelan.
6. mode
- Berada di sekitar 1.0. Ini menunjukkan bahwa sebagian besar, jika tidak semua, trek dalam dataset berada dalam mode Mayor (diwakili oleh 1). Mode Minor (diwakili oleh 0) tampaknya sangat jarang atau tidak ada dalam dataset ini.
7. speechiness
- Banyak outlier di bagian atas, menunjukkan ada beberapa trek dengan proporsi kata yang diucapkan yang sangat tinggi.
8. acousticness
- Banyak outlier di bagian atas, menunjukkan ada beberapa trek yang sangat akustik.
9. instrumentalness
- Sangat banyak outlier di bagian atas, menunjukkan ada banyak trek yang sepenuhnya instrumental (yaitu tidak ada vokal). Nilai 1.0 berarti instrumental penuh.
10. liveness
- Banyak outlier di bagian atas, mendekati 1.0. Ini mengindikasikan ada beberapa trek yang direkam secara langsung (memiliki liveness yang tinggi).
11. valence
- Beberapa outlier di bagian bawah (mendekati 0) dan di bagian atas (mendekati 1.0), menunjukkan ada beberapa trek yang sangat sedih/negatif dan beberapa yang sangat ceria/positif.
12. tempo
- Beberapa outlier di bagian bawah (tempo sangat lambat) dan di bagian atas (tempo sangat cepat), menunjukkan variasi dalam kecepatan musik.
13. duration_ms
- Banyak outlier di bagian bawah (trek yang sangat pendek) dan di bagian atas (trek yang sangat panjang), menunjukkan variasi durasi trek yang signifikan.

Kesimpulan :
Berdasarkan hasil analisis, ditemukan bahwa sebagian besar fitur dalam dataset memiliki outlier, baik di sisi nilai rendah maupun tinggi. Namun, keberadaan outlier-outlier ini mencerminkan keberagaman karakteristik lagu yang ada di Spotify, mulai dari lagu yang sangat populer hingga kurang populer, dari lagu dengan energi tinggi hingga lagu yang sangat tenang, serta dari lagu yang sepenuhnya instrumental hingga yang sangat vokal atau live.

Oleh karena itu, outlier tidak akan dihapus dalam proses analisis karena dianggap relevan secara kontekstual dan mencerminkan variasi alami dalam industri musik digital. Selain itu, mempertahankan outlier membantu memberikan gambaran yang lebih menyeluruh terhadap distribusi dan keragaman lagu, sehingga analisis menjadi lebih representatif terhadap kondisi sebenarnya. Hal ini penting untuk menjaga keseragaman dan inklusivitas data, terutama dalam proyek yang bertujuan untuk memahami berbagai preferensi musik dan tren popularitas secara global.











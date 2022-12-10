# Laporan Proyek Pertama Machine Learning Terapan - Alifi Lazuardi Gunawan

## Domain Proyek

*Wine* atau dalam Bahasa Indonesia disebut anggur adalah salah satu jenis minuman yang sangat populer. Kualitas dari sebuah jenis anggur ditentukan oleh banyak faktor, seperti kandungan kimia di dalamnya yang merupakan hasil dari proses fermentasi, bahan baku, dan cara pengolahan. Saat ini telah terdapat serifikasi untuk menjamin kualitas dari anggur yang diproduksi. Sertifikasi ini dilakukan dengan menggunakan tes fisiokimia dan sensor untuk mengetahui kandungan dari anggur tersebut (Ebeler, 1999).

Perbedaan kandungan bahan kimia yang ada di dalam anggur membuat kualitas rasa yang dihasilkan berbeda pula. Salah satu ukuran untuk menentukan kulitas anggur adalah *My Wine Rating Scale* yang dibuat oleh Tim Elliott. Berikut tabel penjelasan dari *My Wine Rating Scale.*

| ***NUMERICAL RANK*** | ***WORD RANK***                      | ***COMMENTS***                                               |
| -------------------- | ------------------------------------ | ------------------------------------------------------------ |
| **10**               | ***EXCELLENT***                      | *Heitz  “MarthaÃƒÂ¢Ã¢â€šÂ¬Ã¢â€žÂ¢s Vineyard” Cabernet Sauvignon 1974 comes to mind as  the best wine I have ever had the good fortune to taste and would earn a  “10”. This rating is reserved for classic wines.* |
| **9**                | ***DELICIOUS***                      | *A wine  of complexity and distinction; the top-end of wines tasted on the show to  date.* |
| **8**                | ***VERY GOOD***                      | *Highly  recommended wine; one that I probably have in my cellar right now.* |
| **7**                | ***“QUAFFABLE”***                    | *Like  Miles says in “[Sideways](http://www2.foxsearchlight.com/sideways/)“, a well made, but ultimately  non-distinctive wine. Nothing wrong here, just not a transcendent wine  experience.* |
| **6**                | ***FAIR, BUT HAS NOTICEABLE FLAWS*** | *A  drinkable wine, but one that is not recommended due to winemaking problems or  thin fruit flavors.* |
| **5**                | ***PRETTY BAD***                     | *A wine  that is on the verge of being undrinkable; avoid!*  |
| **1-4**              | ***UNDRINKABLE***                    | *I would  demand a refund should I have the bad fortune to taste a wine that rates a 4  or below.* |

Berdasarkan permasalahan di atas penulis ingin membuat sebuah sistem klasifikasi anggur secara otomatis berdasarkan kandungan fisiokimia di dalam anggur untuk mempermudah klasifikasi kualitas anggur. 

## Business Understanding

### a. Rumusan Masalah

1. Bagaimana proses *preprocessing* dari data untuk membuat model yang baik?
2. Bagaimana cara penerapan model *Random Forest Classifier* dalam melakukan klasifikasi data?
3. Apa saja fitur yang berpengaruh dalam proses klasifikasi? 

### b. Tujuan

1. Mengetahui proses *preprocessing* dari data untuk membuat model yang baik.
2. Melakukan penerapan model *Random Forest Classifier* dalam melakukan klasifikasi data.
3. Mendapatkan fitur berpengaruh dalam proses klasifikasi.

### c. Pernyataan solusi

1. Untuk memperisapkan data agar dapat dikenali model dengan baik dilakukan beberapa tahapan yaitu:

   a. Mengapus kolom 'Id'

   b. Melakukan *oversampling*

   c. Melakukan *scaling data*

   d. Membagi data menjadi data latih dan data uji

2. Dalam proyek ini akan dignakan algoritma *Random Forest Classifier. Random Forest Classifier* adalah algoritma *machine learing* berbasis *decision tree*. *Random Forest Classifier* membuat banyak *decision tree* yang dilatih kemudian mengkombinasikannya untuk mendapatkan akurasi yang baik. Dengan menggunakan algoritma ini juga dapat diketahui seberapa berpengaruh sebuah fitur terhadap kelas dari data. Algoritma *Random Forest Classifier* sudah tersedia dalam *library sklearn*. Selain itu dalam proyek ini juga menggunakan *GridSearchCV* untuk mencari *hyperparameter* terbaik.

3. Fitur yang paling berpengaruh akan dicari menggunakan fungsi feature_importances



## Data Understanding

Data yang digunakan dalam proyek ini  adalah data  *Wine Quality Dataset* yang berasal dari Kaggle. Data ini berisi kualitas dari  anggur merah "*Vinho Verde*"  dari Portugal berdasarkan kandungan bahan kimia di dalam anggur. Bahan kimia tersebut antara lain alkohol, asam, gula, dan sulfur. Data ini dapat diakses pada tautan berikut [Wine Quality Dataset | Kaggle](https://www.kaggle.com/datasets/yasserh/wine-quality-dataset) 

### a. Variabel-Variabel Dari Dataset

Variabel beradasarakan output pengamatan (sensor data):

* *fixed acidity* : Kandungan asam non volatil seperti asam sitrat, malat, dan tartarat yang menyebabkan rasa asam pada anggur. Jenis asam ini memadukan keharmonisan rasa anggur dan menambah kesegaran.

* *volatile acidity* : kandungan asam volatil (atau gas) dalam anggur. Asam volatil utama dalam anggur adalah asam asetat, yang memberi bau dan rasa cuka.

* *citric acid* : kandungan asam sitrat, salah satu asam yang kurang umum ditemukan dalam anggur. Asam adalah senyawa organik lemah yang umumnya ditemukan dalam jumlah besar dalam buah jeruk seperti jeruk dan limau. Jumlah asam sitrat yang ditemukan dalam anggur kecil, masih mencapai 5% dari total kandungan asam dalam anggur.

* *residual sugar* : kadar gula anggur alami yang tersisa dalam anggur setelah fermentasi alkohol selesai. Semakin banyak sisa gula yang tersisa dalam anggur, semakin manis anggur itu.

* *chlorides* : jumlah mineral dalam anggur juga memengaruhi strukturnya. Konten mereka sebagian besar dipengaruhi oleh wilayah iklim, prosedur,  penyimpanan anggur, dan penuaan.

* *free sulfur dioxide* : kandungan sulfur dioksida yang ditambahkan. Dalam industri anggur, sulfur dioksida (SO2) sering ditambahkan ke must dan jus sebagai pengawet untuk mencegah pertumbuhan bakteri dan memperlambat proses oksidasi dengan menghambat enzim oksidatif.

* *total sulfur dioxide* : Total bagian dari SO2 yang bebas dalam anggur ditambah bagian yang terikat dengan bahan kimia lain dalam anggur seperti aldehida, pigmen, atau gula. kerapatan: massa satuan volume suatu zat material. Rumus kerapatan adalah d = M/V, di mana d adalah kerapatan, M adalah massa, dan V adalah volume.

* pH : Derajat keasaman dari anggur. Kisaran pH optimal untuk semua anggur adalah antara 2,9 dan 4,2. Anggur yang lebih asam memiliki nilai pH yang lebih rendah; anggur yang kurang asam memiliki nilai pH yang lebih tinggi.

* *sulphates* : Kandungan Sulfat yang merupakan produk sampingan dari gula anggur yang difermentasi oleh ragi menjadi alkohol.

* *alcohol* : kandungan alkohol dalam anggur. Persentase alkohol anggur dipengaruhi oleh berbagai faktor, termasuk varietas anggur, kandungan gula beri, metode pembuatan, dan lingkungan pertumbuhan.

  Variabel target :

* *quality* : skor antara 0-10. Semakin tinggi skor kualitas anggur semakin bagus sesuai dengan *My Wine Rating Scale*.

### b. Analisis data

#### 1. Analisis deskriptif

| index | fixed acidity     | volatile acidity   | citric acid         | residual sugar     | chlorides           | free sulfur dioxide | total sulfur dioxide | density               | pH                  | sulphates          | alcohol            | quality            | Id                 |
| ----- | :---------------- | ------------------ | ------------------- | ------------------ | ------------------- | ------------------- | -------------------- | --------------------- | ------------------- | ------------------ | ------------------ | ------------------ | ------------------ |
| count | 1143.0            | 1143.0             | 1143.0              | 1143.0             | 1143.0              | 1143.0              | 1143.0               | 1143.0                | 1143.0              | 1143.0             | 1143.0             | 1143.0             | 1143.0             |
| mean  | 8.311111111111112 | 0.5313385826771653 | 0.2683639545056868  | 2.5321522309711284 | 0.0869326334208224  | 15.615485564304462  | 45.91469816272966    | 0.9967304111986001    | 3.3110148731408575  | 0.6577077865266842 | 10.442111402741034 | 5.657042869641295  | 804.9693788276466  |
| std   | 1.74759501716954  | 0.1796331930225245 | 0.19668585234821898 | 1.3559174666826799 | 0.04726733795238057 | 10.250486123430822  | 32.78213030734311    | 0.0019250671302545696 | 0.15666405977275194 | 0.1703987144670741 | 1.0821956098890875 | 0.8058242481000952 | 463.99711629510614 |
| min   | 4.6               | 0.12               | 0.0                 | 0.9                | 0.012               | 1.0                 | 6.0                  | 0.99007               | 2.74                | 0.33               | 8.4                | 3.0                | 0.0                |
| 25%   | 7.1               | 0.3925             | 0.09                | 1.9                | 0.07                | 7.0                 | 21.0                 | 0.99557               | 3.205               | 0.55               | 9.5                | 5.0                | 411.0              |
| 50%   | 7.9               | 0.52               | 0.25                | 2.2                | 0.079               | 13.0                | 37.0                 | 0.99668               | 3.31                | 0.62               | 10.2               | 6.0                | 794.0              |
| 75%   | 9.1               | 0.64               | 0.42                | 2.6                | 0.09                | 21.0                | 61.0                 | 0.997845              | 3.4                 | 0.73               | 11.1               | 6.0                | 1209.5             |
| max   | 15.9              | 1.58               | 1.0                 | 15.5               | 0.611               | 68.0                | 289.0                | 1.00369               | 4.01                | 2.0                | 14.9               | 8.0                | 1597.0             |

​		Berdasarkan analisis deskriptif di atas diperroleh hasil berupa :

​		a. Sample berjumlah 1143 data	

​		b. Rentang dari tiap fitur dalam data masih berbeda

​		c. Quality yang merupakan target mempunyai rentang dari 3-8

#### 2. Pengecekan missing value dan data duplikat

​		a. Pengecekan missing value 

Untuk mengecek value difunakan fungsi isna(). Fungsi ini akan menegembalikan nilai apabila terdapat null value. Selanjutnya dilakukan penjumlahan dengan fungsi sum() untuk menjumlahkan nilai null pada tiap kolom/fitur 

```
fixed acidity           0
volatile acidity        0
citric acid             0
residual sugar          0
chlorides               0
free sulfur dioxide     0
total sulfur dioxide    0
density                 0
pH                      0
sulphates               0
alcohol                 0
quality                 0
Id                      0
dtype: int64
```

​			Tidak ada missing value yang ditemukan

​		b. Pengecekan data duplikat

Pengecekan duplikat dilakukan dengan menggunakan fungsi duplicated(). Fungsi ini akan mengembalikan nilai apabila terdapat nilai duplikat. Selanjutnya dilakukan penjumlahan dengan menggunakan fungsi sum() untuk mendapatkan total dari nilai duplikat.

```
0
```

​			Tidak terdapat data duplikat

#### 3. Visualisasi data

​		a. Visualisasi banyaknya data dalam tiap kelas quality

Visualisasi menggunakan libary seaborn dengan fungsi countplot(). Fungsi ini akan menghitung banyaknya data dalam tiap kelas. Jadi visualisasi dilakukan pada kolom quality dan akan menampilkan jumlah data pada setiap kelas.

![KELAS](https://user-images.githubusercontent.com/68947748/201933085-caae6808-b9c6-44ad-9a40-41ca8c224591.png)

Berdasarkan visualisasi di atas dikatahui bahwa terjdi imbalance pada data. Imbalance adalah kondisi dimana data pada kelas tertentu mempunyai jumlah jauh lebih banyak dari kelas yang lain. Akibat dari imbalance data bagi model machine learning adalah model seolah olah akan mempunyai akurasi yang biak, tetapi nyatanya model tidak dapat memprediksi data dengan kelas mempunyai sedikit data.

​		b. Korelasi antar fitur

Visualisasi menggunakan library seaborn dengan fungsi hatmap(). Dalam visualisasi ini akan menampilkan kekuatan korelasi antar fitur di dalam dataset dengan rentang nilai -1 sampa 1. Semakin mendekati nilai 1 atau -1 berarti korelasi semakin kuat.

![heatmap](https://user-images.githubusercontent.com/68947748/201933251-4e3a5d91-d3ca-4866-8739-38abcf668fca.png)

Korelasi antara fitur dengan quality

```
quality                 1.000000
alcohol                 0.484866
sulphates               0.257710
citric acid             0.240821
fixed acidity           0.121970
Id                      0.069708
residual sugar          0.022002
pH                     -0.052453
free sulfur dioxide    -0.063260
chlorides              -0.124085
density                -0.175208
total sulfur dioxide   -0.183339
volatile acidity       -0.407394
Name: quality, dtype: float
```

Terdapat korelasi positif yang kuat antara kualitas dengan kadar alkohol. Sementara itu terdapat korelasi negatif yang kuat antara kualitas dan volatile acidity. Korelasi yang kuat baik positif maupun negatif menunjukkan fitur tersebut berpengaruh besar terhadap kelas dari quality

## Data Preparation

### a. Menghapus kolom 'Id'

Kolom 'Id' bukan merupakan fitur dari data. Kolom ini lebih baik dihapus dari data. Penghapusan kolom dilakukan dengan menggunakan fungsi drop.

### b. Memisahkan fitur dan target

Melakukan pemisahan fitur dan target dari data menjadi dua variabel berbeda. Variabel features diperoleh dengan menghapus kolom quality dengan perintah drop. Sedangkan variabel target diperoleh dengan mengambil kolom quality dari data.

### c. Melakukan *oversample* untuk mengatasi *imbalance* data

Imbalance data dapat diatasi dengan melakukan *oversample*. Tahapan ini dilakukan dengan menggunakan bantuan dari *library SMOTE*. Variable oversample digunakan untuk menampung funsi smote(). Untuk mengaplikasikan fungsi ini digunakan perintah fit_resample(). Hasil dari oversample ini akan ditampung salam variabel X dan Y.

![kelas oversample](https://user-images.githubusercontent.com/68947748/201933247-2d866c06-2552-4b52-901b-014a92c1cfb7.png)

Kondisi data setelah dilakukan *oversample*

### d. Melakukan *Min-Max Scaler* 

*Min-Max Scaler* digunakan untuk menyamakan rentang value pada setiap fitur data menjadi 0-1. Tahapan ini dilakukan dengan menggunakan bantuan dari *library* *MinMaxScaler*. Untuk mengaplikasikan fungsi ini terlebih dahulu disimpan di variabel *scaler*. Kemudian digunakan fungsi fit_transform untuk mengaplikasikan fungsi. 



### e. Melakukan pembagian data menjadi data latih dan data test

Tahap ini dilakukan dengan menggunakan bantuan dari *library* *train_test_split*. Dalam proyek ini data akan dibagi menjadi 80% data latih dan 20% data validasi. Fungsi yang digunakan adalah train_test_split dan akan ditampung di dalam X_train, X_val, Y_train, dan Y_val.

## Modeling

Dalam model ini digunakan *Random Forest Classifier*. *Random Forest Classifier* adalah algoritma *machine learing* berbasis *decision tree*. *Random Forest Classifier* membuat banyak *decision tree* yang dilatih kemudian mengkombinasikannya untuk mendapatkan akurasi yang baik. Dengan menggunakan algoritma ini juga dapat diketahui seberapa berpengaruh sebuah fitur terhadap kelas dari data.

Algoritma *Random Forest Classifier* disimpan di dalam variabel. Selanjutnya dibuat array yang berisi parameter yang akan diujikan untuk mendapatakan performa terbaik. Parameter yang diuji adalah *n_estimatros, max_features, max_depth*, dan *criterion*. Selanjutnya digunakan Fungsi GridSearchCV() yang akan menlatih model dengan tiap parameter dalam array. 

Parameter terbaik yang diperoleh dari *GridSearchCV*

```
{'criterion': 'gini', 'max_depth': 8, 'max_features': 'auto', 'n_estimators': 200}
```

Tahap selanjutnya adalah melatih model dengan menggunakan parameter terbaik yang diperoleh. Untuk melatih model digunakan fungsi fit() dengan parameter data latih dan label latih.

## Evaluation

Berdasarkan prediksi yang dilakukan model, diperoleh hasil sebagai berikut

```
              precision    recall  f1-score   support

           3       0.92      1.00      0.96        82
           4       0.88      0.90      0.89        88
           5       0.63      0.60      0.62        73
           6       0.58      0.43      0.49        68
           7       0.85      0.89      0.87        84
           8       0.90      1.00      0.95        70

    accuracy                           0.82       465
   macro avg       0.79      0.80      0.80       465
weighted avg       0.80      0.82      0.81       465
```

- Model menghasilkan akurasi yang cukup baik yaitu sebesar 82%. Akurasi adalah perbandingan nilai yang diprediksi dengan benar dibagi ground truth/fakta sebenarnya dari data. Hal ini berarti model berhasil memprediksi data sesuai dengan kelas targetnya sebesar 82% dari total data.

- *Precision* adalah perbandingan antara data kelas a dengan banyaknya data yang diprediksi mempunyai kelas a. *Recall* adalah perbandingan data kelas a dengan data yang sebenarnya mempunyai kelas a. 

  ![img](https://miro.medium.com/max/320/0*fD_fCLwvjNnp2Nel)

  

![img](https://miro.medium.com/max/272/0*jnTAutFpHEVqqBHJ)

- *F1 Score* adalah harmonic mean dari precision dan recall. Nilai *F1 Score* yang tinggi mengindikasikan model mempunyai precision dan recall yang baik

  

  ![img](https://miro.medium.com/max/422/0*RdOj9EZ6TbVmwWmi)
  
  Berdasarkan prediksi yang dilakukan model, model telah mampu melakukan klasifikasi dengan baik. hal ini dapat dilihat dari nilai F1 Score yang cukup tinggi. Akan tetapi, terdapat satu kelas data dengan nilai F1 Score paling rendah yakni Kelas 6. Hal ini mengindikasikan model mengalami kegagalan dalam menemukan ciri dari Kelas 6. Akibatnya model melakukan kesalahan prediksi baik itu false positif maupun false negatif.
  
  Fitur yang paling berpengaruh dalam menentukan kelas/kualitas dari anggur adalah kandungan alcohol, sulphate, dan volatile acidity. Berikut adalah visualisasi dari fitur yang berpengaruh dalam klasifikasi.
  
  ![fitur](https://user-images.githubusercontent.com/68947748/201933241-3fe478cf-261d-40e4-9670-d075bb467304.png)

## Kesimpulan

*Preprocessing* data dilakukan untuk mempersiapkan data agar dapat dikenali model dengan baik. *Preprocessing* data dapat dilakukan sesuai dengan keadaan data. Dalam proyek ini *preprocessing* data dilakukan dengan menerapkan *oversampling* untuk mengatasi kelas yang tidak seimbang dalam data. Selanjutnya dilakukan *scaling* pada data untuk menyamakan rentang pada data menjadi antara 0-1. Tahap terakhir adalah membagi data menjadi data latih dan data validasi.

Penerapan algoritma *Random Forest classifier* dilakukan dengan menggunakan *GridSearchCV*. Dengan menggunakan *GridSearchCV* beberapa nilai dari parameter dapat diuji untuk mencari perpaduan parameter terbaik. Hasilnya diperoleh parameter terbaik berupa *criterion = 'gini', max_depth = 8, max_features = 'auto',* dan *n_estimators = 200*. Parameter ini kemudian digunakan untuk melatih model. Hasilnya diperoleh model dengan akurasi 82%. Hal ini berarti model cukup baik dalam mengenali data.

Fitur yang paling berpengaruh dalam menentukan kualitas dari anggur adalah *alcohol, sulphates,* dan *volatile acidity*. Fitur terbaik ini sama dengan korelasi yang diperoleh sebelumnya. Fitur *alcohol* dan *sulphates* memiliki korelasi positif berarti semakin banyak nilai dari *alcohol* dan *sulphates* akan membuat kulitas anggur semakin baik. Sementara itu *volatile acidity* mempunyai korelasi negatif, yang berarti semakin sedikit kandungan *volatile acidity* kualitas anggur semakin baik.

## Daftar Referensi

Anon., 2022. *Mengenal Algoritma Random Forest.* [Online]  
  Available at: https://algorit.ma/blog/cara-kerja-algoritma-random-forest-2022
  [Accessed 14 November 2022].

Cicchetti, D. V.  & Cicchetti, A. F., 2009. Wine rating scales: Assessing their utility. *International  Journal of Wine Research,* Volume I, pp. 73-83.

Ebeler, S. E.,  1999. Linking Flavor Chemistry to Sensory Analysis of Wine. *Flavor  Chemistry,* Volume I, pp. 409-422.

Er, Y. & Er,  Y., 2016. The Classification of White Wine and Red Wine According to Their  Physicochemical Qualities. *International Journal of Intelligent Systems  and Applications in Engineering,* Volume I, pp. 23-26.

Fikri, R., 2020. *Handling  Imbalanced Dataset.* [Online] 
  Available at: https://medium.com/@rusnandifikri96/handling-imbalanced-dataset-260378b2a21b
  [Accessed 13 November 2022].

Setiawan, S.,  2020. *Membicarakan Precision, Recall, dan F1-Score.* [Online] 
  Available at: https://stevkarta.medium.com/membicarakan-precision-recall-dan-f1-score-e96d81910354
  [Accessed 14 November 2022].

 
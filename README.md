# Analisis dan Klasifikasi Data Teks E-commerce
Di proyek ini akan dilakukan analisis data teks dari e-commerce dan membuat model machine learning untuk melakukan klasifikasi dari data teks tersebut.

## Pendahuluan
* Ecommerce (perdagangan elektronik) semakin marak di era digitalisasi ini. Dengan ecommerce, semua orang memiliki akses untuk masuk ke dalamnya akan lebih mudah untuk melakukan aktivitas jual beli barang maupun jasa. Sehingga semakin lama, produk yang dijual di ecommerce akan semakin besar dan sulit untuk dikendalikan.
* Dengan teknologi machine learning, data-data produk yang terdapat di dalam ecommerce akan dengan mudah dikendalikan dengan memberikan label pada produk-produk tersebut secara otomatis.

<p align="center">
  <img src="https://static.vecteezy.com/system/resources/previews/001/871/349/non_2x/illustration-of-shopping-and-spending-money-with-e-commerce-apps-own-your-own-shop-with-e-commerce-find-the-right-item-with-online-shops-landing-page-template-for-web-websites-site-banner-flyer-free-vector.jpg" alt="Ecommerce" width="500">
  <figcaption align="center">Ecommerce (Sumber: vecteezy/naki-sama)</figcaption>
</p>

Data yang digunakan pada proyek ini diperoleh dari [kaggle](https://www.kaggle.com/datasets/saurabhshahane/ecommerce-text-classification).

Data terdiri dari puluhan ribu teks dari ecommerce beserta label dari tiap teks tersebut.

## Tahap-Tahap Project
Terdapat 7 tahap yang dilakukan secara garis besar pada project ini, yaitu:

### 1. Persiapan package/library dan data
Meliputi import library yang dibutuhkan seperti pandas, numpy, hingga tensorflow.

Kemudian mengambil data dari sumbernya. Pada project ini, data teks ecommerce diambil dari [kaggle](https://www.kaggle.com/datasets/saurabhshahane/ecommerce-text-classification).

Data mentah ini terdiri 50245 baris dan memiliki 4 kategori yang biasa ada di ecommerce, yaitu:
1. household (barang rumah tangga)
2. clothing & accessories (pakaian & aksesoris)
3. books (buku)
4. electronics (barang elektronik)

### 2. Data Cleansing.
Proses membersihkan data dari semua kesalahan-kesalahan yang mungkin terjadi, termasuk kesalahan dalam penginputan data, duplikat, atau data yang tidak valid.

### 3. Text Preprocessing
Tindakan yang digunakan untuk mempersiapkan teks agar dapat digunakan dalam analisis atau pemrosesan. Pada project ini, terdapat 4 tindakan, yaitu:
3.1. Case folding, yaitu mengubah semua huruf menjadi huruf kecil.
3.2. Menghapus tanda baca.
3.3. Menghapus stopword atau kata-kata yang sering muncul namun tidak memiliki makna yang signifikan.
3.4. Tokenizing, yaitu memecah teks menjadi kata-kata atau token-token.

### 4. Exploratory Data Analysis (EDA)
Di tahap ini, akan dilakukan analisis data teks.
Pertama akan dilihat sebaran jumlah data pada tiap label.

![image](https://user-images.githubusercontent.com/115754250/211972088-2dc96208-38f1-4b77-a26d-166b1cbc0a0f.png)

Kemudian akan diperiksa statistika jumlah kata pada tiap label baik sebelum preprocessing maupun setelah preprocessing.

![image](https://user-images.githubusercontent.com/115754250/211972279-9407d984-da6c-45fe-9726-534d5bc49a51.png)
![image](https://user-images.githubusercontent.com/115754250/211972320-5424ef99-96b6-4a24-8c3e-02b3dd88c4bc.png)
![image](https://user-images.githubusercontent.com/115754250/211972358-a144ae28-628f-4a04-887e-b7e45d1be94e.png)

Selanjutnya akan dibuat visualisasi word cloud.

Visualisasi word cloud adalah sebuah representasi grafis dari kata-kata yang muncul dalam suatu teks atau dokumen. Word cloud menunjukkan frekuensi kata-kata yang muncul dalam teks dengan menggunakan ukuran font yang berbeda. Kata-kata yang muncul lebih sering ditampilkan dengan ukuran font yang lebih besar, sedangkan kata-kata yang muncul lebih jarang ditampilkan dengan ukuran font yang lebih kecil. Tujuan dari visualisasi word cloud ini adalah untuk memberikan gambaran umum tentang topik atau tema dari suatu teks atau dokumen.

![image](https://user-images.githubusercontent.com/115754250/211972931-5509e9da-0e93-4aca-b63f-ff03ef9fc6a0.png)

Dari visualisasi di atas, terlihat:
* pada label Household kata yang paling mencolok adalah *stainless* dan *steel*
* pada label Books kata yang paling mencolok *book*, *author*, *review*, dan *life*
* pada label Clothing & Accessories kata yang paling mencolok adalah *women*, *men*, *style*, *product*, dan *black*
* pada label Electronics kata yang paling mencolok adalah *feature*, *device*, *support*, dan *camera*

Kata-kata yang paling mencolok tersebut menunjukan kata-kata yang paling sering muncul pada tiap label.

### 5. Data Splitting
Memisahkan antara data latih dan data validasi.
Data latih sebesar 80% dari data asli.
Data validasi sebesar 20& dari data asli.

### 6. Pembuatan Model Machine Learning dan Evaluasi Performa
Model yang akan digunakan adalah Bidirectional LSTM dengan konfigurasi sebagai berikut:
* 1 BiLSTM Layer dengan jumlah hidden state 16 dan dropout 0,5
* 1 Dense Layer dengan jumlah hidden state 32 dan dropout 0,5 serta fungsi aktivasi relu
* Output Layer dengan fungsi aktivasi softmax
* Optimizer Adam
* Learning rate = 0,001
* Epochs = 10, namun jika akurasi validasi telah mencapai lebih dari 95%, proses pelatihan akan langsung berhenti
* Batch size = 512

![image](https://user-images.githubusercontent.com/115754250/211973702-be3909a1-6913-4a00-aa6b-3d793f8cc7dc.png)

Setelah akurasi validasi mencapai 95% atau lebih, proses pelatihan akan otomatis berhenti.

![image](https://user-images.githubusercontent.com/115754250/211973857-24d00d5a-48a0-4159-a028-a49027bd0f65.png)

Pada project ini, diperoleh akurasi validasi sebesar **95,2%** pada epoch ke delapan.

### 7. Simpan Model
Model disimpan dalam format model.h5 dan konversinya dalam format tensorflow.js agar bisa dilakukan deployment model ke dalam website.

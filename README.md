# Final Project
## Teknologi Komputasi Awan
### Kelompok C5
|Nama|NRP |
|--|--|
|Raditya Hardian Santoso|5027231033|
|Fiorenza|50272310|
|Harwinda|50272310|
|Nayyara Ashila|50272210|
## Permasalahan
Anda adalah seorang lulusan Teknologi Informasi, sebagai ahli IT, salah satu kemampuan yang harus dimiliki adalah Keampuan merancang, membangun, mengelola aplikasi berbasis komputer menggunakan layanan awan untuk memenuhi kebutuhan organisasi.

Pada suatu saat anda mendapatkan project untuk mendeploy sebuah aplikasi Sentiment Analysis dengan komponen Backend menggunakan python: sentiment-analysis.py dengan spesifikasi sebagai berikut
## Endpoints:
1. **Analyze Text**

   - **Endpoint:** `POST /analyze`
   - **Description:** This endpoint accepts a text input and returns the sentiment score of the text.
   - **Request:**
     ```json
     {
       "text": "Your text here"
     }
     ```
   - **Response:**
     ```json
     {
       "sentiment": <sentiment_score>
     }
     ```

2. **Retrieve History**
   - **Endpoint:** `GET /history`
   - **Description:** This endpoint retrieves the history of previously analyzed texts along with their sentiment scores.
   - **Response:**
     ```json
     {
      {
        "text": "Your previous text here",
        "sentiment": <sentiment_score>
      },
      ...
     }
     ```

---

Kemudian juga disediakan sebuah Frontend sederhana menggunakan [index.html](/Resources/FE/index.html) dan [styles.css](/Resources/FE/styles.css) dengan tampilan antarmuka sebagai berikut

<img width="1186" alt="image" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/137570361/d74da3ed-30f7-49ef-b4a3-8b36bda62ade">

Kemudian anda diminta untuk mendesain arsitektur cloud yang sesuai dengan kebutuhan aplikasi tersebut. Apabila dana maksimal yang diberikan adalah **1 juta rupiah per bulan (65 US$)**
konfigurasi cloud terbaik seperti apa yang bisa dibuat?
## Rancangan Arsitektur dan Tabel Harga Spesifikasi VM
Sebelum kami menggunakan Digital Ocean, kami sebenarnya memutuskan untuk menggunakan Google Cloud Platform. Namun, karena terjadi kendala saat pengujian endpoint yang membutuhkan izin firewall yang kami masih belum bisa troubleshoot, kami memutuskan untuk berpindah platform cloud ke Digital Ocean.

Kenapa kami memilih Digital Ocean? Karena untuk UI dan UX, Digital Ocean yang paling ramah pemula, serta jika terhubung dengan Github Education kami bisa mendapat credit gratis. Selain itu, untuk troubleshooting jika ada masalah lebih mudah karena komunitasnya lebih ramah untuk pemula dan mudah dipahami.

**Berikut adalah rancangan arsitektur yang akan kami buat:**


**Harga perkiraan yang akan kami pakai adalah seperti berikut:**

## Hasil Pengujian Setiap Endpoint

### Pengujian dengan Thunder Client

1. Get All History



2. Create a New Text



### Pengujian dari Web





## Hasil Pengujian dan Analisis Loadtesting Locust

- RPS Maksimum (load testing 60 detik)

> **RPS Maksimum yang kami dapati dari beberapa stress test locust adalah 149 RPS, didapatkan ketika di test dengan menggunakan spawn rate 500 dengan Peak Concurrency Maksimum sebesar 2000 User**

- Peak Concurrency Maksimum (spawn rate 50, load testing 60 detik)



- Peak Concurrency Maksimum (spawn rate 100, load testing 60 detik)



- Peak Concurrency Maksimum (spawn rate 200, load testing 60 detik)



- Peak Concurrency Maksimum (spawn rate 500, load testing 60 detik)



## Kesimpulan dan Saran





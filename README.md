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

## Langkah-Langkah Pengerjaan
### Resources yang dibutuhkan
1. buat 1 droplet yang bernama frontend
2. buat 1 droplet yang bernama backend
3. buat mongo database bernama db-mongodb
4. buat 1 load balancer, pastikan saat membuat loadbalancer, health-check diganti menjadi TCP)
### Langkah-langkah untuk droplet frontend
1. ssh ke droplet frontend
2. sudo apt-get update
3. sudo apt-get install apache2 
4. cd /var/www/html, ls 
5. download index.html dan styles.css yang terdapat pada github
    1. wget -O index.html https://raw.githubusercontent.com/fuaddary/fp-tka/main/Resources/FE/index.html
    2. wget -O styles.css https://raw.githubusercontent.com/fuaddary/fp-tka/main/Resources/FE/styles.css
6. Di index.html, ganti fetch api menjadi /analyze dan /history
7. cd /etc/apache2/sites-available
8. nano 000-default.conf, tambahkan konfigurasi proxy
9. sudo a2enmod proxy, sudo a2enmod proxy_http
10. systemctl restart apache2 untuk restart servicenya
11. tampilan frontend dapat diakses melalui IP address frontend-01 atau IP address load-balancer 
### Langkah-langkah untuk droplet backend
1. ssh ke droplet backend-02
2. sudo apt-get update
3. sudo apt-get install python 3
4. install dependencies :
    1. sudo apt-get install python3-pip
    2. pip install flask
    3. pip install flask_cors
    4. pip install textblob
    5. pip install pymongo
    6. pip install gunicorn
5. tambahkan file sentiment-analysis.py sesuai pada github 
    1. wget -O sentiment-analysis.py https://raw.githubusercontent.com/fuaddary/fp-tka/main/Resources/BE/sentiment-analysis.py
6. ubah client pada file tersebut menjadi link database pada connection details db-mongodb
7. run dengan command python3 sentiment-analysis.py atau bisa juga run secara daemon dengan command gunicorn -b 0.0.0.0:80 -w 4 -D sentiment-analysis:app
8. akses ke IP Address load balancer

## Hasil Pengujian Setiap Endpoint

### Pengujian dengan Thunder Client

1. Get All History



2. Create a New Text



### Pengujian dari Web





## Hasil Pengujian dan Analisis Loadtesting Locust

- RPS Maksimum (load testing 60 detik)


- Peak Concurrency Maksimum (spawn rate 50, load testing 60 detik)



- Peak Concurrency Maksimum (spawn rate 100, load testing 60 detik)



- Peak Concurrency Maksimum (spawn rate 200, load testing 60 detik)



- Peak Concurrency Maksimum (spawn rate 500, load testing 60 detik)



## Kesimpulan dan Saran





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
1. Buat 2 droplet yang bernama frontend-01 
2. ⁠Buat 2 droplet yang bernama backend-02 dan backend-03
3. ⁠Buat mongo database bernama db-mongodb
3. ⁠Buat 1 load balancer, koneksikan dengan 3 droplet yang telah dibuat
### Langkah-langkah untuk droplet frontend-01
1. ⁠Ssh ke droplet frontend-01 
2.⁠ ⁠⁠Sudo apt-get update
3.⁠ ⁠⁠Sudo apt-get install apache2 
4.⁠ ⁠⁠Cd /var/www/html, ls 
5.⁠ ⁠⁠Download index.html dan styles.css yang terdapat pada github
6.⁠ ⁠Di index.html, ubah localhost:5000 analyze menjadi IPAddressBackend-02:5000 dan localhost:5000 history menjadi IPAddressBackend-02:5000
7.⁠ ⁠⁠systemctl restart apache2 untuk restart servicenya
8.⁠ ⁠Tampilan frontend dapat diakses melalui IP address frontend-01 atau IP address load-balancer
### Langkah-langkah untuk droplet backend-02
1. SSH ke droplet backend-02
2. ⁠Sudo apt-get update
3. ⁠Sudo apt-get install python 3
4. ⁠Install dependencies :
- Sudo apt-get install python3-pip
- ⁠pip install flask
- ⁠pip install flask_cors
- ⁠pip install textblob
- ⁠pip install pymongo
- ⁠pip install gunicorn
5. Tambahkan file sentiment-analysis.py sesuai pada github 
6. ⁠ubah client pada file tersebut menjadi link database pada connection details db-mongodb
7. ⁠run dengan command python3 sentiment-analysis.py atau bisa juga run secara daemon dengan command gunicorn -b 0.0.0.0:5000 -w 4 -D sentiment-analysis:app
8. ⁠Akses ke IP Address load balancer
### Langkah-langkah untuk droplet backend-03
1. SSH ke droplet backend-03
2. ⁠Sudo apt-get update
3. ⁠Sudo apt-get install python 3
4. ⁠Install dependencies :
- Sudo apt-get install python3-pip
- ⁠pip install flask
- ⁠pip install flask_cors
- ⁠pip install textblob
- ⁠pip install pymongo
- ⁠pip install gunicorn
5. Tambahkan file sentiment-analysis.py sesuai pada github 
6. ⁠ubah client pada file tersebut menjadi link database pada connection details db-mongodb
7. ⁠run dengan command python3 sentiment-analysis.py atau bisa juga run secara daemon dengan command gunicorn -b 0.0.0.0:5000 -w 4 -D sentiment-analysis:app
8. ⁠Akses ke IP Address load balancer

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





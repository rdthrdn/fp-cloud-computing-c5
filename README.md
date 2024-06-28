<img width="1440" alt="Screenshot 2024-06-29 at 02 16 56" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/75177c59-57c3-4e93-a7e0-afb6c04dba43"># Final Project
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
![Group 78](https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/599f7661-658e-4852-b595-9b8f0433006c)
**Harga perkiraan yang akan kami pakai adalah seperti berikut:**
<img width="1440" alt="Screenshot 2024-06-28 at 22 26 49" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/389a5612-e49a-4173-b311-2704e0df7a48">

## Langkah-Langkah Pengerjaan
### Resources yang dibutuhkan
   1. buat 1 droplet yang bernama frontend
      <img width="1440" alt="Screenshot 2024-06-28 at 22 51 03" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/2944cd96-7b4d-45c9-b5f4-b1d723a517f1">
   2. buat 1 droplet yang bernama backend
      <img width="1440" alt="Screenshot 2024-06-28 at 22 50 47" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/05f3b5e7-2282-4bc9-ae4d-aa6bd0c12381">
   3. buat mongo database bernama db-mongodb
      <img width="1440" alt="Screenshot 2024-06-29 at 02 09 31" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/6a979d8d-9ea4-487d-bc4e-3fc256153d05">
   4. buat 1 load balancer, pastikan saat membuat loadbalancer, health-check diganti menjadi TCP)
      <img width="1440" alt="Screenshot 2024-06-28 at 23 05 46" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/da6d0b4d-bd26-4f57-b480-0fdd5fa2a3f8">
### Langkah-langkah untuk droplet frontend
   1. ssh ke droplet frontend
      <img width="1440" alt="Screenshot 2024-06-28 at 23 11 08" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/98170e73-6314-4e7a-b3d4-840bb2feca2c">
   2. ``sudo apt-get update``
      <img width="1440" alt="Screenshot 2024-06-28 at 23 11 36" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/466319e8-6168-4c67-a41a-e3992fdec7fc">
   3. ``sudo apt-get install apache2``
      <img width="1440" alt="Screenshot 2024-06-28 at 23 12 19" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/773155b3-4ae2-4574-a235-6c64ab6e6c70">
   4. ``cd /var/www/html``, ``ls``
      <img width="1440" alt="Screenshot 2024-06-28 at 23 12 46" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/7ede1b7d-894b-4426-a480-05f2529b5982">
   5. download index.html dan styles.css yang terdapat pada github
       1. ``wget -O index.html https://raw.githubusercontent.com/fuaddary/fp-tka/main/Resources/FE/index.html``
       2. ``wget -O styles.css https://raw.githubusercontent.com/fuaddary/fp-tka/main/Resources/FE/styles.css``
      <img width="1440" alt="Screenshot 2024-06-28 at 23 14 32" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/8ceec7dc-aefa-4a83-b15d-f3dbf3e51b38">
   6. Di index.html, ganti fetch api menjadi /analyze dan /history
      <img width="1440" alt="Screenshot 2024-06-28 at 23 15 49" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/2ebb9238-4868-4dd9-a1d7-abd168205e69">
   7. ``cd /etc/apache2/sites-available``, ``ls``
      <img width="1440" alt="Screenshot 2024-06-28 at 23 16 49" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/270e9cf3-0e30-4007-b5fe-5e509f001025">
   9. ``nano 000-default.conf``, tambahkan konfigurasi proxy
      <img width="1440" alt="Screenshot 2024-06-28 at 23 21 08" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/a8ce4136-c07a-4643-8f6b-b9559efbd103">
   10. ``sudo a2enmod proxy``, ``sudo a2enmod proxy_http``
       <img width="1440" alt="Screenshot 2024-06-28 at 23 22 13" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/c41be1c0-0427-4d1e-8553-cc02e6d1a0ea">
   11. ``systemctl restart apache2`` untuk restart servicenya
       <img width="1440" alt="Screenshot 2024-06-28 at 23 22 36" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/71229ef7-e68c-4752-b332-62f05da3bbcf">
   13. tampilan frontend dapat diakses melalui IP address frontend-01 atau IP address load-balancer
       <img width="1440" alt="Screenshot 2024-06-28 at 23 23 15" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/e5007799-ec5b-4016-a5bc-eb2fffa50aec">

### Langkah-langkah untuk droplet backend
   1. ```ssh ke droplet backend-02```
      <img width="1440" alt="Screenshot 2024-06-28 at 23 34 14" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/4fb6c81c-9749-42f2-8d6e-92776efbd48f">
   2. ```sudo apt-get update```
      <img width="1440" alt="Screenshot 2024-06-28 at 23 34 31" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/7697f9ef-1349-4d03-867c-0618bfe0ecbb">
   3. ```sudo apt-get install python3```
      <img width="1440" alt="Screenshot 2024-06-28 at 23 41 36" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/2ebb90f4-44b4-470e-943b-e52bd981e016">
   4. install dependencies :
       1. ```sudo apt-get install python3-pip```
          <img width="1440" alt="Screenshot 2024-06-28 at 23 42 28" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/d78771d0-02b4-4bad-b888-17c15fd8c434">
       2. ```pip install flask```
          <img width="1440" alt="Screenshot 2024-06-28 at 23 43 22" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/fef0ede7-d6fa-45a5-9392-d6d7b3145461">
       3. ```pip install flask_cors```
          <img width="1440" alt="Screenshot 2024-06-28 at 23 43 53" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/998444d9-2f96-44d8-bc29-378005d2bc7d">
       4. ```pip install textblob```
          <img width="1440" alt="Screenshot 2024-06-28 at 23 44 30" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/6591579e-0e1e-4fae-8612-920980f08a0e">
       5. ```pip install pymongo```
          <img width="1440" alt="Screenshot 2024-06-28 at 23 45 06" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/77e3f7e7-cebf-45b8-aed6-ccf3c604fad9">
       6. ```pip install gunicorn```
          <img width="1440" alt="Screenshot 2024-06-28 at 23 45 34" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/b240dfa5-f8a2-4334-b7da-77556f0d113c">
   5. tambahkan file sentiment-analysis.py sesuai pada github 
       1. ```wget -O sentiment-analysis.py https://raw.githubusercontent.com/fuaddary/fp-tka/main/Resources/BE/sentiment-analysis.py```
      <img width="1440" alt="Screenshot 2024-06-28 at 23 48 56" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/053b5d3f-25d5-475c-b4c1-740f7b8eee1c">
   6. ubah client pada file tersebut menjadi link database pada connection details db-mongodb
      <img width="1440" alt="Screenshot 2024-06-29 at 02 16 56" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/ce245e11-37a4-4714-8725-fb6d01dfa4b0">
   7. run dengan command ```python3 sentiment-analysis.py``` atau bisa juga run secara daemon dengan command ```gunicorn -b 0.0.0.0:80 -w 4 -D sentiment-analysis:app```, lalu ```ps aux | grep gunicorn``` untuk melihat apakah sudah running atau belum
      <img width="1440" alt="Screenshot 2024-06-29 at 00 54 07" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/1b63c1ec-aab7-4568-b6d7-44d329757ab3">
   8. akses ke IP Address load balancer

## Hasil Pengujian Setiap Endpoint

### Pengujian dengan Thunder Client
1. Get History
   <img width="1024" alt="Screenshot 2024-06-29 at 00 04 39" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/52e0d6f1-1d96-4992-8301-73148194df2b">
2. Post Analyze
   <img width="1017" alt="Screenshot 2024-06-29 at 00 04 46" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/56f85e28-7af6-486a-a755-9d55085ac817">
### Pengujian dari Web
<img width="1440" alt="Screenshot 2024-06-29 at 00 02 22" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/5e5693bc-e3cf-4a1f-8fa6-41bd87f452e5">




## Hasil Pengujian dan Analisis Loadtesting Locust

- RPS Maksimum (load testing 60 detik)


- Peak Concurrency Maksimum (spawn rate 50, load testing 60 detik)



- Peak Concurrency Maksimum (spawn rate 100, load testing 60 detik)



- Peak Concurrency Maksimum (spawn rate 200, load testing 60 detik)



- Peak Concurrency Maksimum (spawn rate 500, load testing 60 detik)



## Kesimpulan dan Saran





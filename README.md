# Final Project
## Teknologi Komputasi Awan
### Kelompok C5
|Nama|NRP |
|--|--|
|Raditya Hardian Santoso|5027231033|
|Fiorenza|5027231053|
|Harwinda|5027231079|
|Nayyara Ashila|5027221083|

## Video Revisi
https://youtu.be/qYH7urZCgAI?si=sfflgmcht8fYszhZ
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
![Group 79 (1)](https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/e91949e8-023e-48fb-af20-24b7694b1e68)
**Harga perkiraan yang akan kami pakai adalah seperti berikut:**
<img width="1440" alt="Screenshot 2024-06-29 at 18 56 16" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/0532190e-b2ae-4908-86dd-24ba28d1f898">


## Langkah-Langkah Pengerjaan
### Resources yang dibutuhkan
   1. buat 1 droplet yang bernama worker-01
      <img width="1440" alt="Screenshot 2024-06-29 at 17 32 10" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/a210027e-4853-436c-8eb7-b7e6b4f44554">
   2. buat 1 droplet yang bernama worker-02
      <img width="1440" alt="Screenshot 2024-06-29 at 17 32 21" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/b0daf327-287b-4394-b658-7c1598d6e491">
   3. buat mongo database bernama db-mongodb
      <img width="1440" alt="Screenshot 2024-06-29 at 17 31 31" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/971b810b-f1e1-40d0-a9cf-d0017d79ee58">
   4. buat 1 droplet yang dijadikan load-balancer
      <img width="1440" alt="Screenshot 2024-06-29 at 17 30 44" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/1ff7e98e-2d50-46ef-8e12-a8e1cc113bb5">
### Langkah-langkah konfigurasi worker
   * Tiap satu droplet worker akan bekerja sebagai frontend sekaligus backend

   * Langkah-langkah untuk frontend
   1. ssh ke droplet 
      <img width="1440" alt="Screenshot 2024-06-29 at 17 40 37" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/cd4ea800-4c37-45d9-abaf-f6e62d5e3748">
      <img width="1440" alt="Screenshot 2024-06-29 at 17 40 44" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/af1eb21e-7424-4d7f-8514-69ac32ef2c46">
   2. ``sudo apt-get update``
      <img width="1440" alt="Screenshot 2024-06-29 at 17 41 27" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/a1fe3194-19c0-4025-a2ea-e2ab23df882f">
   3. ``sudo apt-get install nginx``
      <img width="1440" alt="Screenshot 2024-06-29 at 17 42 36" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/49514a4e-8f8b-4507-acb4-94f3d311dbfb">
   4. ``cd /var/www/html``, ``ls``
     <img width="1440" alt="Screenshot 2024-06-29 at 17 43 39" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/03e5d45c-ca22-48c1-b9fe-7239491581f4">
   5. download index.html dan styles.css yang terdapat pada github
       1. ``wget -O index.html https://raw.githubusercontent.com/fuaddary/fp-tka/main/Resources/FE/index.html``
       2. ``wget -O styles.css https://raw.githubusercontent.com/fuaddary/fp-tka/main/Resources/FE/styles.css``
      <img width="1440" alt="Screenshot 2024-06-29 at 17 45 11" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/5f272bbb-9ff8-45b4-8b2a-d1704ad26a04">
   6. Di index.html, ganti fetch api menjadi /analyze dan /history
      <img width="1440" alt="Screenshot 2024-06-29 at 17 48 02" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/833e8a81-a0d4-424e-a5a0-318f5c483e54">
   7. ``cd /etc/nginx/sites-available``, ``ls``
      <img width="1440" alt="Screenshot 2024-06-29 at 17 49 58" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/0ddb9452-fae8-428e-86fe-73a257ecbd36">
   9. ``nano default``, tambahkan konfigurasi proxy
      <img width="1440" alt="Screenshot 2024-06-29 at 17 52 40" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/14dfe434-2b44-4f66-a097-a6ae5f41ead2">
   10. ``systemctl restart nginx`` untuk restart servicenya

       
   * Langkah-langkah untuk droplet backend
   1. ssh ke droplet
      <img width="1440" alt="Screenshot 2024-06-29 at 17 55 38" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/9703ee54-8633-4152-be05-e2fba57803ae">
      <img width="1440" alt="Screenshot 2024-06-29 at 17 55 42" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/d0221b8e-1153-40ca-b47e-f3307822b311">
   2. ```sudo apt-get update```
      <img width="1440" alt="Screenshot 2024-06-29 at 17 57 18" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/df320a16-248a-49be-b2bb-cb7f532f90fc">
   3. ```sudo apt-get install python3```
      <img width="1440" alt="Screenshot 2024-06-29 at 17 57 59" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/e213448d-8c5a-46ff-a54c-26100f07b361">
   4. install dependencies :
       1. ```sudo apt-get install python3-pip```
          <img width="1440" alt="Screenshot 2024-06-29 at 17 59 03" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/169e68bc-d25b-4c68-993e-a6eb5e688ff2">
       2. ```pip install flask```
          <img width="1437" alt="Screenshot 2024-06-29 at 18 01 37" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/a305feea-f8d9-4d26-a0a4-7afe5a9bb0db">
       3. ```pip install flask_cors```
         <img width="1440" alt="Screenshot 2024-06-29 at 18 02 25" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/c083c10b-a4ab-49e6-b538-c8bb09b48e9a">
       4. ```pip install textblob```
          <img width="1440" alt="Screenshot 2024-06-29 at 18 02 37" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/006f48e4-0861-4a44-a9c1-7b57bc2deb47">
       5. ```pip install pymongo```
         <img width="1440" alt="Screenshot 2024-06-29 at 18 04 09" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/cb480dfe-bb4f-403b-bba1-98aff4ec636d">
       6. ```pip install gunicorn```
          <img width="1440" alt="Screenshot 2024-06-29 at 18 04 29" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/1ec274a5-2647-4840-bc4c-c2c91646f8a9">
       7. ```pip install gevent```
          <img width="1434" alt="Screenshot 2024-06-29 at 18 04 43" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/985b3d0e-7969-4289-a49f-9ddea4de8b17">
   5. tambahkan file sentiment-analysis.py sesuai pada github 
       1. ```wget -O sentiment-analysis.py https://raw.githubusercontent.com/fuaddary/fp-tka/main/Resources/BE/sentiment-analysis.py```
      <img width="1440" alt="Screenshot 2024-06-29 at 18 05 49" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/e8f35b6b-52d3-407b-a564-7c637c177faa">
   6. ubah client pada file tersebut menjadi link database pada connection details db-mongodb
      <img width="1440" alt="Screenshot 2024-06-29 at 18 08 27" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/fb79c358-c97d-4954-b06a-66d286195f51">
   7. run dengan command ```gunicorn -b 0.0.0.0:5000 -w 5 -k gevent --timeout 60 --graceful-timeout 60 sentiment-analysis:app ```, lalu ```ps aux | grep gunicorn``` untuk melihat apakah sudah running atau belum
      <img width="1440" alt="Screenshot 2024-06-29 at 18 12 14" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/8fbd1c0f-f3fb-44c8-b4e2-8ad872a19c64">

### Langkah-langkah konfigurasi load balancer
   1. ```sudo apt-get update```
      <img width="1440" alt="Screenshot 2024-06-29 at 18 21 51" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/bc5f4378-1de7-4458-aad0-80826f332422">
   2. ```sudo apt-get install nginx```
      <img width="1440" alt="Screenshot 2024-06-29 at 18 22 48" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/763f1f0b-ac68-4bde-8ac8-2e3c8458c4d7">
   3. buat konfigurasi baru di /etc/nginx/sites-available/lb
   4. konfigurasi /etc/nginx/nginx.conf
   5. sudo systemctl restart nginx

### Setup Database
   1. Install MongoDB compass GUI
      <img width="1440" alt="Screenshot 2024-06-29 at 02 28 36" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/e89731ef-e798-46da-b892-8020d54a9770">
   2. Tambahkan koneksi baru menggunakan link database pada connection details
     <img width="1440" alt="Screenshot 2024-06-29 at 02 10 11" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/b94d603e-f621-4715-8598-45a1ada0bf98">
   3. Database sentiment analysis sudah bisa diakses
      <img width="1440" alt="Screenshot 2024-06-29 at 02 31 16" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/b2568780-c669-4770-ae29-6ac065861aac">
      <img width="1440" alt="Screenshot 2024-06-29 at 02 32 11" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/2ce8ba6c-0dac-4a6a-9eb7-411f28cec9d1">
   4. Kosongkan database setiap ingin analisis loadtesting menggunakan locust
      <img width="1440" alt="Screenshot 2024-06-29 at 02 26 23" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/3a37626d-d97d-4dde-a21d-30466444792c">


## Hasil Pengujian Setiap Endpoint

### Pengujian dengan Thunder Client
Diakses menggunakan ip salah satu droplet
1. Get History
   <img width="1024" alt="Screenshot 2024-06-29 at 19 20 22" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/4c0de8e1-a3bb-4dbf-b471-2193bd95ff14">
2. Post Analyze
   <img width="1030" alt="Screenshot 2024-06-29 at 19 20 01" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/64a00670-d233-41f2-a959-efd818549e80">
   
### Pengujian dari Web
Diakses menggunakan ip salah satu droplet
<img width="1440" alt="Screenshot 2024-06-29 at 19 41 59" src="https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/dd589d96-4546-4291-b4f7-5bfc0da4b1df">




## Hasil Pengujian dan Analisis Loadtesting Locust

- RPS Maksimum (load testing 60 detik)
  RPS maksimum 312.3/200 x 30 = 46,845
  ![WhatsApp Image 2024-06-29 at 23 15 20](https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/bf59708c-c74a-46cb-936d-e9470fb9ed9b)

- Peak Concurrency 1000 (spawn rate 50, load testing 60 detik)
   ![WhatsApp Image 2024-06-29 at 23 15 20](https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/adc6992e-b50f-4cca-8bfd-d4d677be039e)

- Peak Concurrency 1000 (spawn rate 100, load testing 60 detik)
   ![WhatsApp Image 2024-06-29 at 23 13 11](https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/773178b4-b159-47c4-971b-85440e8db569)

- Peak Concurrency 1000 (spawn rate 200, load testing 60 detik)
   ![WhatsApp Image 2024-06-29 at 23 11 08](https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/c561f391-8284-4d76-8df8-1d7d63c0a8ef)

- Peak Concurrency 1000 (spawn rate 500, load testing 60 detik)
   ![WhatsApp Image 2024-06-29 at 23 19 55](https://github.com/rdthrdn/fp-cloud-computing-c5/assets/147926732/2aef6401-b5cd-4ad3-b22c-3ddd2784a2f8)



## Kesimpulan
Kesimpulan :

Berdasarkan hasil pengujian yang dilakukan terhadap sistem sentiment analysis, terdapat beberapa hal yang menunjukkan bahwa performa dan stabilitas sistem masih memerlukan perbaikan signifikan. Berikut adalah poin-poin utama dari pengujian kami:

Responsivitas yang Rendah:
Sistem kami menunjukkan waktu respon yang cukup tinggi selama pengujian, dengan waktu respon rata-rata mencapai 2 detik pada beban normal, dan meningkat hingga 5 detik atau lebih pada beban puncak (4000 peak concurrency). Hal ini menunjukkan bahwa sistem tidak mampu merespons permintaan dengan cepat ketika jumlah pengguna meningkat.

Stabilitas yang Kurang:
Selama pengujian load testing menggunakan Locust, kami menemukan bahwa sistem mengalami beberapa kali crash ketika mencapai beban puncak. Ini menunjukkan bahwa ada masalah stabilitas yang perlu segera diatasi untuk memastikan sistem tetap berfungsi dengan baik di bawah beban tinggi.

Kemampuan Skalabilitas yang Terbatas:
Sistem tidak menunjukkan kemampuan skalabilitas yang baik, dengan performa yang menurun drastis ketika jumlah pengguna meningkat. Ini mengindikasikan bahwa arsitektur saat ini belum optimal untuk menangani peningkatan jumlah pengguna secara efektif.

Penggunaan Sumber Daya yang Tinggi:
Penggunaan CPU dan RAM meningkat secara signifikan selama pengujian beban, menunjukkan bahwa sistem saat ini tidak efisien dalam mengelola sumber daya. Hal ini bisa menyebabkan server mengalami kelebihan beban dan akhirnya menurunkan performa secara keseluruhan.

## Saran

Berdasarkan temuan di atas, kami memberikan saran sebagai berikut:

Optimasi Kode dan Query: Lakukan optimasi pada kode backend dan query database untuk mengurangi waktu respon dan meningkatkan efisiensi.

Implementasi Caching: Pertimbangkan untuk menggunakan caching pada beberapa bagian sistem untuk mengurangi beban pada server dan mempercepat waktu respon.

Peningkatan Arsitektur: Evaluasi kembali arsitektur sistem dan pertimbangkan untuk menggunakan solusi skalabilitas seperti load balancer dan microservices untuk meningkatkan kemampuan sistem dalam menangani beban tinggi.

Pengujian Berkelanjutan: Lakukan pengujian berkelanjutan dan iteratif untuk mengidentifikasi dan mengatasi masalah stabilitas sebelum sistem digunakan secara luas.

Pemantauan dan Logging: Implementasikan pemantauan dan logging yang lebih baik untuk mendeteksi dan mendiagnosa masalah performa secara real-time.

Dengan mengikuti rekomendasi di atas, kami berharap sistem sentiment analysis dapat ditingkatkan performa dan skalabilitasnya, sehingga mampu memberikan pengalaman pengguna yang lebih baik dan memenuhi kebutuhan beban tinggi di masa mendatang.

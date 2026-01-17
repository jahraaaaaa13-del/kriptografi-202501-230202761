# Laporan Praktikum Kriptografi
Minggu ke-: 12  
Topik: Aplikasi-tls   
Nama: Khoirun Nisa Az-Zahra  
NIM: 230202761  
Kelas: 5IKRB  

---

## 1. Tujuan
1. Menganalisis penggunaan kriptografi pada email dan SSL/TLS.
2. Menjelaskan enkripsi dalam transaksi e-commerce.
3. Mengevaluasi isu etika & privasi dalam penggunaan kriptografi di kehidupan sehari-hari.

---

## 2. Dasar Teori
Transport Layer Security (TLS) adalah protokol kriptografi standar industri yang dirancang untuk mengamankan komunikasi data antar aplikasi di jaringan komputer. Sebagai evolusi dari protokol Secure Sockets Layer (SSL), TLS bekerja pada lapisan di atas transpor (TCP) untuk menyediakan tiga pilar keamanan utama: kerahasiaan melalui enkripsi data, integritas untuk memastikan data tidak dimanipulasi selama transmisi, dan autentikasi untuk memvalidasi identitas pihak yang berkomunikasi menggunakan sertifikat digital.

Mekanisme operasional TLS terbagi menjadi dua tahap utama, yaitu Handshake Protocol dan Record Protocol. Pada tahap handshake, klien dan server melakukan negosiasi algoritma kriptografi dan pertukaran kunci sesi secara asimetris. Setelah koneksi aman terbentuk, data kemudian dikirimkan melalui Record Protocol menggunakan enkripsi simetris yang lebih efisien secara komputasi. Dalam implementasi praktis, TLS secara luas digunakan untuk mengamankan protokol aplikasi seperti HTTP (menjadi HTTPS), pengiriman email (SMTP/IMAP), dan transfer file, sehingga melindungi informasi sensitif dari ancaman penyadapan (eavesdropping) dan serangan man-in-the-middle.

---

## 3. Alat dan Bahan
- Python 3.14
- Visual Studio Code / editor lain
- Git dan akun GitHub

---

## 4. Langkah Percobaan
1. Laporan studi kasus tentang penerapan SSL/TLS pada email dan e-commerce.
2. Analisis isu privasi dan etika penggunaan kriptografi.

---

## 5. Source Code

---

## 6. Hasil dan Pembahasan
<img width="1366" height="768" alt="Screenshot week12" src="https://github.com/user-attachments/assets/bf10ddc3-2b4b-4187-8465-56ddb18fd6d2" />
Analisis Sertifikat Digital (Lazada)
Hasil observasi menunjukkan penerapan protokol TLS yang aktif pada situs e-commerce Lazada. Poin-poin teknis utamanya adalah:
- Issuer CA (Certificate Authority): Sertifikat diterbitkan oleh GlobalSign GCC R3 OV TLS CA 2024. Ini menunjukkan bahwa Lazada menggunakan pihak ketiga tepercaya untuk memvalidasi identitas server mereka.
- Masa Berlaku: Sertifikat diterbitkan pada 29 Desember 2025 dan akan berakhir pada 30 Januari 2027. Hal ini memastikan bahwa kunci enkripsi diperbarui secara berkala untuk menjaga keamanan.
- Identitas Pemilik: Sertifikat diterbitkan untuk organisasi Alibaba (China) Technology Co., Ltd. dengan Common Name (CN) untuk domain *.lazada.vn (wildcard certificate).
- Algoritma Fingerprint: Menggunakan SHA-256, yang merupakan algoritma hash standar industri untuk memastikan bahwa sertifikat tersebut otentik dan tidak dimodifikasi oleh pihak luar.

Relevansi dengan Keamanan E-commerce
Penggunaan TLS pada gambar tersebut sangat krusial karena:
1. Enkripsi Transaksi: Mengamankan data sensitif pengguna (seperti nomor kartu kredit atau alamat pengiriman) saat dikirim dari browser ke server Lazada, sehingga tidak bisa disadap (eavesdropping).
2. Autentikasi Server: Sertifikat dari GlobalSign memberikan jaminan kepada pengguna bahwa mereka benar-benar terhubung ke situs resmi Lazada, bukan situs palsu yang dibuat oleh penyerang (phishing).
3. Mencegah MitM: Dengan enkripsi yang aktif, penyerang tidak dapat mengubah data transaksi di tengah jalan (Man-in-the-Middle attack).

---

## 7. Jawaban Pertanyaan  
- Pertanyaan 1: Apa perbedaan utama antara HTTP dan HTTPS?
Perbedaan utama antara HTTP dan HTTPS terletak pada keamanannya. HTTP mengirimkan data tanpa enkripsi sehingga informasi mudah disadap atau dimodifikasi oleh pihak tidak berwenang. Sebaliknya, HTTPS menggunakan SSL/TLS untuk mengenkripsi data, memverifikasi identitas server melalui sertifikat digital, dan memastikan komunikasi antara pengguna dan server lebih aman serta tepercaya.

- Pertanyaan 2: Mengapa sertifikat digital menjadi penting dalam komunikasi TLS?
Sertifikat digital penting dalam komunikasi TLS karena berfungsi untuk memverifikasi identitas server dan memastikan bahwa pengguna benar-benar terhubung ke server yang sah. Dengan adanya sertifikat dari Certificate Authority (CA) tepercaya, sertifikat digital membantu mencegah serangan seperti Man-in-the-Middle serta memungkinkan proses enkripsi data berjalan dengan aman.

- Pertanyaan 3: Bagaimana kriptografi mendukung privasi dalam komunikasi digital, tetapi sekaligus menimbulkan tantangan hukum dan etika?
Kriptografi mendukung privasi dalam komunikasi digital dengan mengenkripsi data sehingga hanya pihak yang berwenang yang dapat membaca isi pesan, melindungi informasi pribadi dari penyadapan dan penyalahgunaan. Namun, di sisi lain, penggunaan enkripsi yang kuat juga menimbulkan tantangan hukum dan etika karena dapat menghambat proses penegakan hukum dan pengawasan, serta memunculkan dilema antara perlindungan privasi individu dan kepentingan keamanan publik.

---

## 8. Kesimpulan
Penerapan TLS pada platform e-commerce Lazada memiliki peran yang sangat penting dalam menjaga keamanan dan kepercayaan pengguna. Dengan penggunaan protokol HTTPS dan sertifikat digital dari Certificate Authority (CA) tepercaya, TLS memastikan bahwa komunikasi antara pengguna dan server Lazada terlindungi melalui proses enkripsi data. Hal ini melindungi informasi sensitif seperti data login, informasi pribadi, dan detail transaksi pembayaran dari risiko penyadapan atau manipulasi oleh pihak tidak berwenang. Selain itu, TLS juga berfungsi untuk memverifikasi identitas server sehingga pengguna dapat memastikan bahwa mereka benar-benar terhubung ke situs Lazada yang resmi. Meskipun TLS memberikan perlindungan privasi yang kuat, penerapannya tetap perlu diimbangi dengan kebijakan keamanan dan etika yang jelas agar perlindungan data pengguna tidak bertentangan dengan kebutuhan audit, regulasi, dan kepentingan hukum yang berlaku.

---

## 9. Daftar Pustaka
(Cantumkan referensi yang digunakan.  
Contoh:  
- Katz, J., & Lindell, Y. *Introduction to Modern Cryptography*.  
- Stallings, W. *Cryptography and Network Security*.  )

---

## 10. Commit Log
commit abc12345
Author: Khoirun Nisa Az-Zahra <jahraaaaaa.13@gmail.com>
Date:   2026-01-17


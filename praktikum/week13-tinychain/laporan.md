# Laporan Praktikum Kriptografi
Minggu ke-: 13  
Topik: Tiny-chain  
Nama: Khoirun Nisa Az-Zahra  
NIM: 230202761  
Kelas: 5IKRB  

---

## 1. Tujuan
1. Menjelaskan peran hash function dalam blockchain.
2. Melakukan simulasi sederhana Proof of Work (PoW).
3. Menganalisis keamanan cryptocurrency berbasis kriptografi.

---

## 2. Dasar Teori
Tiny-chain merupakan simulasi sederhana dari konsep blockchain yang digunakan untuk memahami prinsip dasar kerja sistem cryptocurrency. Blockchain adalah struktur data berbentuk rantai blok, di mana setiap blok berisi data transaksi, hash blok sebelumnya, dan hash blok saat ini. Keterkaitan antarblok melalui hash kriptografis membuat data di dalam blockchain bersifat immutable, karena perubahan pada satu blok akan memengaruhi seluruh blok setelahnya.

Fungsi hash kriptografis, seperti SHA-256, berperan penting dalam Tiny-chain untuk menjamin integritas dan keamanan data. Hash function menghasilkan nilai hash dengan panjang tetap dari input apa pun, serta memiliki sifat satu arah dan tahan terhadap kolisi. Dengan sifat tersebut, hash digunakan untuk mengidentifikasi blok secara unik dan mendeteksi perubahan data secara cepat.

Selain itu, Tiny-chain juga mengadopsi konsep Proof of Work (PoW) sebagai mekanisme validasi blok. PoW mengharuskan pencarian nilai nonce yang menghasilkan hash dengan kriteria tertentu (misalnya diawali dengan sejumlah nol). Mekanisme ini membuat proses penambahan blok membutuhkan usaha komputasi, sehingga dapat mencegah manipulasi data dan meningkatkan keamanan sistem blockchain secara keseluruhan.

---

## 3. Alat dan Bahan
- Python 3.14
- Visual Studio Code
- Git dan akun GitHub  

---

## 4. Langkah Percobaan
1. Membuat file tinychain.py di folder praktikum/week13-tinychain/src/.
2. Menyalin kode program dari panduan praktikum.
3. Menjalankan program dengan perintah python tinychain.py

---

## 5. Source Code
<img width="1026" height="436" alt="Screenshot1 source code week13" src="https://github.com/user-attachments/assets/468bc309-e33a-4796-a5af-9769f2509feb" />
<img width="712" height="455" alt="Screenshot2 source code week13" src="https://github.com/user-attachments/assets/f204ea91-d97d-4abe-9dfb-fa6c8c1c4053" />


---

## 6. Hasil dan Pembahasan
<img width="1139" height="172" alt="Screenshot hasil week13" src="https://github.com/user-attachments/assets/dc56ac02-fcd0-4f23-8cb1-1bf5c9fdce74" />
Program ini mensimulasikan proses dasar blockchain mining, di mana setiap blok dicari nonce-nya hingga menghasilkan hash yang memenuhi kriteria tertentu (biasanya diawali dengan sejumlah nol). Proses ini menunjukkan bagaimana sistem blockchain menjaga integritas data dengan kriptografi — setiap blok bergantung pada hash blok sebelumnya. Hasil tersebut membuktikan algoritma mining bekerja dengan benar dan berhasil menghasilkan dua blok valid.

---

## 7. Jawaban Pertanyaan 
- Pertanyaan 1: Mengapa fungsi hash sangat penting dalam blockchain?
Fungsi hash sangat penting dalam blockchain karena berperan sebagai pengaman dan pengidentifikasi unik setiap blok. Hash mengubah data menjadi kode digital tetap yang sulit ditebak, sehingga jika ada sedikit perubahan pada data, hasil hash akan berubah total. Hal ini membuat blockchain tahan terhadap manipulasi, karena setiap blok terhubung melalui hash blok sebelumnya. Dengan demikian, fungsi hash menjaga integritas, keaslian, dan keamanan data dalam seluruh jaringan blockchain.
 
- Pertanyaan 2: Bagaimana Proof of Work mencegah double spending?
Proof of Work (PoW) mencegah double spending dengan memastikan bahwa setiap transaksi hanya dapat dicatat pada satu blok yang sah dalam blockchain. Untuk menambahkan blok baru, penambang harus menyelesaikan perhitungan kriptografi yang memerlukan waktu dan daya komputasi besar. Setelah blok divalidasi dan ditambahkan ke rantai, mengubah data di dalamnya akan membutuhkan pengulangan seluruh proses mining di semua blok berikutnya — sesuatu yang hampir mustahil dilakukan secara bersamaan oleh penyerang. Dengan cara ini, PoW memastikan transaksi tidak bisa digandakan atau dimodifikasi, sehingga menjaga keabsahan dan kepercayaan sistem.
 
- Pertanyaan 3: Apa kelemahan dari PoW dalam hal efisiensi energi?
Kelemahan utama Proof of Work (PoW) dalam hal efisiensi energi adalah konsumsi daya yang sangat besar. Proses mining memerlukan komputer dengan daya tinggi untuk melakukan perhitungan kriptografi kompleks demi menemukan hash yang valid. Ribuan penambang di seluruh dunia bersaing memecahkan teka-teki yang sama, sehingga banyak energi terbuang hanya untuk menentukan satu blok pemenang. Akibatnya, PoW dianggap boros energi, tidak ramah lingkungan, dan kurang efisien dibandingkan mekanisme lain seperti Proof of Stake (PoS) yang jauh lebih hemat daya.  

---

## 8. Kesimpulan
Program Tinychain merupakan simulasi sederhana dari konsep blockchain yang menunjukkan cara kerja proses mining dan pembentukan blok menggunakan algoritma kriptografi. Melalui fungsi hash, setiap blok memiliki identitas unik yang menjaga integritas data, sementara mekanisme Proof of Work (PoW) memastikan keaslian dan keamanan transaksi dengan mencegah manipulasi serta double spending. Meskipun PoW memerlukan energi besar dan kurang efisien, konsep ini tetap penting untuk memahami dasar keamanan dan keandalan sistem blockchain yang menjadi fondasi berbagai teknologi modern seperti kripto dan sistem desentralisasi lainnya.

---

## 9. Daftar Pustaka 
- Katz, J., & Lindell, Y. *Introduction to Modern Cryptography*.  
- Stallings, W. *Cryptography and Network Security*.  )

---

## 10. Commit Log
commit abc12345
Author: Khoirun Nisa Az-Zahra <jahraaaaaa.13@gmail.com>
Date:   2026-01-17

# Laporan Praktikum Kriptografi
Minggu ke-: 14  
Topik: Analisis Serangan Kriptografi  
Nama: Khoirun Nisa Az-Zahra 
NIM: 230202761  
Kelas: 5IKRB  

---

## 1. Tujuan
1. Mengidentifikasi jenis serangan pada sistem informasi nyata.
2. Mengevaluasi kelemahan algoritma kriptografi yang digunakan.
3. Memberikan rekomendasi algoritma kriptografi yang sesuai untuk perbaikan keamanan.

---

## 2. Dasar Teori
Analisis serangan kriptografi merupakan studi tentang cara menembus atau melemahkan sistem kriptografi dengan tujuan untuk memperoleh informasi rahasia tanpa memiliki kunci yang sah. Dalam kriptografi, keamanan suatu algoritma tidak hanya bergantung pada kerahasiaan kunci, tetapi juga pada ketahanan algoritma terhadap berbagai jenis serangan. Secara umum, serangan kriptografi dibagi menjadi beberapa kategori, seperti ciphertext-only attack, di mana penyerang hanya memiliki data terenkripsi; known-plaintext attack, di mana penyerang mengetahui sebagian pasangan teks asli dan terenkripsi; serta chosen-plaintext attack dan chosen-ciphertext attack, di mana penyerang dapat memilih data untuk dianalisis.

Tujuan utama analisis serangan ini adalah untuk menguji kekuatan algoritma dan menemukan potensi kelemahan pada sistem keamanan. Dengan memahami berbagai bentuk serangan kriptografi, pengembang dapat merancang algoritma yang lebih kuat, efisien, dan tahan terhadap upaya pembobolan data, sehingga menjaga kerahasiaan, integritas, dan autentikasi informasi dalam sistem keamanan digital.

---

## 3. Alat dan Bahan
- Python 3.x  
- Visual Studio Code  
- Git dan akun GitHub  

---

## 4. Langkah Percobaan
1. Membuat file `caesar_cipher.py` di folder `praktikum/week2-cryptosystem/src/`.
2. Menyalin kode program dari panduan praktikum.
3. Menjalankan program dengan perintah `python caesar_cipher.py`.)

---

## 5. Source Code
<img width="578" height="265" alt="Screenshot source code week14" src="https://github.com/user-attachments/assets/c6b3a608-0479-4ca4-a3d6-8b9050c1991e" />

---

## 6. Hasil dan Pembahasan
<img width="1149" height="197" alt="Screenshot hasil week14" src="https://github.com/user-attachments/assets/cd181548-1c98-4c85-94db-f99ad9d7770e" />
MD5 menghasilkan hash pendek dan kini dianggap lemah (rentan collision dan brute-force), sedangkan SHA-256 jauh lebih kuat secara kriptografis. Namun untuk penyimpanan kata sandi sebaiknya tidak hanya pakai SHA-256 saja—gunakan algoritma hashing khusus kata sandi seperti bcrypt/scrypt/Argon2 dengan salt unik untuk setiap pengguna agar tahan terhadap serangan brute-force dan dictionary.

---

## 7. Jawaban Pertanyaan
- Pertanyaan 1: Mengapa banyak sistem lama masih rentan terhadap brute force?
Banyak sistem lama masih rentan terhadap brute force karena mereka menggunakan algoritma hashing atau mekanisme keamanan yang sudah usang dan tidak dirancang untuk menghadapi kekuatan komputasi modern. Sistem lama sering memakai algoritma cepat seperti MD5 atau SHA-1, tanpa menambahkan salt atau mekanisme perlambatan seperti bcrypt. Selain itu, banyak sistem lama tidak membatasi jumlah percobaan login atau tidak memiliki deteksi serangan otomatis, sehingga penyerang bisa mencoba jutaan kombinasi password tanpa terblokir. Akibatnya, sistem tersebut menjadi mudah ditembus dengan brute force meskipun algoritmanya dulunya dianggap aman.
  
- Pertanyaan 2: Apa perbedaan kelemahan algoritma dan implementasi?
Perbedaan antara kelemahan algoritma dan kelemahan implementasi terletak pada sumber masalah keamanannya:
a. Kelemahan algoritma terjadi ketika desain atau struktur matematis algoritma itu sendiri memiliki celah. Contohnya, MD5 dan SHA-1 rentan terhadap collision attack karena sifat internalnya sudah tidak cukup kuat menghadapi teknik kriptanalisis modern. Masalah ini ada pada dasar algoritmanya, bukan pada cara penggunaannya.
b. Kelemahan implementasi muncul karena kesalahan dalam cara algoritma diterapkan di program atau sistem. Misalnya, penggunaan SHA-256 tanpa salt untuk menyimpan password, atau konfigurasi SSL yang tidak aman (misalnya masih mengizinkan TLS versi lama). Dalam hal ini, algoritma dasarnya aman, tetapi cara penerapannya yang tidak tepat membuat sistem rentan.
 
- Pertanyaan 3: Bagaimana memastikan sistem tetap aman di masa depan?
Untuk memastikan sistem tetap aman di masa depan, perlu diterapkan pendekatan keamanan yang berkelanjutan. Langkah utamanya meliputi penggunaan algoritma kriptografi modern seperti SHA-256, AES, atau ECC, serta menghindari algoritma lama yang rentan seperti MD5 dan SHA-1. Sistem juga harus selalu diperbarui agar celah keamanan baru dapat segera ditutup, dan mekanisme hashing adaptif seperti bcrypt, scrypt, atau Argon2 digunakan untuk menyesuaikan diri dengan peningkatan daya komputasi di masa depan. Selain itu, penerapan keamanan berlapis, autentikasi multifaktor, serta audit dan pengujian keamanan secara rutin sangat penting untuk mendeteksi serta mencegah potensi serangan. Dengan penerapan langkah-langkah tersebut, sistem dapat tetap tangguh menghadapi ancaman siber yang terus berkembang.

---

## 8. Kesimpulan
Analisis serangan kriptografi merupakan langkah penting untuk memahami dan mengantisipasi berbagai bentuk ancaman terhadap sistem keamanan data. Melalui analisis ini, kita dapat mengidentifikasi kelemahan baik pada algoritma maupun implementasi kriptografi yang digunakan, seperti penggunaan hash lemah atau konfigurasi sistem yang tidak aman. Dengan memahami cara kerja serangan seperti brute force, dictionary, atau collision attack, pengembang dapat merancang sistem yang lebih tangguh menggunakan algoritma modern dan praktik keamanan yang benar. Secara keseluruhan, analisis serangan kriptografi berperan penting dalam menjaga kerahasiaan, integritas, dan keandalan informasi di era digital yang terus berkembang.

---

## 9. Daftar Pustaka
- Ramalinda & Raharja. *Strategi Perlindungan Data Menggunakan Sistem Kriptografi dalam Keamanan Informasi*.  

---

## 10. Commit Log
commit abc12345
Author: Khoirun Nisa Az-Zahra <jahraaaaaa.13@gmail.com>
Date:   2026-01-17


# Laporan Praktikum Kriptografi
Minggu ke-: 7 
Topik: Simulasi Diffie-Hellman  
Nama: Khoirun Nisa Az-Zahra  
NIM: 230202761  
Kelas: 5IKRB  

---

## 1. Tujuan
1. Melakukan simulasi protokol Diffie-Hellman untuk pertukaran kunci publik.
2. Menjelaskan mekanisme pertukaran kunci rahasia menggunakan bilangan prima dan logaritma diskrit.
3. Menganalisis potensi serangan pada protokol Diffie-Hellman (termasuk serangan Man-in-the-Middle / MITM).

---

## 2. Dasar Teori
Diffie-Hellman adalah memungkinkan dua pihak yang belum pernah berbagi informasi rahasia sebelumnya untuk secara aman membuat dan menyepakati kunci rahasia bersama melalui saluran komunikasi yang tidak aman, seperti internet. Protokol ini bekerja berdasarkan asumsi bahwa sangat sulit (tidak praktis secara komputasi) untuk memecahkan masalah logaritma diskret dalam matematika.

Prosesnya melibatkan pemilihan bilangan prima besar $p$ dan generator $g$ (bilangan bulat). Setiap pihak (misalnya, Alice dan Bob) secara pribadi memilih bilangan bulat acak rahasia ($a$ untuk Alice, $b$ untuk Bob) yang berfungsi sebagai kunci pribadi. Mereka kemudian menghitung nilai publik mereka masing-masing dengan menggunakan kunci pribadi mereka bersama dengan $p$ dan $g$ (misalnya, Alice menghitung $A = g^a \pmod{p}$). Nilai publik ini ($A$ dan $B$) kemudian dipertukarkan secara terbuka. Pihak lawan kemudian menggunakan nilai publik yang diterima, kunci pribadi mereka sendiri, $p$, dan $g$ untuk menghitung kunci rahasia bersama yang identik (Alice menghitung $K = B^a \pmod{p}$, dan Bob menghitung $K = A^b \pmod{p}$). Karena sifat eksponen, kedua perhitungan menghasilkan nilai $K$ yang sama: $g^{ab} \pmod{p}$. Kunci rahasia bersama $K$ inilah yang kemudian dapat digunakan untuk mengenkripsi komunikasi selanjutnya. Seorang penyadap (Eve) yang hanya melihat nilai publik ($A, B, g, p$) tidak dapat dengan mudah menentukan kunci rahasia bersama $K$ tanpa memecahkan kunci pribadi ($a$ atau $b$), yang merupakan masalah logaritma diskret yang sulit.

---

## 3. Alat dan Bahan
- Python
- Visual Studio Code
- Git dan akun GitHub

---

## 4. Langkah Percobaan
1. Membuat file diffie- hellman.py di folder praktikum/week7-diffie-hellman/src/.
2. Menyalin kode program dari panduan praktikum.
3. Menjalankan program dengan perintah python diffie-hellman.py.

## 5. Source Code
import random

# parameter umum (disepakati publik)
p = 23  # bilangan prima
g = 5   # generator

# private key masing-masing pihak
a = random.randint(1, p-1)  # secret Alice
b = random.randint(1, p-1)  # secret Bob

# public key
A = pow(g, a, p)
B = pow(g, b, p)

# exchange public key
shared_secret_A = pow(B, a, p)
shared_secret_B = pow(A, b, p)

print("Kunci bersama Alice :", shared_secret_A)
print("Kunci bersama Bob   :", shared_secret_B)

---

## 6. Hasil dan Pembahasan
<img width="1366" height="768" alt="Simulasi Diffie-Hellman" src="https://github.com/user-attachments/assets/c431cccf-7db6-484f-89df-c4495b3ab33a" />


---

## 7. Jawaban Pertanyaan
- Pertanyaan 1: Mengapa Diffie-Hellman memungkinkan pertukaran kunci di saluran publik? = Diffie-Hellman memungkinkan pertukaran kunci di saluran publik karena ia dirancang untuk memanfaatkan kesulitan komputasi dari Masalah Logaritma Diskret (Discrete Logarithm Problem/DLP). Protokol ini bekerja dengan memungkinkan kedua pihak untuk secara terbuka mempublikasikan nilai-nilai komputasi perantara ($A$ dan $B$), yang merupakan hasil dari pemangkatan modulus dari eksponen rahasia pribadi mereka ($a$ dan $b$). Meskipun seorang penyadap (Eve) dapat melihat semua nilai publik ini, mendapatkan kunci rahasia bersama yang sebenarnya memerlukan penemuan eksponen rahasia ($a$ atau $b$) dari nilai publik yang sesuai. Proses "pembalikan" ini setara dengan memecahkan DLP, yang secara komputasi sangat tidak praktis dan membutuhkan waktu yang sangat lama dengan teknologi saat ini, sehingga kunci akhir tetap aman.
- Pertanyaan 2: Apa kelemahan utama protokol Diffie-Hellman murni? = Kelemahan utama dari protokol Diffie-Hellman murni (tanpa tambahan keamanan) adalah kerentanannya terhadap serangan Man-in-the-Middle (MITM). Protokol ini dirancang untuk mencapai kesepakatan kunci yang aman antara dua pihak yang berinteraksi melalui saluran publik, tetapi ia tidak menyediakan otentikasi bagi para pihak tersebut. Akibatnya, penyerang dapat mencegat nilai publik yang dipertukarkan, menggantinya dengan nilai publik mereka sendiri, dan secara efektif membentuk dua kunci rahasia bersama yang terpisah: satu dengan pihak pertama dan satu lagi dengan pihak kedua. Hal ini memungkinkan penyerang untuk membaca, memodifikasi, dan meneruskan semua komunikasi yang terenkripsi di antara keduanya tanpa terdeteksi, karena kedua pihak tersebut tidak memiliki cara untuk memverifikasi bahwa mereka benar-benar berbicara dengan pihak yang mereka yakini. Kelemahan ini diatasi dalam praktik dengan mengintegrasikan Diffie-Hellman dengan skema otentikasi, seperti sertifikat digital atau tanda tangan digital.
- Pertanyaan 3: Bagaimana Cara Mencegah Serangan MITM pada Protokol Ini? = Cara utama untuk mencegah serangan Man-in-the-Middle (MITM) pada protokol Diffie-Hellman murni adalah dengan menambahkan mekanisme otentikasi yang kuat untuk memverifikasi identitas pihak-pihak yang berkomunikasi. Pendekatan yang paling umum adalah menggunakan Infrastruktur Kunci Publik (PKI), di mana kedua pihak menggunakan Sertifikat Digital yang dikeluarkan oleh Otoritas Sertifikasi (CA) tepercaya. Sertifikat ini berisi kunci publik yang telah diverifikasi dan tanda tangan digital yang tidak dapat dipalsukan, yang menjamin bahwa nilai publik Diffie-Hellman yang dipertukarkan ($A$ dan $B$) benar-benar berasal dari pihak yang diklaim (Alice dan Bob), sehingga mencegah penyerang menyuntikkan kunci palsu mereka sendiri. Selain itu, Diffie-Hellman Ephemeral (DHE) atau Elliptic Curve Diffie-Hellman Ephemeral (ECDHE) sering digunakan untuk memastikan Perfect Forward Secrecy (PFS), yang berarti bahkan jika kunci rahasia jangka panjang suatu saat terbongkar, kunci sesi di masa lalu tetap aman.

---

## 8. Kesimpulan
Diffie-Hellman merupakan metode revolusioner untuk mencapai pertukaran kunci kriptografi yang aman di atas saluran komunikasi yang tidak aman. Intinya, ia memanfaatkan sifat asimetris dari matematika modular, khususnya kesulitan komputasi Masalah Logaritma Diskret (DLP), untuk memungkinkan dua pihak secara terpisah menghitung kunci rahasia bersama yang identik. Kunci ini berasal dari nilai publik yang dipertukarkan dan eksponen rahasia pribadi masing-masing pihak. Meskipun protokol ini berhasil dalam membuat kunci bersama tanpa pernah mengirimkannya secara langsung, kelemahan mendasarnya adalah kurangnya otentikasi, menjadikannya rentan terhadap serangan Man-in-the-Middle (MITM). Oleh karena itu, dalam penerapannya di dunia nyata, protokol ini selalu dikombinasikan dengan mekanisme otentikasi seperti sertifikat digita

---

## 9. Daftar Pustaka
(Cantumkan referensi yang digunakan.  
Contoh:  
- Lie, I. R., & Alamsyah, D. (2023). Penerapan Algoritma Diffie-Hellman pada Steganografi Least Significant Bit.
- Wahyuni, A. (2011). Keamanan Pertukaran Kunci Kriptografi dengan Algoritma Hybrid: Diffie-Hellman dan RSA.

---

## 10. Commit Log
```
commit abc12345
Author: Khoirun Nisa Az-Zahra <jahraaaaaa.13@gmail.com>
Date:   2025-11-24

    week2-cryptosystem: implementasi Caesar Cipher dan laporan )
```

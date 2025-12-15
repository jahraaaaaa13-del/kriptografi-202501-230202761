# Laporan Praktikum Kriptografi
Minggu ke-: 9  
Topik: Digital Signature (RSA/DSA)  
Nama: Khoirun Nisa Az-Zahra  
NIM: 230202761 
Kelas: 5IKRB  

---

## 1. Tujuan
1. Mengimplementasikan tanda tangan digital menggunakan algoritma RSA/DSA.
2. Memverifikasi keaslian tanda tangan digital.
3. Menjelaskan manfaat tanda tangan digital dalam otentikasi pesan dan integritas data.

---

## 2. Dasar Teori
Tanda Tangan Digital adalah mekanisme kriptografi yang digunakan untuk menjamin otentikasi (memastikan identitas pengirim), integritas (memastikan data tidak diubah), dan non-repudiasi (pengirim tidak dapat menyangkal telah mengirim data) suatu pesan atau dokumen. Berbeda dengan enkripsi, yang bertujuan menyembunyikan isi pesan, tanda tangan digital bertujuan memverifikasi asal dan keutuhan pesan. Prosesnya selalu menggunakan kriptografi kunci asimetris (seperti RSA atau DSA). Pertama, pengirim menghitung nilai hash kriptografi (seperti SHA-256) dari dokumen, yang menghasilkan "sidik jari" unik dari data tersebut. Kedua, nilai hash ini kemudian dienkripsi menggunakan Kunci Privat milik pengirim—hasil enkripsi inilah yang disebut sebagai Tanda Tangan Digital. Pihak penerima kemudian memverifikasi tanda tangan tersebut dengan dua langkah: mendekripsi tanda tangan menggunakan Kunci Publik pengirim untuk mendapatkan kembali nilai hash awal, dan membandingkannya dengan nilai hash yang ia hitung sendiri dari dokumen yang diterima. Jika kedua nilai hash identik, tanda tangan dianggap valid, membuktikan bahwa pesan berasal dari pemilik kunci privat tersebut dan isinya tidak mengalami perubahan.

---

## 3. Alat dan Bahan
- Python 3.x  
- Visual Studio Code / editor lain  
- Git dan akun GitHub  
- Library tambahan pycryptodome

---

## 4. Langkah Percobaan
1. Membuat file Digital Signature.py di folder praktikum/week9-Digital Signature/src/.
2. Menyalin kode program dari panduan praktikum.
3. Menjalankan program dengan perintah Digital Signature.py.
   
---

## 5. Source Code
from Crypto.PublicKey import RSA
from Crypto.Signature import pkcs1_15
from Crypto.Hash import SHA256

# Generate pasangan kunci RSA
key = RSA.generate(2048)
private_key = key
public_key = key.publickey()

# Pesan yang akan ditandatangani
message = b"Hello, ini pesan penting."
h = SHA256.new(message)

# Buat tanda tangan dengan private key
signature = pkcs1_15.new(private_key).sign(h)
print("Signature:", signature.hex())
try:
    pkcs1_15.new(public_key).verify(h, signature)
    print("Verifikasi berhasil: tanda tangan valid.")
except (ValueError, TypeError):
    print("Verifikasi gagal: tanda tangan tidak valid.")
    # Modifikasi pesan
fake_message = b"Hello, ini pesan palsu."
h_fake = SHA256.new(fake_message)

try:
    pkcs1_15.new(public_key).verify(h_fake, signature)
    print("Verifikasi berhasil (seharusnya gagal).")
except (ValueError, TypeError):
    print("Verifikasi gagal: tanda tangan tidak cocok dengan pesan.")

---

## 6. Hasil dan Pembahasan
![Screenshot source code week9](https://github.com/user-attachments/assets/cbbccf12-69b0-4a33-b61d-d28d45181ad2)


---

## 7. Jawaban Pertanyaan
- Pertanyaan 1: Perbedaan utama antara enkripsi RSA dan tanda tangan digital RSA terletak pada tujuan penggunaan dan peran kunci publik dan privat yang dipertukarkan. Dalam enkripsi RSA, tujuannya adalah kerahasiaan data: pesan dienkripsi menggunakan Kunci Publik penerima, dan hanya dapat didekripsi oleh Kunci Privat penerima. Sebaliknya, dalam tanda tangan digital RSA, tujuannya adalah otentikasi, integritas, dan non-repudiasi: pesan (hash pesan) dienkripsi (ditandatangani) menggunakan Kunci Privat pengirim, dan diverifikasi (didekripsi) menggunakan Kunci Publik pengirim. Singkatnya, enkripsi RSA menggunakan kunci publik untuk mengunci data bagi orang lain, sedangkan tanda tangan digital RSA menggunakan kunci privat untuk membuktikan identitas diri sendiri.  
- Pertanyaan 2: Tanda tangan digital menjamin integritas dan otentikasi pesan secara efektif karena prosesnya didasarkan pada dua komponen kriptografi yang unik. Integritas dijamin melalui penggunaan fungsi hash kriptografi (seperti SHA-256), yang menghasilkan nilai hash unik dari pesan; jika bahkan satu bit pesan diubah selama transmisi, nilai hash yang dihitung ulang oleh penerima akan berbeda dari hash yang ditandatangani, sehingga menunjukkan adanya perusakan. Sementara itu, otentikasi dijamin karena hanya Kunci Privat milik pengirim yang dapat menghasilkan tanda tangan tersebut, dan hanya Kunci Publik pengirim yang terkait yang dapat memverifikasinya. Ketika penerima berhasil mendekripsi tanda tangan menggunakan Kunci Publik pengirim, hal itu secara matematis membuktikan bahwa pemilik Kunci Privat (yaitu, pengirim yang sah) adalah satu-satunya entitas yang menandatangani pesan tersebut.
- Pertanyaan 3: Peran Certificate Authority (CA) dalam sistem tanda tangan digital modern sangatlah krusial sebagai pihak ketiga yang dipercaya dan independen. CA bertugas untuk mengikatkan Kunci Publik seseorang atau suatu entitas (server, perusahaan) dengan identitas yang sebenarnya. Proses ini dilakukan melalui penerbitan Sertifikat Digital (X.509), yang berisi Kunci Publik dan identitas pemilik yang telah diverifikasi, kemudian ditandatangani menggunakan Kunci Privat milik CA itu sendiri. Dengan demikian, CA menyelesaikan masalah kepercayaan kunci publik: ketika seseorang menerima pesan yang ditandatangani, mereka tidak hanya memverifikasi tanda tangan menggunakan Kunci Publik pengirim, tetapi juga memverifikasi bahwa Kunci Publik itu sendiri adalah asli dan milik pengirim yang diklaim, dengan cara memeriksa tanda tangan CA pada Sertifikat Digital tersebut. Ini memastikan bahwa serangan Man-in-the-Middle dapat dicegah dan sistem dapat beroperasi secara global dengan kepercayaan penuh.

---

## 8. Kesimpulan
Tanda tangan digital merupakan fungsi krusial dari kriptografi kunci asimetris (seperti RSA atau DSA) yang memiliki tujuan tunggal untuk menjamin otentikasi, integritas, dan non-repudiasi suatu data. Mekanismenya berpusat pada penggunaan Kunci Privat pengirim untuk "menandatangani" (enkripsi) nilai hash unik dari pesan, yang secara matematis membuktikan bahwa hanya pemilik kunci yang sah yang mengirimkannya (otentikasi). Pada saat verifikasi, Kunci Publik yang sesuai digunakan untuk mendekripsi tanda tangan dan membandingkannya dengan hash yang dihitung ulang dari pesan; jika cocok, integritas pesan terjamin. Dalam sistem modern, Certificate Authority (CA) melengkapi proses ini dengan memverifikasi dan mengikatkan identitas asli pengirim dengan Kunci Publiknya, sehingga Tanda Tangan Digital menjadi standar global untuk membangun kepercayaan pada komunikasi digital.

---

## 9. Daftar Pustaka 
- Juniar Hutagalung, Puji Sari Ramadhan, dan Sarah Juliana Sihombing. *Keamanan Data Menggunakan Secure Hashing Algorithm (SHA)-256 dan Rivest Shamir Adleman (RSA) pada Digital Signature*.
- Sahl Fawzy Sutopo, Rini Marwati, dan Cece Kustiawan. *Implementasi Digital Signature Algorithm (DSA) Menggunakan Secure Hash Algorithm-256 (SHA-256) Pada Media Gambar* 

---

## 10. Commit Log
commit abc12345
Author: Khoirun Nisa Az-Zahra <jahraaaaaa.13@gmail.com>
Date:   2025-12-16

    week2-cryptosystem: implementasi Caesar Cipher dan laporan )
```

# Laporan Praktikum Kriptografi
Minggu ke-: 6  
Topik: Chipher Modern (DES,AES,RSA)  
Nama: Khoirun Nisa Az-Zahra  
NIM: 230202761
Kelas: 5IKRB  

---

## 1. Tujuan
1. Mengimplementasikan algoritma DES untuk blok data sederhana.
2. Menerapkan algoritma AES dengan panjang kunci 128 bit.
3. Menjelaskan proses pembangkitan kunci publik dan privat pada algoritma RS**.

---

## 2. Dasar Teori
Dasar teori kriptografi modern berakar pada konsep sistematis yang jauh lebih kompleks dan aman dibandingkan metode klasik. Cipher modern terbagi menjadi dua kategori utama: kriptografi kunci simetris (seperti AES) dan kriptografi kunci asimetris atau kriptografi kunci publik (seperti RSA dan Elliptic Curve Cryptography/ECC). Kunci simetris menggunakan kunci yang sama untuk enkripsi dan dekripsi, mengandalkan kecepatan dan efisiensi, dan strukturnya didasarkan pada operasi berulang dari substitusi dan permutasi (prinsip Shannon yang dikenal sebagai confusion dan diffusion).

Sementara itu, kunci asimetris menggunakan sepasang kunci—satu publik untuk enkripsi dan satu privat untuk dekripsi—yang secara matematis terkait, dengan keamanan yang didasarkan pada masalah matematika yang sulit dipecahkan (seperti faktorisasi bilangan prima atau masalah logaritma diskret), yang memungkinkan komunikasi aman tanpa pertukaran kunci rahasia sebelumnya. Selain enkripsi, kriptografi modern mencakup fungsi hashing kriptografi (misalnya, SHA-256) untuk integritas data dan tanda tangan digital untuk otentikasi dan non-repudiasi, menjadikan keamanan tidak hanya bergantung pada kerahasiaan tetapi juga pada integritas, otentikasi, dan ketersediaan data.

---

## 3. Alat dan Bahan
- Python 3.x  
- Visual Studio Code 
- Git dan akun GitHub  

---

## 4. Langkah Percobaan
1. Membuat file AES.py, RSA.py, DES.py di folder praktikum/week6-cipher modern/src/.
2. Menyalin kode program dari panduan praktikum.
3. Menjalankan program dengan perintah.

---

## 5. Source Code
## a. Implementasi DES
from Crypto.Cipher import DES
from Crypto.Random import get_random_bytes

key = get_random_bytes(8)  # kunci 64 bit (8 byte)
cipher = DES.new(key, DES.MODE_ECB)

plaintext = b"ABCDEFGH"
ciphertext = cipher.encrypt(plaintext)
print("Ciphertext:", ciphertext)

decipher = DES.new(key, DES.MODE_ECB)
decrypted = decipher.decrypt(ciphertext)
print("Decrypted:", decrypted)

## b. Implementasi AES
from Crypto.Cipher import AES
from Crypto.Random import get_random_bytes

key = get_random_bytes(16)  # 128 bit key
cipher = AES.new(key, AES.MODE_EAX)

plaintext = b"Modern Cipher AES Example"
ciphertext, tag = cipher.encrypt_and_digest(plaintext)

print("Ciphertext:", ciphertext)

# Dekripsi
cipher_dec = AES.new(key, AES.MODE_EAX, nonce=cipher.nonce)
decrypted = cipher_dec.decrypt(ciphertext)
print("Decrypted:", decrypted.decode())

## c. Implementasi RSA
from Crypto.PublicKey import RSA
from Crypto.Cipher import PKCS1_OAEP

# Generate key pair
key = RSA.generate(2048)
private_key = key
public_key = key.publickey()

# Enkripsi dengan public key
cipher_rsa = PKCS1_OAEP.new(public_key)
plaintext = b"RSA Example"
ciphertext = cipher_rsa.encrypt(plaintext)
print("Ciphertext:", ciphertext)

# Dekripsi dengan private key
decipher_rsa = PKCS1_OAEP.new(private_key)
decrypted = decipher_rsa.decrypt(ciphertext)
print("Decrypted:", decrypted.decode())


---

## 6. Hasil dan Pembahasan
## a. Implementasi DES
![Implementasi DES](https://github.com/user-attachments/assets/b218ead7-6c47-48a9-b8fa-366a3f0f421b)

## b. Implementasi AES
![Implementasi AES](https://github.com/user-attachments/assets/8e09659e-18ed-4539-8efe-53ba0f166846)

## c. Implementasi RSA
![Implementasi RSA](https://github.com/user-attachments/assets/50e7c425-a9ff-42e0-9e10-47908021e995)




---

## 7. Jawaban Pertanyaan
- Pertanyaan 1: Perbedaan mendasar antara ketiga algoritma ini terletak pada jenis kunci dan tingkat keamanan yang ditawarkan. DES (Data Encryption Standard) dan AES (Advanced Encryption Standard) adalah algoritma kunci simetris, artinya mereka menggunakan satu kunci rahasia yang sama untuk enkripsi dan dekripsi. Perbedaan keamanan mereka terletak pada panjang kunci: DES (56-bit) kini dianggap tidak aman dan telah dihentikan, sedangkan AES menggunakan kunci yang jauh lebih panjang (128-bit, 192-bit, atau 256-bit) dan menjadi standar keamanan global saat ini. Sebaliknya, RSA (Rivest–Shamir–Adleman) adalah algoritma kunci asimetris atau kunci publik, yang selalu menggunakan sepasang kunci berbeda (publik untuk enkripsi, privat untuk dekripsi). RSA menggunakan panjang kunci yang jauh lebih besar (misalnya, 2048-bit ke atas) dan bergantung pada kesulitan memfaktorkan bilangan prima besar untuk keamanan, menjadikannya ideal untuk pertukaran kunci dan tanda tangan digital, meskipun lebih lambat untuk mengenkripsi data dalam jumlah besar dibandingkan dengan AES. 
- Pertanyaan 2: AES lebih banyak digunakan di era modern karena kelemahan utama DES (Data Encryption Standard) terletak pada panjang kunci 56-bit yang pendek, menjadikannya sangat rentan terhadap serangan brute-force (mencoba semua kemungkinan kunci) menggunakan daya komputasi modern. Sebaliknya, AES (Advanced Encryption Standard), sebagai pengganti DES dan standar enkripsi saat ini, menawarkan tingkat keamanan yang jauh lebih tinggi melalui dukungan panjang kunci 128-bit, 192-bit, atau 256-bit. Jumlah kombinasi kunci yang sangat besar pada AES, terutama pada varian 256-bit (2^{256}), menjadikannya mustahil untuk dipecahkan dalam jangka waktu yang wajar bahkan dengan komputer tercepat sekalipun. Selain itu, AES dirancang dengan struktur matematis yang lebih modern (Substitution-Permutation Network) yang tidak hanya lebih aman, tetapi juga memiliki efisiensi kinerja dan kecepatan yang lebih baik di berbagai platform perangkat keras dan lunak, menjadikannya pilihan ideal untuk melindungi data sensitif secara global.
- Pertanyaan 3: RSA (Rivest–Shamir–Adleman) dikategorikan sebagai algoritma asimetris karena secara inheren ia bekerja dengan pasangan kunci yang berbeda dan terkait secara matematis: Kunci Publik yang dapat disebarkan secara bebas untuk enkripsi, dan Kunci Privat yang harus dijaga kerahasiaannya untuk dekripsi. Proses pembangkitan kuncinya didasarkan pada masalah matematika yang sulit dipecahkan, yaitu faktorisasi bilangan prima yang sangat besar. Secara ringkas, prosesnya dimulai dengan memilih dua bilangan prima besar yang berbeda (p dan q), menghitung modulus (n = p x q), dan menghitung nilai yang disebut fungsi Euler's Totient (\phi(n)). Dari nilai-nilai ini, akan ditentukan eksponen publik (e) dan eksponen privat (d), di mana e dan d merupakan invers perkalian modulo \phi(n), sehingga Kunci Publik terdiri dari pasangan (e, n) dan Kunci Privat terdiri dari pasangan (d, n). 

---

## 8. Kesimpulan
Dasar teori kriptografi modern dibangun di atas dua pilar utama: kriptografi kunci simetris dan kriptografi kunci asimetris. Algoritma Simetris (seperti AES) menggunakan satu kunci rahasia untuk enkripsi dan dekripsi, mengutamakan kecepatan dan efisiensi, serta menjadi pilihan utama untuk mengenkripsi data dalam jumlah besar. Sementara itu, Algoritma Asimetris (seperti RSA) menggunakan sepasang kunci (publik dan privat) yang berbeda, mengandalkan kompleksitas matematika (faktorisasi bilangan prima) untuk menyediakan keamanan pertukaran kunci dan otentikasi digital yang tidak dapat dicapai oleh metode simetris. Transisi dari algoritma lama yang rentan (seperti DES dengan 56-bit) ke standar modern yang kuat (seperti AES dengan 128-256 bit) dan penggunaan bersama antara AES dan RSA dalam sistem hybrid modern memastikan kerahasiaan, integritas, dan otentikasi data yang komprehensif.

---

## 9. Daftar Pustaka
- Nurrohmah Zulkarnain, A., Tahir, M., Wahyuningsih, U., et al. *Analisis Proses Enkripsi Algoritma Kriptografi Modern Advanced Encryption Standard (AES)*.
- Basri. *Kriptografi Simetris Dan Asimetris Dalam Perspektif Keamanan Data Dan Kompleksitas Komputasi*.

---

## 10. Commit Log
commit abc12345
Author: Khoirun Nisa Az-Zahra <jahraaaaaa.13@gmail.com>
Date:   2025-12-16

    week2-cryptosystem: implementasi Caesar Cipher dan laporan )
```

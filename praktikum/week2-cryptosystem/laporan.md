# Laporan Praktikum Kriptografi
Minggu ke-: 2  
Topik: Crytosystem  
Nama: Khoirun Nisa Az-Zahra  
NIM: 230202761  
Kelas: 5IKRB  

---

## 1. Tujuan
1. Mengidentifikasi komponen dasar kriptosistem (plaintext, ciphertext, kunci, algoritma).
2. Menggambarkan proses enkripsi dan dekripsi sederhana.
3. Mengklasifikasikan jenis kriptosistem (simetris dan asimetris).

---

## 2. Dasar Teori
1. Membuat skema kriptosistem.
2. Diagram Kriptosistem.
3. Implementasi program sederhana.
4. Simulasi enkripsi & dekripsi menggunakan substitusi sederhana (misalnya Caesar Cipher).

Klasifikasi Simetris dan Asimetris

Kriptografi Simetris menggunakan satu kunci rahasia yang sama untuk mengenkripsi dan mendekripsi data. Keunggulan utamanya adalah kecepatan proses yang sangat tinggi, menjadikannya ideal untuk mengenkripsi data dalam jumlah besar. Namun, kelemahan terbesarnya adalah kesulitan dan risiko dalam distribusi kunci yang aman kepada semua pihak yang berkomunikasi. Contoh algoritmanya adalah AES (Advanced Encryption Standard) dan DES (Data Encryption Standard).

Sebaliknya, Kriptografi Asimetris (atau kunci publik) menggunakan sepasang kunci yang berbeda, yaitu kunci publik untuk enkripsi dan kunci privat untuk dekripsi. Kelebihan utamanya adalah keamanan yang lebih baik dalam distribusi kunci, karena kunci publik dapat dibagikan secara bebas. Namun, kelemahannya adalah proses yang jauh lebih lambat dan membutuhkan daya komputasi yang lebih besar. Contoh algoritmanya adalah RSA (Rivest–Shamir–Adleman) dan ECC (Elliptic Curve Cryptography).


---

## 3. Alat dan Bahan
Python 3.x, Visual Studio Code, akun GitHub, Google chrome Google schollar.

---

## 4. Langkah Percobaan
1. Membuat file simple_crypto.py di folder praktikum/week2-cryptosystem/src/. 
2. Menyalin kode program dari panduan praktikum.
3. Menjalankan program dengan perintah python simple_crypto.py.
4. Membuat ringkasan perbedaan antara kriptosistem simetris dan asimetris.
5. Mengaploud hasil eksekusi di folder praktikum/week2-cryptosistem/screenshots/
6. Menjawab pertanyaan diskusi.

---

## 5. Source Code
file: praktikum/week2-cryptosystem/src/simple_crypto.py

def encrypt(plaintext, key):
    result = ""
    for char in plaintext:
        if char.isalpha():
            shift = 65 if char.isupper() else 97
            result += chr((ord(char) - shift + key) % 26 + shift)
        else:
            result += char
    return result

def decrypt(ciphertext, key):
    result = ""
    for char in ciphertext:
        if char.isalpha():
            shift = 65 if char.isupper() else 97
            result += chr((ord(char) - shift - key) % 26 + shift)
        else:
            result += char
    return result

if __name__ == "__main__":
    message = "Khoirun Nisa Az-Zahra"
    key = 5

    enc = encrypt(message, key)
    dec = decrypt(enc, key)

    print("Plaintext :", message)
    print("Ciphertext:", enc)
    print("Decrypted :", dec)

---

## 6. Hasil dan Pembahasan

Hasil dari program yang diberikan dari github menunjukan bahwa enkripsi yang digunakan adalah caesar chiper dengan hasil enkripsi hanya teks berupa huruf saja yang terenkripsi sedangkan angka tidak terenkripsi, lalu saya modifikasi programnya dengan menambahkan baris : elif char.isdigit(): # Enkripsi Angka (menggeser dalam rentang 0-9) # 48 adalah nilai ASCII untuk '0' shift = 48 # (ord(char) - shift) menghasilkan nilai 0-9 dari digit. # Kemudian geser (shift) dengan key, mod 10, dan tambahkan kembali shift. result += chr((ord(char) - shift + key) % 10 + shift) dengan menambahkan baris tersebut maka sekarang karakter angka pun menjadi ikut terenkripsi juga. untuk perbandingan hasilnya bisa dilihat pada tangkapan layar berikut

<img width="1366" height="768" alt="Screenshot" src="https://github.com/user-attachments/assets/1c6f844d-46d3-4ff3-a66c-e023d6ae8b3a" />

<img width="1366" height="768" alt="Screenshot source code" src="https://github.com/user-attachments/assets/310c443a-0c03-463e-964a-da92cfa475f1" />

---

## 7. Jawaban Pertanyaan
1. a. Algoritma Kriptografi (Cryptographic Algorithm) adalah prosedur matematis yang digunakan untuk enkripsi dan dekripsi.
   b. Kunci (Key) adalah informasi rahasia yang digunakan bersama dengan algoritma untuk mengunci (enkripsi) dan membuka (dekripsi) data.
   c. Teks Biasa (Plaintext) adalah data asli yang belum dienkripsi, yaitu data yang mudah dibaca dan dipahami.
   d. Teks Tersandi (Ciphertext) adalah hasil dari proses enkripsi, yaitu data yang sudah diubah menjadi bentuk tidak dapat dibaca tanpa kunci yang benar.
   e. Protokol Kriptografi (Cryptographic Protocol) adalah serangkaian langkah atau prosedur yang menentukan bagaimana algoritma dan kunci diterapkan, seperti urutan operasi atau cara pertukaran kunci.
   
2. A. Sistem simetris (kunci rahasia tunggal) memiliki kelebihan utama yaitu kecepatan enkripsi dan dekripsi yang jauh lebih tinggi dan lebih efisien untuk data dalam jumlah besar. Namun, kelemahan terbesarnya adalah masalah distribusi kunci, di mana kunci rahasia yang sama harus dibagikan melalui saluran yang aman kepada setiap pihak yang berkomunikasi, yang menimbulkan risiko kebocoran.
   B. Sistem asimetris (kunci publik/privat) memiliki kelebihan utama dalam hal kemudahan distribusi kunci yang aman, karena kunci publik dapat dibagikan secara bebas dan hanya kunci privat yang harus dirahasiakan oleh pemiliknya, menjadikannya ideal untuk komunikasi jarak jauh, autentikasi, dan tanda tangan digital. Meskipun demikian, kelemahan signifikan dari sistem asimetris adalah proses enkripsi dan dekripsi yang jauh lebih lambat dan membutuhkan daya komputasi yang lebih besar, karena melibatkan operasi matematis yang lebih kompleks.
   Oleh karena itu, dalam praktiknya sering digunakan sistem hibrida, di mana sistem asimetris digunakan untuk menukar kunci simetris secara aman, dan selanjutnya sistem simetris yang cepat digunakan untuk mengenkripsi data.
   
4. Karena kunci yang digunakan untuk enkripsi dan dekripsi adalah sama (kunci tunggal) dan harus dibagikan (dipertukarkan) antara pengirim dan penerima melalui saluran yang sudah aman (out-of-band).
    

---

## 8. Kesimpulan

Algoritma Kriptografi, Kunci, Plaintext, dan Ciphertext bekerja secara terpadu untuk menjamin keamanan data. Perbedaan mendasar antara dua jenis utama sistem kriptografi terlihat jelas: sistem Simetris seperti AES dan DES unggul dalam kecepatan enkripsi/dekripsi yang tinggi karena menggunakan satu kunci, namun memiliki kelemahan signifikan dalam hal distribusi kunci yang aman. Sebaliknya, sistem Asimetris seperti RSA dan ECC menawarkan solusi distribusi kunci yang jauh lebih aman melalui penggunaan pasangan kunci publik dan privat, namun dengan konsekuensi kecepatan proses yang lebih lambat. Secara praktis, sebagian besar implementasi keamanan modern mengadopsi pendekatan hibrida, memanfaatkan keunggulan kriptografi asimetris untuk menukar kunci rahasia, kemudian beralih ke kriptografi simetris yang lebih cepat untuk mengenkripsi volume data yang besar, menciptakan keseimbangan optimal antara keamanan, kerahasiaan, dan efisiensi.

---

## 9. Daftar Pustaka

---

## 10. Commit Log

commit abc12345
Author: Khoirun Nisa Az-Zahra jahraaaaa.13@gmail.com
Date:   2025-09-21

    week2-cryptosystem: implementasi Caesar Cipher dan laporan )
```

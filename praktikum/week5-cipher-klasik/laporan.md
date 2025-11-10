# Laporan Praktikum Kriptografi
Minggu ke-: 5
Topik: Cipher Klasik(Caesar,Vigenere,Tranposisi)  
Nama: Khoirun Nisa Az-Zahra  
NIM: 230202761  
Kelas: 5IKRB  

---

## 1. Tujuan
1. Menerapkan algoritma Caesar Cipher untuk enkripsi dan dekripsi teks.
2. Menerapkan algoritma Vigenère Cipher dengan variasi kunci.
3. Mengimplementasikan algoritma transposisi sederhana.
4. Menjelaskan kelemahan algoritma kriptografi klasik dalam konteks keamanan modern.

---

## 2. Dasar Teori
Cipher Klasik merujuk pada metode enkripsi dan dekripsi yang digunakan sebelum munculnya kriptografi elektronik dan digital modern. Teknik-teknik ini umumnya berbasis karakter dan diimplementasikan secara manual atau dengan bantuan perangkat mekanis sederhana. Dasar teori Cipher Klasik berfokus pada dua prinsip utama: substitusi dan transposisi. Cipher substitusi melibatkan penggantian setiap huruf dalam pesan asli (teks biasa) dengan huruf atau simbol lain secara sistematis; contohnya termasuk Caesar Cipher dan Vigenère Cipher. Sementara itu, cipher transposisi melibatkan pengubahan urutan huruf dalam pesan, tanpa mengubah huruf itu sendiri; contohnya adalah Rail Fence Cipher dan Columnar Transposition Cipher. Meskipun dianggap tidak aman terhadap serangan kriptanalisis modern, terutama analisis frekuensi, Cipher Klasik meletakkan dasar konseptual untuk semua kriptografi berikutnya, memperkenalkan konsep kunci enkripsi, dan menjadi tonggak sejarah penting dalam pengembangan ilmu pengamanan komunikasi.

---

## 3. Alat dan Bahan
- Python 3.x
- Visual Studio Code / editor lain
- Git dan akun GitHub

---

## 4. Langkah Percobaan
1. Membuat file caesar_cipher.py di folder praktikum/week5-cryptosystem/src/.
2. Menyalin kode program dari panduan praktikum.
3. Menjalankan program dengan perintah python caesar_cipher.py.)

---

## 5. Source Code
## Langkah 1 — Implementasi Caesar Cipher
def caesar_encrypt(plaintext, key):
    result = ""
    for char in plaintext:
        if char.isalpha():
            shift = 65 if char.isupper() else 97
            result += chr((ord(char) - shift + key) % 26 + shift)
        else:
            result += char
    return result

def caesar_decrypt(ciphertext, key):
    return caesar_encrypt(ciphertext, -key)
## Contoh uji
msg = "CLASSIC CIPHER"
key = 3
enc = caesar_encrypt(msg, key)
dec = caesar_decrypt(enc, key)
print("Plaintext :", msg)
print("Ciphertext:", enc)
print("Decrypted :", dec)
## Langkah 2 — Implementasi Vigenère Cipher
def transpose_encrypt(plaintext, key=5):
    ciphertext = [''] * key
    for col in range(key):
        pointer = col
        while pointer < len(plaintext):
            ciphertext[col] += plaintext[pointer]
            pointer += key
    return ''.join(ciphertext)

def transpose_decrypt(ciphertext, key=5):
    num_of_cols = int(len(ciphertext) / key + 0.9999)
    num_of_rows = key
    num_of_shaded_boxes = (num_of_cols * num_of_rows) - len(ciphertext)
    plaintext = [''] * num_of_cols
    col = 0
    row = 0
    for symbol in ciphertext:
        plaintext[col] += symbol
        col += 1
        if (col == num_of_cols) or (col == num_of_cols - 1 and row >= num_of_rows - num_of_shaded_boxes):
            col = 0
            row += 1
    return ''.join(plaintext)
## Contoh uji
msg = "TRANSPOSITIONCIPHER"
enc = transpose_encrypt(msg, key=5)
dec = transpose_decrypt(enc, key=5)
print("Plaintext :", msg)
print("Ciphertext:", enc)
print("Decrypted :", dec)
## Langkah 3 — Implementasi Transposisi Sederhana
def transpose_encrypt(plaintext, key=5):
    ciphertext = [''] * key
    for col in range(key):
        pointer = col
        while pointer < len(plaintext):
            ciphertext[col] += plaintext[pointer]
            pointer += key
    return ''.join(ciphertext)

def transpose_decrypt(ciphertext, key=5):
    num_of_cols = int(len(ciphertext) / key + 0.9999)
    num_of_rows = key
    num_of_shaded_boxes = (num_of_cols * num_of_rows) - len(ciphertext)
    plaintext = [''] * num_of_cols
    col = 0
    row = 0
    for symbol in ciphertext:
        plaintext[col] += symbol
        col += 1
        if (col == num_of_cols) or (col == num_of_cols - 1 and row >= num_of_rows - num_of_shaded_boxes):
            col = 0
            row += 1
    return ''.join(plaintext)
## Contoh uji
msg = "TRANSPOSITIONCIPHER"
enc = transpose_encrypt(msg, key=5)
dec = transpose_decrypt(enc, key=5)
print("Plaintext :", msg)
print("Ciphertext:", enc)
print("Decrypted :", dec)




---

## 6. Hasil dan Pembahasan
1. Langkah 1 — Implementasi Caesar Cipher
<img width="1366" height="768" alt="source code L1" src="https://github.com/user-attachments/assets/05e87e68-41ee-4ebc-95c4-77cce448558a" />

2. Langkah 2 — Implementasi Vigenère Cipher
<img width="1366" height="768" alt="source code L2" src="https://github.com/user-attachments/assets/02b0a334-60fa-4147-a997-4eb2a80beadc" />

3. Langkah 3 — Implementasi Transposisi Sederhana
<img width="1366" height="768" alt="source code L3" src="https://github.com/user-attachments/assets/11dcb266-53b5-472f-a08a-ca6208fe141c" />

   
---

## 7. Jawaban Pertanyaan 
- Pertanyaan 1: Apa kelemahan utama algoritma Caesar Cipher dan Vigenère Cipher?
Kelemahan utama kedua algoritma sandi klasik, Caesar Cipher dan Vigenère Cipher, terletak pada kerentanan mereka terhadap kriptanalisis berbasis statistik. Untuk Caesar Cipher, kelemahannya sangat parah karena hanya menggunakan pergeseran tunggal dan tetap (kunci berukuran 1) untuk setiap huruf, sehingga sangat rentan terhadap analisis frekuensi; kriptanalis dapat dengan mudah mengidentifikasi pergeseran yang digunakan dengan mencocokkan frekuensi huruf yang paling sering muncul di sandi (misalnya, 'E' atau 'A') dengan frekuensi huruf di bahasa teks asli. Sementara itu, Vigenère Cipher memang jauh lebih kuat karena menggunakan kunci multi-alfabet yang berulang, sehingga menyamarkan frekuensi huruf tunggal; namun, ia masih rentan terhadap teknik yang dikenal sebagai uji Kasiski atau metode pencocokan indeks yang dapat menentukan panjang kunci, setelah itu sandi tersebut dapat dipecah menjadi beberapa sandi Caesar terpisah (polyalphabetic substitution menjadi monoalphabetic substitution), memungkinkan analisis frekuensi standar diterapkan untuk setiap sandi individu. 
- Pertanyaan 2: Mengapa cipher klasik mudah diserang dengan analisis frekuensi?
Cipher klasik mudah diserang dengan analisis frekuensi karena mereka gagal menyembunyikan distribusi frekuensi statistik dari bahasa teks asli . Kebanyakan bahasa alami, seperti Bahasa Inggris atau Bahasa Indonesia, memiliki pola yang sangat khas di mana huruf tertentu (misalnya, 'E', 'T', 'A' dalam Bahasa Inggris, atau 'A', 'I', 'N' dalam Bahasa Indonesia) muncul jauh lebih sering daripada yang lain. Cipher seperti Caesar Cipher dan cipher substitusi monoalfabetik lainnya mempertahankan rasio frekuensi ini secara utuh; mereka hanya mengganti satu huruf dengan huruf lain secara konsisten, sehingga huruf sandi yang paling sering muncul akan sesuai langsung dengan huruf teks biasa yang paling sering muncul. Bahkan cipher yang lebih kompleks seperti Vigenère Cipher, meskipun menggunakan banyak sandi (polialfabetik), masih menggunakan kunci yang berulang, yang memungkinkan kriptanalis untuk menguraikan sandi menjadi beberapa sandi tunggal yang lebih kecil, yang kemudian dapat dipecahkan menggunakan analisis frekuensi pada setiap bagian, sehingga secara fundamental masih mengekspos pola statistik dasar dari pesan.
- Pertanyaan 3: Bandingkan kelebihan dan kelemahan cipher substitusi vs transposisi.
Perbedaan utama antara keduanya terletak pada cara mereka menyembunyikan pesan. Cipher Substitusi memiliki kelebihan karena ia mengubah setiap karakter teks biasa menjadi karakter yang berbeda, yang paling rumit seperti Vigenère Cipher dapat menyamarkan frekuensi huruf tunggal. Namun, kelemahan utamanya adalah keterbatasannya dalam mengubah pola statistik, menjadikannya rentan terhadap analisis frekuensi atau analisis kunci berulang, terutama pada versi monoalfabetik yang sederhana. Sebaliknya, Cipher Transposisi memiliki kelebihan karena ia mempertahankan semua karakter asli dan hanya mengacak urutan kemunculannya, sehingga pola frekuensi huruf tunggal tetap sama seperti teks biasa; hal ini membuat kriptanalisis berdasarkan frekuensi huruf tunggal menjadi tidak efektif. Akan tetapi, justru kelemahan utama transposisi adalah frekuensi huruf yang tidak berubah, dan ia rentan terhadap serangan yang berfokus pada analisis bigram atau trigram (pasangan atau tiga serangkai huruf) serta pencarian anagram dan pola umum yang dapat mengarah pada penemuan matriks atau kolom pengacakan. Pada akhirnya, kedua jenis cipher ini sering dikombinasikan (product ciphers) untuk menggabungkan keuntungan keduanya yaitu mengubah karakter (substitusi) dan mengacak posisi (transposisi) guna mencapai tingkat keamanan yang jauh lebih tinggi.

---

## 8. Kesimpulan
Cipher Klasik adalah fondasi historis kriptografi yang didominasi oleh dua teknik utama: substitusi (mengganti karakter, seperti Caesar dan Vigenère) dan transposisi (mengubah urutan karakter, seperti Rail Fence). Kelemahan mendasar mereka adalah kerentanan terhadap analisis frekuensi dan teknik statistik lainnya karena keterbatasan manual atau mekanisnya dalam mengacak pola bahasa. Meskipun tidak lagi digunakan untuk pengamanan data modern karena tingkat keamanannya yang rendah, Cipher Klasik sangat penting karena telah memperkenalkan konsep kunci, enkripsi, dan dekripsi, membuka jalan bagi pengembangan algoritma kriptografi yang jauh lebih kompleks dan aman di era digital saat ini.

---

## 9. Daftar Pustaka
1. Sasono, D. M. A., Tahir, M., M. V., F. A., Azizah, M., Utami, L. F., & Septiana, N. (2023). Jurnal Informasi, Sains dan Teknologi (ISAINTEK), 6(1), 72–77. https://isaintek.polinef.ac.id/index.php/isaintek/article/view/93
2. Harahap, M. K. (2016). InfoTekJar: Jurnal Nasional Informatika dan Teknologi Jaringan, 1(1), 61–64. https://ojs23.uisu.ac.id/index.php/infotekjar/article/view/43
---

## 10. Commit Log
commit week5-chiper klasik
Author: Khoirun Nisa Az-Zahra <jahraaaaaa.13@gmail.com>
Date:   2025-11-11

    week5-chiper klasik: implementasi Caesar Cipher dan laporan )


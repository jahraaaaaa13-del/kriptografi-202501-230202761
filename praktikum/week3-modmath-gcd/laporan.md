# Laporan Praktikum Kriptografi
Minggu ke-: 3 
Topik: Modular Math  
Nama: Khoirun Nisa Az-Zahra  
NIM: 230202761  
Kelas: 5IKRB  

---

## 1. Tujuan
1. Menyelesaikan operasi aritmetika modular.
2. Menentukan bilangan prima dan menghitung GCD (Greatest Common Divisor).
3. Menerapkan logaritma diskrit sederhana dalam simulasi kriptografi

---

## 2. Dasar Teori
Aritmetika modular adalah cabang matematika yang mempelajari operasi bilangan berdasarkan sisa hasil bagi terhadap suatu bilangan tertentu yang disebut modulus. Dalam sistem ini, dua bilangan dianggap kongruen jika keduanya memiliki sisa pembagian yang sama terhadap modulus tersebut, yang dinyatakan sebagai 𝑎 ≡ 𝑏 (mod 𝑛). Aritmetika modular memungkinkan operasi penjumlahan, pengurangan, perkalian, dan perpangkatan dilakukan dalam ruang bilangan yang terbatas oleh modulus. Konsep ini sangat penting dalam ilmu komputer dan kriptografi karena memungkinkan perhitungan dengan bilangan besar secara efisien dan aman. Misalnya, dalam kriptografi kunci publik seperti RSA dan Diffie–Hellman, operasi modular digunakan untuk mengenkripsi dan mendekripsi pesan tanpa perlu menangani bilangan yang terlalu besar secara langsung, sehingga menjaga keamanan dan efisiensi sistem.

---

## 3. Alat dan Bahan
- Python 3.x  
- Visual Studio Code / editor lain  
- Git dan akun GitHub  

---

## 4. Langkah Percobaan
(Tuliskan langkah yang dilakukan sesuai instruksi.  
Contoh format:
1. Membuat file modular_math.py di folder praktikum/week3-modmath/src/.
2. Menyalin kode program dari panduan praktikum.
3. Menjalankan program dengan perintah python modular_math.py.)

---

## 5. Source Code
## 1. Langkah 1-Aritmatika Modular

def mod_add(a, b, n): return (a + b) % n
def mod_sub(a, b, n): return (a - b) % n
def mod_mul(a, b, n): return (a * b) % n
def mod_exp(base, exp, n): return pow(base, exp, n)  # eksponensiasi modular

print("7 + 5 mod 12 =", mod_add(7, 5, 12))
print("7 * 5 mod 12 =", mod_mul(7, 5, 12))
print("7^128 mod 13 =", mod_exp(7, 128, 13))

## 2. Langkah 2-GCD & Algoritma Euclidean

def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a

print("gcd(54, 24) =", gcd(54, 24))

## 3. Langkah 3-Extend Euclidean Algorthm

def egcd(a, b):
    if a == 0:
        return b, 0, 1
    g, x1, y1 = egcd(b % a, a)
    return g, y1 - (b // a) * x1, x1

def modinv(a, n):
    g, x, _ = egcd(a, n)
    if g != 1:
        return None
    return x % n

print("Invers 3 mod 11 =", modinv(3, 11))  # hasil: 4

## 4. Langkah 4-Discrete Log

def discrete_log(a, b, n):
    for x in range(n):
        if pow(a, x, n) == b:
            return x
    return None

print("3^x ≡ 4 (mod 7), x =", discrete_log(3, 4, 7))  # hasil: 4

## Source Code Keseluruhan

def mod_add(a, b, n): return (a + b) % n
def mod_sub(a, b, n): return (a - b) % n
def mod_mul(a, b, n): return (a * b) % n
def mod_exp(base, exp, n): return pow(base, exp, n)  # eksponensiasi modular

print("7 + 5 mod 12 =", mod_add(7, 5, 12))
print("7 * 5 mod 12 =", mod_mul(7, 5, 12))
print("7^128 mod 13 =", mod_exp(7, 128, 13))
def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a

print("gcd(54, 24) =", gcd(54, 24))
def egcd(a, b):
    if a == 0:
        return b, 0, 1
    g, x1, y1 = egcd(b % a, a)
    return g, y1 - (b // a) * x1, x1

def modinv(a, n):
    g, x, _ = egcd(a, n)
    if g != 1:
        return None
    return x % n

print("Invers 3 mod 11 =", modinv(3, 11))  # hasil: 4
def discrete_log(a, b, n):
    for x in range(n):
        if pow(a, x, n) == b:
            return x
    return None

print("3^x ≡ 4 (mod 7), x =", discrete_log(3, 4, 7))  # hasil: 4

---

## 6. Hasil dan Pembahasan
Hasil eksekusi program modmath

<img width="1366" height="768" alt="Screenshot source code week3" src="https://github.com/user-attachments/assets/cb6988fa-e640-4c44-a503-f83e8f500b18" />

Penjelasan: program berjalan sesuai instruksi tanpa adanya bug.

---

## 7. Jawaban Pertanyaan 
- Pertanyaan 1: Apa peran aritmetika modular dalam kriptografi modern?

Aritmetika modular berperan penting dalam kriptografi modern karena menjadi dasar bagi banyak algoritma enkripsi dan tanda tangan digital. Operasi seperti perpangkatan dan invers modulo digunakan untuk:

1. Menjaga keamanan data – sulit membalikkan operasi tanpa kunci rahasia (contohnya dalam RSA).
2. Efisiensi komputasi – memungkinkan perhitungan besar dilakukan dengan cepat dan aman.
3. Membangun fungsi satu arah – penting untuk enkripsi, hashing, dan autentikasi.

Contohnya, algoritma RSA, Diffie–Hellman, dan ElGamal semuanya bergantung pada aritmetika modular.
  
- Pertanyaan 2: Mengapa invers modular penting dalam algoritma kunci publik (misalnya RSA)?

Invers modular penting dalam algoritma kunci publik seperti RSA karena digunakan untuk menghasilkan kunci dekripsi yang dapat membalikkan proses enkripsi. Dalam RSA, setelah memilih dua bilangan prima besar dan menghitung nilai totient-nya, diperlukan sebuah bilangan ( d ) yang merupakan invers modular dari ( e ) terhadap totient tersebut, sehingga memenuhi persamaan ( e \times d \equiv 1 \ (\text{mod } \varphi(n)) ). Nilai ( d ) inilah yang menjadi kunci privat. Tanpa invers modular, tidak mungkin menemukan pasangan kunci yang memungkinkan pesan terenkripsi dapat dikembalikan ke bentuk aslinya dengan aman. Dengan demikian, invers modular menjamin keterkaitan matematis antara kunci publik dan kunci privat, yang menjadi inti keamanan sistem RSA.

- Pertanyaan 3: Apa tantangan utama dalam menyelesaikan logaritma diskrit untuk modulus besar?

Tantangan utama dalam menyelesaikan logaritma diskrit untuk modulus besar adalah kompleksitas komputasinya yang sangat tinggi. Tidak ada algoritma efisien yang dapat menghitung logaritma diskrit dalam waktu polinomial ketika modulusnya besar, terutama jika bilangan tersebut adalah bilangan prima besar. Hal ini terjadi karena ruang pencarian nilai eksponen sangat luas dan tidak ada pola sederhana yang bisa dimanfaatkan untuk mempercepat perhitungan. Akibatnya, meskipun mudah melakukan perpangkatan modular, mencari eksponen (yakni memecahkan logaritma diskrit) menjadi sangat sulit. Kesulitan inilah yang menjadi dasar keamanan berbagai algoritma kriptografi seperti Diffie–Hellman dan ElGamal.

---

## 8. Kesimpulan
Aritmetika modular merupakan dasar penting dalam berbagai sistem kriptografi modern karena kemampuannya menjaga keamanan data melalui operasi matematika yang sulit dibalik tanpa kunci rahasia. Dengan menggunakan konsep kongruensi dan operasi dalam ruang bilangan terbatas, aritmetika modular memungkinkan pembentukan algoritma yang efisien dan tahan terhadap serangan komputasional. Keberhasilan sistem seperti RSA, Diffie–Hellman, dan ElGamal sangat bergantung pada sifat-sifat aritmetika modular, khususnya kesulitan dalam menyelesaikan operasi seperti invers modular dan logaritma diskrit. Oleh karena itu, pemahaman yang kuat tentang aritmetika modular menjadi landasan utama dalam pengembangan dan penerapan kriptografi yang aman.

---

## 9. Daftar Pustaka
Aminudin dkk "https://jtiik.ub.ac.id/index.php/jtiik/article/view/844?utm_source=chatgpt.com"

---

## 10. Commit Log
commit week3-modmath-gcd
Author: Khoirun Nisa Az-Zahra <jahraaaaaa.13@gmail.com>
Date:   2025-10-27

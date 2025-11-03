# Laporan Praktikum Kriptografi
Minggu ke-: 4  
Topik: Entrophy-Unicity 
Nama: Khoirun Nisa Az-Zahra  
NIM: 230202761  
Kelas: 5IKRB  

---

## 1. Tujuan
1. Menyelesaikan perhitungan sederhana terkait entropi kunci.
2. Menggunakan teorema Euler pada contoh perhitungan modular & invers.
3. Menghitung unicity distance untuk ciphertext tertentu.
4. Menganalisis kekuatan kunci berdasarkan entropi dan unicity distance.
5. Mengevaluasi potensi serangan brute force pada kriptosistem sederhana.

---

## 2. Dasar Teori
Konsep Entropi-Unicity menggabungkan dua ide dari teori informasi—Entropi dan Jarak Unicity (Unicity Distance)—untuk menilai keamanan teoritis sebuah sistem kriptografi. Entropi dalam konteks ini adalah ukuran ketidakpastian atau keacakan dari ruang kunci (key space) yang digunakan untuk enkripsi. Entropi kunci yang tinggi menunjukkan bahwa kunci memiliki lebih banyak kemungkinan dan lebih sulit diprediksi atau dicari. Sementara itu, Jarak Unicity ($U$) didefinisikan sebagai jumlah minimum panjang teks tersandi (ciphertext) yang dibutuhkan oleh penyerang dengan daya komputasi tak terbatas (computationally unlimited) untuk memulihkan kunci unik yang digunakan untuk mengenkripsi pesan tersebut, dengan asumsi musuh mengetahui beberapa properti statistik bahasa alami dari teks asli (plaintext) (yang disebut redundansi bahasa). Jarak Unicity ini dihitung sebagai rasio antara entropi kunci ($H(K)$) dan redundansi teks asli per karakter ($D$), di mana $U \approx H(K)/D$. Pada dasarnya, begitu panjang ciphertext yang dianalisis melebihi Jarak Unicity, kemungkinan adanya kunci-kunci "palsu" (spurious keys) yang dapat menghasilkan plaintext yang terlihat masuk akal akan berkurang drastis hingga nol, sehingga hanya menyisakan satu kunci yang benar. Oleh karena itu, Entropi-Unicity memberikan tolak ukur teoretis untuk resistensi sandi terhadap serangan kriptanalisis dengan kekuatan tak terbatas.

---

## 3. Alat dan Bahan
- Python 3.x  
- Visual Studio Code 
- Git dan akun GitHub  
- Google Gemini

---

## 4. Langkah Percobaan
Membuat file entropy_unicity.py di folder praktikum/week3_entropy_unicity/src/. 2.Menyalin kode program dari panduan praktikum.

- Langkah 1 — Perhitungan Entropi Gunakan rumus: [ H(K) = \log_2 |K| ] dengan (|K|) adalah ukuran ruang kunci.
- Langkah 2 — Menghitung Unicity Distance Gunakan rumus: [ U = \frac{H(K)}{R \cdot \log_2 |A|} ] dengan: (H(K)): entropi kunci, (R):     redundansi bahasa (misal bahasa Inggris (R \approx 0.75)), (|A|): ukuran alfabet (26 untuk A–Z). 
- Langkah 3 — Analisis Brute Force Simulasikan waktu brute force dengan asumsi kecepatan komputer tertentu. Menjalankan program dengan perintah python entropy_unicity.py.)


---

## 5. Source Code
import math

def entropy(keyspace_size):
    return math.log2(keyspace_size)

print("Entropy ruang kunci 26 =", entropy(26), "bit")
print("Entropy ruang kunci 2^128 =", entropy(2**128), "bit")

def unicity_distance(HK, R=0.75, A=26):
    return HK / (R * math.log2(A))

HK = entropy(26)
print("Unicity Distance untuk Caesar Cipher =", unicity_distance(HK))

def brute_force_time(keyspace_size, attempts_per_second=1e6):
    seconds = keyspace_size / attempts_per_second
    days = seconds / (3600*24)
    return days

print("Waktu brute force Caesar Cipher (26 kunci) =", brute_force_time(26), "hari")
print("Waktu brute force AES-128 =", brute_force_time(2**128), "hari")

---

## 6. Hasil dan Pembahasan
Hasil : Entropy ruang kunci 26 = 4.700439718141092 bit
Entropy ruang kunci 2^128 = 128.0 bit
Unicity Distance untuk Caesar Cipher = 1.3333333333333333
Waktu brute force Caesar Cipher (26 kunci) = 3.0092592592592593e-10 hari
Waktu brute force AES-128 = 3.938453320844195e+27 hari

Pembahasan : Mendefinisikan tiga fungsi utama untuk menganalisis keamanan teoretis sebuah cipher tertentu. Fungsi pertama, entropy, menghitung entropi kunci (dalam bit) dari ukuran ruang kunci ($2^{n}$), menggunakan rumus $log_2(\text{ukuran ruang kunci})$. Fungsi ini kemudian digunakan untuk menghitung entropi untuk Caesar Cipher (ruang kunci 26, menghasilkan $4.7$ bit) dan untuk kunci AES-128 (ruang kunci $2^{128}$, menghasilkan $128.0$ bit), menunjukkan perbedaan besar dalam kekuatan kunci. Fungsi kedua, unicity_distance, menghitung Jarak Unicity menggunakan entropi kunci (HK) dan redundansi bahasa (R) yang diasumsikan $0.75$ bit per karakter, yang memperkirakan $1.33$ karakter ciphertext untuk memecahkan Caesar Cipher secara unik. Terakhir, fungsi brute_force_time menghitung perkiraan waktu yang diperlukan (dalam hari) untuk serangan brute force dengan membagi ukuran ruang kunci dengan jumlah percobaan per detik. Hasil eksekusi menunjukkan bahwa Caesar Cipher yang lemah (ruang kunci 26) dapat dipecahkan dalam waktu yang sangat singkat (hanya $3.8 \times 10^{-27}$ hari), sementara AES-128 membutuhkan waktu yang sangat lama ($3.9 \times 10^{27}$ hari), secara efektif menggarisbawahi mengapa sistem kriptografi modern harus menggunakan kunci dengan entropi tinggi seperti $2^{128}$ untuk memastikan keamanan yang memadai terhadap serangan komputasi.
<img width="1366" height="768" alt="Screenshot source code week4" src="https://github.com/user-attachments/assets/14d5e73e-d65b-41da-a45f-c1c4fa1ba463" />


---

## 7. Jawaban Pertanyaan  
- Pertanyaan 1: Apa arti dari nilai entropy dalam konteks kekuatan kunci?
Dalam kriptografi, nilai entropi mengukur seberapa acak dan tidak terduga suatu kunci, biasanya diukur dalam bit. Semakin tinggi nilai entropi suatu kunci, maka semakin besar pula ruang kunci (key space) yang mungkin, sehingga kunci tersebut secara teoritis lebih kuat dan lebih sulit untuk ditebak oleh penyerang, bahkan dengan serangan brute-force (mencoba semua kemungkinan kunci). Entropi yang rendah menunjukkan kunci yang memiliki pola, dapat diprediksi, atau berasal dari sumber keacakan yang buruk, yang secara signifikan akan melemahkan keamanan sistem enkripsi. Dengan demikian, entropi tinggi sangat penting untuk memastikan kunci kriptografi aman dan efektif.
- Pertanyaan 2: Mengapa unicity distance penting dalam menentukan keamanan suatu cipher?
Jarak Unicity ($U$) adalah metrik kritis karena menentukan panjang minimum teks tersandi (ciphertext) yang diperlukan agar hanya ada satu kunci yang masuk akal yang dapat mendekripsinya. Dalam kriptanalisis, ciphertext yang lebih pendek dari $U$ secara teoretis dapat didekripsi menggunakan banyak kunci berbeda, yang masing-masing menghasilkan teks asli (plaintext) yang valid—ini membuat penyerang tidak mungkin memilih kunci yang benar. Sebaliknya, begitu panjang ciphertext melebihi $U$, jumlah kunci palsu (spurious keys) yang tersisa akan berkurang menjadi nol. Metrik ini memberikan estimasi jumlah data yang diperlukan musuh dengan daya komputasi tak terbatas (computationally unlimited) untuk memecahkan sandi dengan kepastian, menjadikannya standar dasar untuk mengevaluasi seberapa tahan suatu sandi terhadap serangan teoretis, terutama yang melibatkan analisis statistik redundansi bahasa.
- Pertanyaan 3: Mengapa brute force masih menjadi ancaman meskipun algoritma sudah kuat?
Serangan brute force efektif karena ia tidak menargetkan kelemahan matematika pada algoritma itu sendiri, melainkan ruang kunci dan kecepatan komputasi:
1. Panjang dan Kualitas Kunci yang Lemah (Human Error): Algoritma yang kuat seperti AES dirancang untuk tahan terhadap brute force jika menggunakan kunci yang panjang dan acak dengan entropi tinggi (misalnya, kunci 256-bit). Namun, jika kunci yang digunakan—terutama kata sandi pengguna—terlalu pendek, mudah ditebak, atau memiliki pola (low entropy), penyerang tidak perlu mencoba triliunan kemungkinan yang ditetapkan oleh panjang kunci maksimal, melainkan hanya subset kecil. Ini secara drastis mengurangi waktu serangan dari jutaan tahun menjadi hitungan menit atau jam.
2. Peningkatan Daya Komputasi: Kekuatan komputasi, khususnya melalui penggunaan GPU (Graphics Processing Unit) yang sangat paralel dan komputasi cloud yang terdistribusi, memungkinkan penyerang untuk mencoba kombinasi kunci dalam jumlah yang jauh lebih besar per detik dibandingkan beberapa tahun lalu. Peningkatan kecepatan ini secara efektif "mempercepat" serangan brute force sehingga algoritma yang dulunya dianggap aman kini menghadapi risiko yang lebih besar jika panjang kuncinya tidak memadai atau sistem tidak memiliki mekanisme pembatasan percobaan (rate limiting).
Singkatnya, brute force mengeksploitasi kelemahan pada input kunci (kunci yang lemah) atau kemajuan teknologi (komputer yang lebih cepat), bukan kelemahan pada desain algoritma itu sendiri. 

---

## 8. Kesimpulan
Konsep Entropi-Unicity adalah landasan teoretis untuk menilai keamanan sandi (cipher) dengan mengintegrasikan dua faktor utama: kekuatan kunci dan jumlah data yang dibutuhkan untuk memecahkannya. Entropi mengukur keacakan dan kompleksitas dari ruang kunci yang tersedia; kunci dengan entropi tinggi (misalnya, 128 bit atau lebih) sangat penting untuk resistensi terhadap serangan brute-force. Sementara itu, Jarak Unicity ($U$) menentukan panjang minimum teks tersandi (ciphertext) yang harus dianalisis oleh penyerang, dengan asumsi daya komputasi tak terbatas dan pengetahuan tentang statistik bahasa (redundansi), untuk memulihkan kunci yang unik dan benar. Secara kolektif, teori Entropi-Unicity mengajarkan bahwa sistem kriptografi yang aman harus memiliki entropi kunci yang sangat tinggi untuk membuat serangan brute-force tidak praktis, sekaligus memastikan Jarak Unicitynya tinggi atau ciphertext yang dienkripsi jauh lebih pendek daripada $U$ untuk mencegah analisis statistik yang sukses.

---

## 9. Daftar Pustaka
https://journal.arteii.or.id/index.php/Merkurius/article/view/949

---
## 10. Commit Log
Author: Khoirun Nisa Az-Zahra <jahraaaaaa.13@gmail.com>
Date:   2025-11-03

    week4-entrophy-unicity: entrophy-unicity distance
```

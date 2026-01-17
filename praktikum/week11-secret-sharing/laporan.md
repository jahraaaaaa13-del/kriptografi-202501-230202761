# Laporan Praktikum Kriptografi
Minggu ke-: 11  
Topik: Shamir Secret Sharing (SSS)  
Nama: Khoierun Nisa Az-Zahra  
NIM: 230202761  
Kelas: 5IKRB  

---

## 1. Tujuan
1. Menjelaskan konsep Shamir Secret Sharing (SSS).
2. Melakukan simulasi pembagian rahasia ke beberapa pihak menggunakan skema SSS.
3. Menganalisis keamanan skema distribusi rahasia.

---

## 2. Dasar Teori
Shamir’s Secret Sharing merupakan sebuah algoritma kriptografi yang diperkenalkan oleh Adi Shamir pada tahun 1979 dengan prinsip dasar pembagian rahasia (secret sharing). Algoritma ini dirancang untuk mengamankan data sensitif dengan cara memecah rahasia tersebut menjadi n bagian yang disebut sebagai shares. Keunikan dari skema ini terletak pada mekanisme ambang batasnya (threshold scheme), yang dinyatakan dalam notasi (k, n). Dalam sistem ini, sebuah rahasia hanya dapat dipulihkan atau direkonstruksi jika terdapat setidaknya k jumlah partisipan yang menggabungkan share mereka. Sebaliknya, jika jumlah share yang terkumpul kurang dari nilai k, maka secara matematis mustahil bagi siapa pun untuk mendapatkan informasi sekecil apa pun mengenai rahasia asli tersebut, sehingga memberikan tingkat keamanan yang sangat tinggi atau disebut sebagai perfect secrecy.

Secara matematis, Shamir’s Secret Sharing dibangun di atas konsep polinomial dalam aljabar. Untuk menyembunyikan sebuah rahasia S, algoritma ini membuat sebuah polinomial acak berderajat k-1, di mana nilai rahasia S diletakkan sebagai konstanta atau titik potong pada sumbu y (f(0) = S). Koefisien lainnya dipilih secara acak untuk membentuk kurva polinomial tersebut. Setiap partisipan kemudian diberikan sebuah titik koordinat (x, y) yang berada tepat di sepanjang garis kurva tersebut. Dasar pemikirannya mengikuti prinsip geometri bahwa diperlukan k titik spesifik untuk mengidentifikasi secara unik sebuah polinomial berderajat k-1. Misalnya, dibutuhkan dua titik untuk menentukan sebuah garis lurus (k=2) dan tiga titik untuk menentukan sebuah parabola (k=3).

Proses pemulihan rahasia dilakukan melalui metode yang disebut Interpolasi Lagrange. Ketika k orang partisipan berkumpul dan memberikan titik-titik koordinat yang mereka miliki, rumus interpolasi ini digunakan untuk menghitung kembali koefisien polinomial asli. Setelah polinomial tersebut berhasil dibentuk ulang, nilai rahasia asli dapat ditemukan dengan menghitung nilai fungsi pada titik nol. Keunggulan utama dari teori ini adalah fleksibilitasnya; pemilik rahasia dapat membagikan akses kepada banyak pihak tanpa perlu khawatir akan kebocoran tunggal, karena keamanan sistem ini tidak bergantung pada kerahasiaan satu individu, melainkan pada konsensus kelompok sesuai ambang batas yang telah ditentukan.

---

## 3. Alat dan Bahan
- Python 3.x
- Visual Studio Code
- Git dan akun GitHub

---

## 4. Langkah Percobaan
1. Menginstal library secretsharing menggunakan pip install secretsharing.
2. Mengimplementasikan Shamir Secret Sharing dengan Python.
3. Melakukan simulasi manual menggunakan polinomial modulo bilangan prima.
4. Menganalisis keamanan skema Shamir Secret Sharing.
5. Menjawab pertanyaan diskusi.
6. Menyelesaikan penulisan laporan laporan.md.

---

## 5. Source Code
<img width="649" height="633" alt="Screenshot source code week11" src="https://github.com/user-attachments/assets/4e346bdb-4edb-491d-9dba-5cba0e3e6e52" />


---

## 6. Hasil dan Pembahasan
<img width="992" height="191" alt="Screenshot hasil week11" src="https://github.com/user-attachments/assets/4a9aee7b-1da0-446a-b970-13306ce5179d" />
Berdasarkan hasil eksekusi program tersebut, dapat disimpulkan bahwa sistem telah berhasil mengimplementasikan skema Shamir’s Secret Sharing dengan metode ambang batas (k, n). Dalam output tersebut, program menghasilkan n=5 buah shares yang direpresentasikan sebagai koordinat titik (x, y), yaitu (1, 398), (2, 1210), (3, 1581), (4, 1511), dan (5, 1000). Secara individual, setiap titik koordinat ini tidak memberikan petunjuk apapun mengenai informasi rahasia yang disembunyikan, sehingga keamanan data tetap terjaga meskipun salah satu share jatuh ke tangan pihak yang tidak berwenang.

Proses pemulihan rahasia pada baris terakhir menunjukkan bahwa program menggunakan algoritma Interpolasi Lagrange untuk menarik kembali kurva polinomial dari titik-titik yang tersedia. Melalui perhitungan matematis tersebut, program mencari nilai fungsi pada saat x=0 (titik potong sumbu y), yang kemudian menghasilkan angka 1234 sebagai rahasia yang berhasil dipulihkan (Recovered secret). Keberhasilan ini membuktikan bahwa meskipun rahasia telah dipecah menjadi bagian-bagian yang tampak acak, koordinasi antar share sesuai ambang batas minimal yang ditentukan tetap mampu mengonstruksi ulang informasi asli secara akurat dan presisi.

---

## 7. Jawaban Pertanyaan
- Pertanyaan 1: Apa keuntungan utama Shamir Secret Sharing dibanding membagikan salinan kunci secara langsung?
  
Keuntungan utama Shamir’s Secret Sharing (SSS) dibandingkan pembagian salinan kunci langsung terletak pada keseimbangan antara keamanan tinggi dan fleksibilitas akses. Dalam pembagian salinan langsung, jika satu salinan jatuh ke tangan pihak yang salah, rahasia tersebut langsung terbongkar sepenuhnya. Sebaliknya, SSS menggunakan skema ambang batas (threshold) yang memastikan bahwa satu atau beberapa bagian (shares) yang bocor tidak akan memberikan informasi sedikit pun mengenai rahasia asli selama jumlahnya belum mencapai batas minimum ($k$) yang ditentukan. Selain itu, SSS mencegah risiko kehilangan akses; jika satu pemegang kunci kehilangan bagiannya, rahasia tetap dapat dipulihkan selama partisipan lain yang tersisa masih memenuhi kuorum, sehingga meminimalisir adanya single point of failure. 

- Pertanyaan 2: Apa peran threshold (k) dalam keamanan secret sharing?
  
Peran threshold (k) sangat krusial sebagai penentu batas minimum kepercayaan dalam sistem keamanan. Nilai k berfungsi sebagai filter yang memastikan bahwa rahasia tidak dapat diakses oleh individu secara sepihak, melainkan harus melalui konsensus atau kolaborasi kelompok. Dari sisi keamanan, k memberikan perlindungan terhadap ancaman internal maupun eksternal; jika penyerang berhasil mencuri sejumlah share namun jumlahnya masih di bawah nilai $k$ (maksimal k-1), maka secara matematis penyerang tersebut tetap memiliki probabilitas nol untuk menebak rahasia asli. Di sisi lain, dari sisi ketersediaan (availability), k memungkinkan pemulihan data tetap berjalan meskipun ada beberapa partisipan yang kehilangan bagiannya atau tidak tersedia, selama kuorum minimum tetap terpenuhi.

- Pertanyaan 3: Berikan satu contoh skenario nyata di mana SSS sangat bermanfaat.
  
Salah satu skenario nyata di mana Shamir’s Secret Sharing (SSS) sangat bermanfaat adalah dalam manajemen kunci utama (Master Key) pada infrastruktur perbankan atau perusahaan teknologi besar. Dalam skenario ini, kunci enkripsi tingkat tinggi yang melindungi seluruh data sensitif tidak boleh dipegang oleh satu individu saja untuk menghindari penyalahgunaan kekuasaan atau risiko kehilangan akses jika orang tersebut berhalangan. Dengan SSS, kunci tersebut dipecah menjadi beberapa bagian yang dibagikan kepada jajaran direksi atau manajer keamanan yang berbeda; misalnya, diperlukan minimal 3 dari 5 pejabat untuk hadir dan menggabungkan share mereka agar sistem utama dapat dibuka atau diperbarui. Hal ini memastikan keamanan berlapis karena pencurian satu bagian kunci tidak akan membocorkan rahasia, sekaligus memberikan redundansi jika salah satu pemegang kunci kehilangan aksesnya. 

---

## 8. Kesimpulan
Metode ini merupakan solusi kriptografi yang sangat efektif untuk mengelola rahasia secara kolektif melalui skema ambang batas (k, n). Dengan memanfaatkan prinsip polinomial dan Interpolasi Lagrange, SSS mampu memecah informasi sensitif menjadi bagian-bagian yang tidak berarti secara individual, namun sangat akurat ketika digabungkan kembali sesuai kuorum yang ditetapkan.

Penerapan SSS memberikan dua manfaat fundamental yang tidak dimiliki oleh metode penyalinan kunci konvensional: keamanan sempurna (perfect secrecy) dan ketahanan sistem (fault tolerance). Keamanan terjamin karena informasi rahasia tetap terlindungi meskipun sejumlah k-1 bagian bocor, sementara ketahanan sistem memastikan rahasia tetap dapat diakses walaupun sebagian pemegang share kehilangan datanya. Hal ini menjadikan SSS sebagai fondasi penting dalam perlindungan aset digital modern, mulai dari infrastruktur perbankan hingga pengelolaan kunci dompet mata uang kripto.
---

## 9. Daftar Pustaka 
- Alvira Firjan Humaira, Rini Marwati, Kartika Yulianti. *IImplementasi Kriptografi Secret Sharing Scheme dan Steganografi Audio Least Significant Bit (LSB)*.  
- Fitrah Ramadhani Nugroho. *Implementasi RSA dan Shamir's Secret Sharing pada Web Group Chat System untuk Mengirim Pesan dan File Rahasia*.  

---

## 10. Commit Log
commit abc12345
Author: Khoirun Nisa Az-Zahra <jahraaaaaa.13@gmail.com>
Date:   2026-01-17

```

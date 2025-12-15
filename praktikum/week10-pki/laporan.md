# Laporan Praktikum Kriptografi
Minggu ke-: 10  
Topik: Public Key Infrastructure (PKI & Certificate Authority)  
Nama: Khoirun Nisa Az-Zahra  
NIM: 230202761  
Kelas: 5IKRB  

---

## 1. Tujuan
1. Membuat sertifikat digital sederhana.
2. Menjelaskan peran Certificate Authority (CA) dalam sistem PKI.
3. Mengevaluasi fungsi PKI dalam komunikasi aman (contoh: HTTPS, TLS).

---

## 2. Dasar Teori
Public Key Infrastructure (PKI) adalah kerangka kerja komprehensif yang terdiri dari perangkat keras, perangkat lunak, kebijakan, dan prosedur yang diperlukan untuk mengelola, mendistribusikan, menggunakan, menyimpan, dan mencabut Sertifikat Digital dan mengelola enkripsi kunci publik. PKI adalah fondasi utama bagi keamanan sistem modern, seperti HTTPS, VPN, dan Tanda Tangan Digital. Inti dari PKI adalah untuk memecahkan masalah kepercayaan dalam kriptografi asimetris, yaitu bagaimana memastikan bahwa Kunci Publik yang diterima benar-benar milik entitas yang diklaim. Peran sentral dalam PKI dipegang oleh Certificate Authority (CA), yang bertindak sebagai pihak ketiga yang netral dan terpercaya. CA bertanggung jawab untuk memverifikasi identitas pemohon kunci dan kemudian menerbitkan Sertifikat Digital (X.509) yang secara kriptografis mengikat Kunci Publik tersebut dengan identitas yang sudah diverifikasi, lalu menandatanganinya menggunakan Kunci Privat milik CA. Ini memungkinkan pengguna untuk saling percaya karena verifikasi identitas dilakukan oleh otoritas yang diakui dan dipercaya oleh semua pihak dalam jaringan.

---

## 3. Alat dan Bahan
- Python 3.x  
- Visual Studio Code / editor lain  
- Git dan akun GitHub  
- Library tambahan (cryptography pyopenssl)

---

## 4. Langkah Percobaan
1. Membuat file pki.py di folder praktikum/week10-pki/src/.
2. Menyalin kode program dari panduan praktikum.
3. Menjalankan program dengan perintah python pki.py.

---

## 5. Source Code
from cryptography import x509
from cryptography.x509.oid import NameOID
from cryptography.hazmat.primitives import hashes, serialization
from cryptography.hazmat.primitives.asymmetric import rsa
from datetime import datetime, timedelta

#Generate key pair
key = rsa.generate_private_key(public_exponent=65537, key_size=2048)

#Buat subject & issuer (CA sederhana = self-signed)
subject = issuer = x509.Name([
    x509.NameAttribute(NameOID.COUNTRY_NAME, u"ID"),
    x509.NameAttribute(NameOID.ORGANIZATION_NAME, u"UPB Kriptografi"),
    x509.NameAttribute(NameOID.COMMON_NAME, u"example.com"),
])

#Buat sertifikat
cert = (
    x509.CertificateBuilder()
    .subject_name(subject)
    .issuer_name(issuer)
    .public_key(key.public_key())
    .serial_number(x509.random_serial_number())
    .not_valid_before(datetime.utcnow())
    .not_valid_after(datetime.utcnow() + timedelta(days=365))
    .sign(key, hashes.SHA256())
)

#Simpan sertifikat
with open("cert.pem", "wb") as f:
    f.write(cert.public_bytes(serialization.Encoding.PEM))

print("Sertifikat digital berhasil dibuat: cert.pem")

---

## 6. Hasil dan Pembahasan
![Screenshot source code week10_1](https://github.com/user-attachments/assets/8d60b3c1-4626-43a2-8c0d-a02f5125eac9)

![Screenshot source code week10_2](https://github.com/user-attachments/assets/47e883d1-bd64-4417-9ebb-f88023037aac)

# Langkah 2—Memverifikasi Sertifikat
A. Gunakan public key untuk memverifikasi tanda tangan sertifikat.
Dalam sistem Public Key Infrastructure (PKI), public key memiliki peran sentral dalam memverifikasi keaslian dan integritas Sertifikat Digital. Ketika sebuah entitas (misalnya, browser Anda) menerima Sertifikat Digital, entitas tersebut perlu memastikan bahwa sertifikat tersebut benar-benar dikeluarkan oleh Certificate Authority (CA) yang terpercaya dan belum dimodifikasi. Sertifikat Digital selalu ditandatangani secara kriptografis menggunakan Kunci Privat milik CA. Untuk memverifikasi tanda tangan ini, penerima harus menggunakan Kunci Publik yang sesuai milik CA yang sama. Proses verifikasi melibatkan dekripsi tanda tangan pada sertifikat menggunakan Kunci Publik CA tersebut, yang akan menghasilkan nilai hash asli. Nilai hash ini kemudian dibandingkan dengan nilai hash yang dihitung secara lokal dari isi sertifikat yang diterima. Jika kedua nilai hash cocok, itu membuktikan dua hal: bahwa sertifikat tidak diubah (integritas), dan bahwa sertifikat tersebut benar-benar ditandatangani oleh pemilik Kunci Privat yang sah (yaitu, CA yang dipercaya), sehingga menjamin otentikasi sertifikat tersebut.

B. Jelaskan bagaimana CA digunakan untuk menjamin keaslian sertifikat.
Certificate Authority (CA) adalah entitas tepercaya yang berfungsi sebagai jangkar kepercayaan dalam ekosistem Public Key Infrastructure (PKI) dan digunakan untuk menjamin keaslian sebuah sertifikat digital. Proses penjaminan keaslian dimulai ketika CA melakukan verifikasi identitas yang ketat terhadap pemohon sertifikat (misalnya, sebuah situs web atau individu). Setelah identitas terverifikasi, CA menerbitkan Sertifikat Digital (X.509) yang berisi Kunci Publik pemohon dan informasi identitasnya, kemudian CA menggunakan Kunci Privatnya sendiri untuk membuat tanda tangan digital pada seluruh isi sertifikat tersebut. Tanda tangan CA ini adalah garansi kriptografis bahwa sertifikat tersebut otentik dan isinya belum diubah sejak diterbitkan. Karena Kunci Publik CA sudah ditanamkan dan dipercaya secara default di semua sistem operasi dan browser (dikenal sebagai root certificates), penerima sertifikat dapat memverifikasi tanda tangan CA tersebut, yang secara efektif membuktikan keaslian sertifikat dan identitas pemiliknya.

# Langkah 3—Analisis PKI
A. Bagaimana browser memverifikasi sertifikat HTTPS?
Ketika browser terhubung ke server yang menggunakan HTTPS, serangkaian langkah verifikasi sertifikat dilakukan untuk membangun koneksi yang aman (TLS/SSL). Pertama, server mengirimkan Sertifikat Digital kepada browser. Browser kemudian memeriksa beberapa hal: validitas waktu (apakah sertifikat kedaluwarsa atau belum berlaku), domain (apakah sertifikat dikeluarkan untuk nama domain yang sedang diakses), dan status pencabutan (apakah sertifikat telah dibatalkan oleh CA). Langkah terpenting adalah verifikasi rantai kepercayaan: browser menggunakan Kunci Publik dari Certificate Authority (CA) yang mengeluarkan sertifikat tersebut (atau rantai CA yang lebih tinggi) untuk memverifikasi tanda tangan digital pada sertifikat server. Browser memiliki daftar Kunci Publik CA tepercaya yang sudah tertanam (root store). Jika tanda tangan berhasil diverifikasi menggunakan root key yang dipercaya, ini menjamin bahwa sertifikat tersebut asli, belum diubah, dan dikeluarkan oleh otoritas yang sah, sehingga browser dapat melanjutkan proses handshake TLS dan mengenkripsi komunikasi.

B. Apa yang terjadi jika CA palsu menerbitkan sertifikat?
Sertifikat dari CA palsu langsung ditolak browser karena tidak ada dalam daftar CA tepercaya. Namun jika CA resmi diretas dan menerbitkan sertifikat ilegal, penyerang bisa menyamar sebagai situs asli dan melakukan serangan MITM—karena itu browser akan segera mencabut kepercayaan terhadap CA yang bermasalah.

C. Mengapa PKI penting dalam komunikasi aman (misalnya transaksi online)?
Public Key Infrastructure (PKI) sangat penting dalam mengamankan komunikasi dan transaksi online karena ia menyediakan kerangka kerja untuk kepercayaan (trust) dan kerahasiaan (confidentiality).

---

## 7. Jawaban Pertanyaan  
- Pertanyaan 1: Fungsi utama Certificate Authority (CA) adalah bertindak sebagai pihak ketiga tepercaya dan akar kepercayaan dalam sistem Public Key Infrastructure (PKI). Peran intinya adalah memverifikasi identitas suatu entitas (seperti individu, organisasi, atau server web) dan kemudian secara kriptografis mengikat Kunci Publik entitas tersebut dengan identitas yang telah diverifikasi. Setelah verifikasi identitas berhasil, CA menandatangani sertifikat tersebut menggunakan Kunci Privatnya sendiri, yang berfungsi sebagai garansi digital. Tanda tangan ini memastikan bahwa Kunci Publik dalam sertifikat adalah asli dan memang milik entitas yang diklaim, sehingga memungkinkan browser dan sistem lain untuk memverifikasi keaslian, integritas, dan otentikasi komunikasi yang aman (seperti HTTPS). Selain itu, CA juga bertanggung jawab untuk mengelola siklus hidup sertifikat, termasuk pencabutan jika keamanan sertifikat tersebut terkompromi.
- Pertanyaan 2: Sertifikat self-signed tidak memadai untuk sistem produksi karena gagal membangun rantai kepercayaan yang diperlukan dalam lingkungan Public Key Infrastructure (PKI) global. Ketika server menggunakan sertifikat self-signed, sertifikat tersebut ditandatangani oleh kunci privat server itu sendiri, bukan oleh Certificate Authority (CA) pihak ketiga yang tepercaya dan dikenal secara global. Akibatnya, ketika browser pengguna menerima sertifikat tersebut, browser tidak dapat memverifikasi tanda tangan menggunakan Kunci Publik CA mana pun yang ada di root store tepercayanya.
- Pertanyaan 3: PKI mencegah serangan Man-in-the-Middle (MITM) selama handshake TLS/HTTPS melalui proses otentikasi sertifikat yang ketat. Dalam serangan MITM, penyerang mencoba menyamar sebagai server yang sah. Namun, sebelum koneksi dienkripsi, server yang sah akan menyajikan Sertifikat Digital yang dikeluarkan dan ditandatangani oleh Certificate Authority (CA) yang dipercaya. Browser penerima menggunakan Kunci Publik CA yang sudah tertanam untuk memverifikasi tanda tangan pada sertifikat server. Jika penyerang menyajikan sertifikat palsu, browser tidak akan dapat memverifikasi tanda tangan tersebut menggunakan Kunci Publik CA yang diakui. Kegagalan verifikasi ini segera memutus rantai kepercayaan, menyebabkan browser menampilkan peringatan keamanan dan menolak melanjutkan komunikasi. Dengan demikian, PKI memastikan bahwa koneksi hanya terjalin dengan server yang identitasnya telah terverifikasi secara kriptografis dan sah.

---

## 8. Kesimpulan
Public Key Infrastructure (PKI) adalah kerangka kerja keamanan fundamental yang mengatasi masalah utama kriptografi kunci asimetris, yaitu kepercayaan pada Kunci Publik. PKI menyediakan sistem yang terstruktur (termasuk kebijakan, prosedur, dan perangkat lunak) untuk manajemen Kunci Publik. Fungsi sentral dipegang oleh Certificate Authority (CA), yang bertindak sebagai pihak ketiga yang netral dan dipercaya. CA bertanggung jawab untuk memverifikasi identitas pemohon dan kemudian menerbitkan Sertifikat Digital (X.509) yang mengikat Kunci Publik secara kriptografis dengan identitas yang sah melalui tanda tangan digital CA sendiri. Kesimpulannya, PKI adalah landasan bagi semua komunikasi aman modern (seperti HTTPS dan tanda tangan digital) karena PKI menjamin otentikasi dan integritas Kunci Publik, yang pada gilirannya memungkinkan pembentukan sesi komunikasi yang rahasia (terenkripsi) dan terlindungi dari serangan Man-in-the-Middle.

---

## 9. Daftar Pustaka
- Syahreza Mitzardie Yacub, Rikaro Ramadi, Dani Ernawati. *Public Key Infrastructure : Kerangka Validasi Yang Disempurnakan*.  
- Edmon Makarim. *Penyelenggaraan Community Certification Authority Untuk Pengamanan Sumber Daya Internet Oleh Komunitas Untuk Kesiapan Asean Regional E-Commerce*.

---

## 10. Commit Log
commit abc12345
Author: Khoirun Nisa Az-Zahra <jahraaaaaa.13@gmail.com>
Date:   2025-12-16

```

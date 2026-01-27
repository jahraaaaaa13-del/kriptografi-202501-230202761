# Laporan Praktikum Kriptografi
Minggu ke-: 15  
Topik: TinycCoin ERC20  
Nama: Khoirun Nisa Az-Zahra  
NIM: 230202761  
Kelas: 5IKRB  

---

## 1. Tujuan
1. Mengembangkan proyek sederhana berbasis algoritma kriptografi.
2. Mendokumentasikan proses implementasi proyek ke dalam repository Git.
3. Menyusun laporan teknis hasil proyek akhir.
---

## 2. Dasar Teori
TinyCoin ERC-20 merupakan token kripto yang dibangun di atas blockchain Ethereum dengan mengikuti standar ERC-20, yaitu seperangkat aturan teknis yang memastikan token dapat berinteraksi secara seragam dengan wallet, smart contract, dan aplikasi terdesentralisasi (dApp). Standar ini mendefinisikan fungsi dasar seperti transfer token, pengecekan saldo, dan persetujuan transaksi, sehingga memudahkan integrasi dalam ekosistem Ethereum. TinyCoin sendiri biasanya digunakan sebagai contoh atau proyek sederhana untuk mempelajari pembuatan token, penerapan smart contract berbasis Solidity, serta konsep dasar kriptografi dan desentralisasi, yang menekankan transparansi, keamanan, dan otomatisasi transaksi tanpa perantara.

---

## 3. Alat dan Bahan
(- Python 3.x  
- Visual Studio Code / editor lain  
- Git dan akun GitHub  
- Library tambahan (misalnya pycryptodome, jika diperlukan)  )

---

## 4. Langkah Percobaan
(Tuliskan langkah yang dilakukan sesuai instruksi.  
Contoh format:
1. Membuat file `caesar_cipher.py` di folder `praktikum/week2-cryptosystem/src/`.
2. Menyalin kode program dari panduan praktikum.
3. Menjalankan program dengan perintah `python caesar_cipher.py`.)

---

## 5. Source Code
(Salin kode program utama yang dibuat atau dimodifikasi.  
Gunakan blok kode:

```python
# contoh potongan kode
def encrypt(text, key):
    return ...
```
)

---

## 6. Hasil dan Pembahasan
(- Lampirkan screenshot hasil eksekusi program (taruh di folder `screenshots/`).  
- Berikan tabel atau ringkasan hasil uji jika diperlukan.  
- Jelaskan apakah hasil sesuai ekspektasi.  
- Bahas error (jika ada) dan solusinya. 

Hasil eksekusi program Caesar Cipher:

![Hasil Eksekusi](screenshots/output.png)
![Hasil Input](screenshots/input.png)
![Hasil Output](screenshots/output.png)
)

---

## 7. Jawaban Pertanyaan  
- Pertanyaan 1: Apa fungsi utama ERC20 dalam ekosistem blockchain?
Fungsi utama ERC-20 dalam ekosistem blockchain adalah sebagai standar teknis untuk pembuatan dan pengelolaan token di jaringan Ethereum, sehingga semua token yang mengikuti ERC-20 memiliki cara kerja yang seragam. Dengan adanya standar ini, token dapat dengan mudah ditransfer, disimpan di wallet, diperdagangkan di exchange, serta terintegrasi dengan smart contract dan aplikasi terdesentralisasi (dApp) tanpa perlu penyesuaian khusus. ERC-20 juga memastikan interoperabilitas antar layanan, meningkatkan efisiensi pengembangan, serta mempercepat adopsi token dalam berbagai use case seperti pembayaran digital, crowdfunding, DeFi, dan sistem reward.
  
- Pertanyaan 2: Bagaimana mekanisme transfer token bekerja dalam kontrak ERC20.
Mekanisme transfer token pada kontrak ERC-20 bekerja melalui fungsi standar transfer() dan transferFrom() yang mengatur perpindahan saldo antar alamat secara otomatis oleh smart contract. Saat transfer() dipanggil, kontrak akan mengecek apakah pengirim memiliki saldo cukup, lalu mengurangi saldo pengirim dan menambah saldo penerima di dalam mapping balances, kemudian memancarkan event Transfer sebagai bukti transaksi di blockchain.

Sementara itu, transferFrom() digunakan ketika pihak ketiga melakukan transfer atas nama pemilik token, yang sebelumnya harus diberi izin lewat fungsi approve(). Izin ini disimpan dalam mapping allowance, sehingga kontrak memastikan jumlah yang ditransfer tidak melebihi batas yang disetujui. Dengan mekanisme ini, ERC-20 memungkinkan transfer langsung maupun berbasis izin secara aman, transparan, dan terdesentralisasi.

- Pertanyaan 3: Apa risiko utama dalam implementasi smart contract dan bagaimana cara mitigasinya?
Risiko utama dalam implementasi smart contract meliputi kesalahan logika kode (bug), kerentanan keamanan seperti reentrancy attack, integer overflow/underflow, serta pengelolaan hak akses yang tidak tepat. Selain itu, karena smart contract bersifat immutable (tidak dapat diubah setelah dideploy), kesalahan kecil dapat berdampak besar, termasuk kehilangan aset. Risiko lain adalah ketergantungan pada external contract/oracle dan kurangnya validasi input.

Cara mitigasinya antara lain dengan menerapkan secure coding practices, melakukan pengujian menyeluruh (unit test & integration test), menggunakan library standar terpercaya seperti OpenZeppelin, menerapkan audit kode (internal maupun pihak ketiga), serta menambahkan mekanisme upgrade contract atau proxy pattern bila diperlukan. Penggunaan access control, fail-safe mechanism, dan code review berlapis juga sangat dianjurkan untuk meminimalkan potensi eksploitasi.  

---

## 8. Kesimpulan
standar ERC-20 berperan penting dalam ekosistem blockchain Ethereum karena menyediakan aturan baku dalam pembuatan dan pengelolaan token, sehingga memudahkan integrasi dengan wallet, exchange, dan aplikasi terdesentralisasi. Implementasi token seperti TinyCoin membantu memahami konsep dasar smart contract, mekanisme transfer, serta sistem izin transaksi. Namun, pengembangan smart contract memiliki risiko seperti kesalahan logika dan celah keamanan, sehingga diperlukan praktik pengembangan yang aman melalui pengujian, audit, serta penggunaan library terpercaya. Dengan penerapan yang tepat, teknologi ini mampu menghadirkan sistem transaksi yang transparan, aman, dan terdesentralisasi.

---

## 9. Commit Log
commit abc12345
Author: Khoirun Nisa Az-Zahra <jahraaaaaa.13@gmail.com>
Date:   2026-01-27

  week15-tinycoin-erc20

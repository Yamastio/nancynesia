---
title: Memahami Command Injection
prev: /docs/hacking/hacking_fundamentals/
---

## Apa itu Command Injection?

**Command Injection** adalah kerentanan keamanan yang terjadi ketika suatu aplikasi menerima input dari pengguna dan mengeksekusi perintah sistem operasi tanpa melakukan validasi atau sanitasi yang memadai. Kerentanan ini memungkinkan penyerang untuk menyisipkan dan menjalankan perintah yang tidak diotorisasi pada server.

Command Injection berbeda dengan **Insecure File Upload** atau **Unrestricted File Upload**:

- **Insecure File Upload:** Penyerang mengunggah file berbahaya yang kemudian dijalankan oleh server.
- **Command Injection:** Penyerang langsung menjalankan perintah sistem operasi melalui input yang disediakan aplikasi.

### Contoh Situasi:

Misalnya, pada sistem berbasis Debian, penyerang dapat menjalankan perintah-perintah seperti `ls`, `cat`, atau `id` melalui kerentanan ini. Jika aplikasi tidak membatasi atau memvalidasi input, perintah-perintah ini dapat dijalankan oleh server.

## Demo di DVWA (Damn Vulnerable Web Application)

### Langkah-langkah:

1. **Pastikan DVWA Security Level dalam keadaan "Low":**
   ![Set Security Low](/images/SetSecLow.png)

   - Hal ini memastikan bahwa tidak ada mekanisme mitigasi yang diterapkan, sehingga kita bisa memahami cara kerentanan ini bekerja.

2. **Buka Menu `Command Injection`:**

   - Navigasikan ke menu "Command Injection" di DVWA.

3. **Uji Fitur dengan Input Standar:**

   - Pada form "Ping a Device," masukkan perintah sederhana seperti:

     ```bash
     google.com
     ```

   - Hasilnya akan menampilkan output seperti menjalankan perintah `ping` di shell Bash.

     ![Ping google.com](/images/pingGoogle.png)

4. **Analisis Kode Sumber:**

   - Jika Anda memeriksa kode sumber aplikasi, Anda akan menemukan logika seperti ini:

     - Untuk server Windows NT, menggunakan perintah `ping`.
     - Untuk server UNIX, menggunakan perintah `ping -c 4`.

       ![SourceCI](/images/SourceCommandInjection.png)

5. **Eksploitasi Kerentanan:**

   - Dengan memanfaatkan fakta bahwa sistem ini tidak memvalidasi input, kita dapat menjalankan beberapa perintah sekaligus menggunakan operator seperti:
     - `&&`: Menjalankan perintah berikutnya jika perintah sebelumnya berhasil.
     - `||`: Menjalankan perintah berikutnya jika perintah sebelumnya gagal.
     - `;`: Menjalankan perintah secara berurutan tanpa peduli hasil perintah sebelumnya.

6. **Contoh Input Berbahaya:**

   - Masukkan salah satu perintah berikut untuk menguji kerentanan:

     ```bash
     google.com && id
     ```

     ![Cek ID](/images/CekID.png)
     Hasil: Menampilkan informasi user ID server, seperti `www-data`.

     ```bash
     google.com || id
     ```

     Hasil: Menjalankan perintah `id` jika `ping google.com` gagal.

     ```bash
     google.com; id
     ```

     Hasil: Menjalankan `ping` diikuti dengan `id` terlepas dari keberhasilan perintah pertama.

     ```bash
     google.com; ls
     ```

     ![Cek Dir](/images/CekDir.png)

     Hasil: Menampilkan daftar file di direktori kerja server.

     ```bash
     google.com; cat index.php
     ```

     ![Cat index](/images/CatFile.png)
     Hasil: Membaca isi file `index.php` jika memiliki izin akses.

7. **Dampak:**
   - Dengan mengeksploitasi kerentanan ini, penyerang dapat:
     - Mengakses file sensitif.
     - Mengeksekusi perintah berbahaya.
     - Mengambil alih kontrol penuh server.

## Teknik dan Operator dalam Command Injection

### Operator Umum:

- `&&`: Menjalankan perintah berikutnya jika perintah sebelumnya berhasil.
- `||`: Menjalankan perintah berikutnya jika perintah sebelumnya gagal.
- `;`: Menjalankan perintah secara berurutan tanpa memperhatikan hasil.
- `|`: Mengalihkan output dari perintah pertama sebagai input untuk perintah kedua (pipe).
- `` ` ``: Menjalankan perintah di dalam backticks.
- `$()`: Substitusi perintah, menjalankan perintah di dalam kurung.

## Langkah Mitigasi

1. **Validasi dan Sanitasi Input:**

   - Gunakan whitelist untuk input yang diizinkan.
   - Escape karakter khusus seperti `;`, `|`, `&&`, dan `||`.

2. **Hindari Eksekusi Perintah Shell Secara Langsung:**

   - Gunakan fungsi API yang tidak mengeksekusi shell secara langsung, seperti `exec()` dengan parameter terpisah di Python.

3. **Batasi Hak Akses:**

   - Jalankan aplikasi dengan hak akses minimum (misalnya, pengguna non-root).

4. **Gunakan WAF (Web Application Firewall):**

   - Terapkan WAF untuk mendeteksi dan memblokir pola serangan yang mencurigakan.

5. **Audit dan Monitoring:**
   - Pantau log server untuk mendeteksi aktivitas tidak biasa.

Dengan memahami cara kerja Command Injection dan menerapkan langkah mitigasi yang tepat, Anda dapat melindungi aplikasi Anda dari serangan ini secara efektif.

---
title: Persiapan Pembuatan Report
prev: /docs/hacking/hacking_fundamentals/
---

## **Format Penulisan**

### **Halaman 1**

> **Visualisasi:**

![halaman1](/images/halaman1.png)

**Elemen Utama:**

1. **Logo Perusahaan**: Sertakan logo perusahaan atau organisasi yang menjadi target penilaian.
   _Tips: Pastikan logo terlihat jelas dan sesuai dengan gaya visual laporan._

2. **Judul**: Gunakan format spesifik yang menggambarkan kerentanan, seperti:

   - "Reflected XSS on Search Page"
   - "Broken Access Control in Admin Dashboard"

3. **Tanggal Ditemukan**: Cantumkan tanggal temuan kerentanan, seperti:

   - _on 28 July 2018_

4. **Penemu Bug**: Masukkan nama atau alias penemu bug, contohnya:
   - _by Overflow_

### **Halaman 2** (Disajikan dalam bentuk tabel)

> **Visualisasi:**

![halaman2](/images/halaman2.png)

#### **Struktur Tabel dan Keterangan**

1. **Description**

   - Berisi deskripsi rinci kerentanan. Anda bisa merujuk pada informasi yang tersedia di [OWASP Top 10](https://owasp.org/).
     **Contoh:**
     - _Kerentanan ini memungkinkan input user tidak divalidasi dengan benar, sehingga penyerang dapat menyisipkan skrip berbahaya._

2. **Affected Endpoint**

   - Endpoint yang terdampak. Cantumkan detail URL atau lokasi fungsi yang rentan.
     **Contoh:**
     - _/search?q=example_
     - _API: /api/user/login_

3. **Impact**

   - Penjelasan dampak kerentanan terhadap sistem atau data.
     **Contoh:**
     - _Penyerang dapat mencuri cookie sesi pengguna._
     - _Data pengguna terekspos dan dapat diakses oleh pihak tidak sah._

4. **Steps to Reproduce**

   - Langkah-langkah yang harus diikuti untuk mereproduksi kerentanan.
     **Format:**
     - Langkah 1: Masukkan skrip berikut ke kolom pencarian.
     - Langkah 2: Klik tombol "Search".
     - Langkah 3: Periksa hasil yang menunjukkan adanya skrip yang dieksekusi.

5. **Proof of Concept (POC)**

   - Dokumentasi atau bukti (gambar atau video) yang menunjukkan keberhasilan eksploitasi.
     **Tips:**
     - Gunakan tangkapan layar atau rekaman video untuk memperjelas POC.

6. **Remediation**

   - Saran mitigasi atau langkah-langkah perbaikan.
     **Contoh:**
     - _Gunakan prepared statements untuk query SQL._
     - _Validasi input dengan whitelist._

7. **References**
   - Sumber rujukan tambahan untuk informasi lebih lanjut.
     **Contoh:**
     - [OWASP Top 10: Injection](https://owasp.org/www-project-top-ten/)
     - [Mitigation Techniques](https://cheatsheetseries.owasp.org/)

---
title: OWASP TOP 10 2021
prev: /docs/hacking/hacking_fundamentals/
---

## Apa itu OWASP Top 10 Vulnerabilities

OWASP Top 10 adalah daftar kerentanan keamanan aplikasi web yang paling umum dan berisiko tinggi. Pemahaman dan mitigasi risiko ini sangat penting untuk meningkatkan keamanan aplikasi.

### **A01: Broken Access Control**

- **Definisi:** Kerentanan yang memungkinkan penyerang melakukan tindakan tanpa otorisasi yang sah.
- **Contoh Kasus:**
  - Terjadi di Facebook, di mana hacker dapat menjadi admin dari semua halaman Facebook melalui eksploitasi akses yang salah.
- **Dampak:** Hacker bisa mengakses atau mengubah data yang seharusnya terbatas untuk pengguna tertentu.
- **Pencegahan:**
  - Implementasikan kontrol akses berbasis peran (Role-Based Access Control - RBAC).
  - Uji kontrol akses menggunakan alat penetration testing.

### **A02: Cryptographic Failures**

- **Definisi:** Kerentanan yang timbul akibat kegagalan dalam melindungi data sensitif melalui enkripsi.
- **Dampak:** Data penting seperti password, nomor kartu kredit, atau informasi pribadi dapat terekspos.
- **Pencegahan:**
  - Gunakan algoritma enkripsi yang aman (seperti AES, RSA).
  - Hindari menggunakan protokol komunikasi tanpa enkripsi (seperti HTTP, gunakan HTTPS).

### **A03: Injection**

- **Definisi:** Serangan yang terjadi saat aplikasi tidak memvalidasi input dengan baik, memungkinkan penyerang menyisipkan instruksi berbahaya.
- **Jenis Injection:**
  1. **Command Injection:** Hacker menyisipkan perintah sistem operasi melalui input aplikasi.
  2. **SQL Injection:** Hacker menyisipkan query SQL untuk mengakses data sensitif.
     - **Tool:** SQLMap.
  3. **XSS (Cross-Site Scripting):** Hacker menyisipkan script berbahaya untuk mengendalikan browser user.
- **Dampak:** Data dapat diakses, dimodifikasi, atau dihancurkan.
- **Pencegahan:**
  - Gunakan prepared statements untuk query database.
  - Sanitasi input dari user.

### **A04: Insecure Design**

- **Definisi:** Kerentanan akibat desain aplikasi yang tidak memperhatikan keamanan.
- **Contoh:** Fitur "password recovery" yang tidak aman.
- **Dampak:** Hacker dapat mengeksploitasi kelemahan desain untuk mendapatkan akses tidak sah.
- **Pencegahan:**
  - Terapkan prinsip keamanan sejak awal pengembangan aplikasi (Secure by Design).

### **A05: Security Misconfiguration**

- **Definisi:** Kesalahan dalam konfigurasi sistem atau aplikasi.
- **Contoh:**
  - Penggunaan akun default tanpa perubahan kredensial.
  - Direktori atau file yang tidak dilindungi.
- **Dampak:** Hacker dapat mengeksploitasi sistem dengan mengakses area yang tidak terlindungi.
- **Pencegahan:**
  - Audit konfigurasi sistem secara rutin.
  - Nonaktifkan fitur yang tidak digunakan.

### **A06: Vulnerable and Outdated Components**

- **Definisi:** Menggunakan software, library, atau framework yang sudah usang dan rentan.
- **Dampak:** Hacker dapat mengeksploitasi kerentanan yang sudah diketahui di versi lama.
- **Pencegahan:**
  - Selalu perbarui komponen aplikasi.
  - Gunakan alat seperti Dependabot atau Snyk untuk memantau kerentanan.

### **A07: Identification and Authentication Failures**

- **Definisi:** Kelemahan dalam sistem identifikasi, autentikasi, atau manajemen sesi.
- **Contoh:** Sistem rentan terhadap serangan bruteforce.
- **Dampak:** Hacker bisa mendapatkan akses ke akun pengguna.
- **Pencegahan:**
  - Terapkan multi-factor authentication (MFA).
  - Gunakan bcrypt untuk hashing password.

### **A08: Software and Data Integrity Failures**

- **Definisi:** Kerentanan yang terjadi ketika aplikasi bergantung pada modul atau plugin yang tidak terpercaya.
- **Contoh:** Menggunakan library pihak ketiga yang berisi malware.
- **Dampak:** Data aplikasi atau pengguna dapat dirusak atau disusupi.
- **Pencegahan:**
  - Verifikasi sumber library atau plugin.
  - Gunakan signature-based verification untuk integritas software.

### **A09: Security Logging and Monitoring Failures**

- **Definisi:** Kegagalan dalam mencatat dan memonitor aktivitas keamanan.
- **Contoh:** Tidak mencatat login attempt yang gagal.
- **Dampak:** Serangan yang terjadi tidak terdeteksi, sehingga sulit untuk ditindaklanjuti.
- **Pencegahan:**
  - Gunakan alat monitoring seperti Splunk atau ELK Stack.
  - Konfigurasi logging untuk mencatat semua aktivitas yang relevan.

### **A10: Server-Side Request Forgery (SSRF)**

- **Definisi:** Serangan di mana hacker mengeksploitasi fungsi server untuk mengakses informasi yang tidak boleh diakses.
- **Contoh:** Hacker menggunakan SSRF untuk mengakses metadata cloud (contoh: AWS Metadata).
- **Dampak:** Hacker dapat mencuri data sensitif atau mendapatkan kontrol penuh terhadap sistem.
- **Pencegahan:**
  - Validasi input URL dengan whitelist.
  - Nonaktifkan permintaan ke jaringan internal dari server.

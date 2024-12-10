---
title: Memahami CSRF
prev: /docs/hacking/hacking_fundamentals/
---

## Apa itu CSRF?

Cross Site Request Forgery (CSRF) adalah kerentanan yang memungkinkan hacker untuk membujuk target melakukan tindakan yang tidak diinginkan, sering kali dilakukan melalui metode phishing. CSRF mengeksploitasi kepercayaan yang diberikan oleh sebuah aplikasi kepada browser pengguna.

## Dampak

Dampak dari CSRF sangat signifikan, terutama di Indonesia. Jika korban adalah pengguna biasa, kerugian yang dialami dapat berupa kerugian finansial atau kebocoran data pribadi. Namun, jika korban adalah seorang admin perusahaan, serangan ini dapat membahayakan seluruh perusahaan, termasuk data sensitif dan sistem operasional.

## Alur CSRF

![csrf](/images/csrf.svg)

- Ilustrasi di atas menunjukkan bagaimana hacker mengirim link phishing yang memuat permintaan untuk mengubah informasi akun korban.
- Cara kerja CSRF:
  1. Hacker membuat permintaan palsu (misalnya mengubah password akun).
  2. Hacker mengirimkan permintaan ini melalui link yang terlihat sah kepada korban.
  3. Ketika korban mengklik link tersebut, browser mereka otomatis mengirimkan permintaan beserta sesi cookie aktif, tanpa disadari oleh korban.
- Contoh: Hacker mengirim permintaan perubahan password, sehingga korban percaya dan tanpa sengaja mengubah password sesuai keinginan hacker.

## Alat untuk Mendeteksi CSRF

- **Burp Suite**: Membantu menganalisis dan memanipulasi request.
- **IBM AppScan**: Alat komersial untuk mengidentifikasi berbagai kerentanan termasuk CSRF.
- **OWASP ZAP (Zed Attack Proxy)**: Alat gratis yang dikembangkan oleh OWASP untuk pengujian keamanan aplikasi web.

## Pencegahan CSRF

1. **Validasi Request**:
   - Memastikan setiap permintaan yang dikirim berasal dari pengguna yang sah.
2. **CSRF Token**:
   - Menyisipkan token unik di setiap permintaan.
   - Token ini harus divalidasi oleh server untuk memverifikasi permintaan.
3. **Referer Header**:
   - Memastikan bahwa permintaan berasal dari halaman yang sah.
4. **Sesi yang Aman**:
   - Gunakan sesi cookie dengan atribut `SameSite` untuk membatasi akses lintas situs.
5. **Batasi HTTP Methods**:
   - Gunakan metode POST untuk permintaan yang sensitif.

## 3 Kondisi Serangan CSRF

1. **A Relevant Action**:
   - Serangan CSRF biasanya ditargetkan pada aksi yang istimewa atau sensitif, seperti mengubah data pengguna atau melakukan transaksi.
2. **Cookie-based Session Handling**:
   - Sistem hanya memvalidasi sesi cookie, sehingga hacker dapat memanfaatkannya untuk mengirim permintaan palsu.
3. **No Unpredictable Request Parameter**:
   - Permintaan dengan parameter yang mudah ditebak oleh hacker, seperti `password_new=smithy` atau `email=newuser@domain.com`.

## Contoh Praktis

Misalkan sebuah aplikasi memungkinkan pengguna mengubah alamat email mereka. Permintaan HTTP-nya seperti ini:

```
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
Cookie: session=yvthwsztyeQkAPzeQ5gHgTv1yxHfsAfE
email=wiener@normal-user.com
```

Permintaan di atas memenuhi 3 kondisi serangan CSRF. Hacker dapat membuat halaman web dengan kode HTML berikut:

```html
<img
  src="http://vulnerable-website.com/email/change?email=attacker@malicious.com"
  style="display:none;"
/>
```

Jika korban membuka halaman ini saat sedang login, browser mereka akan secara otomatis menyertakan cookie sesi aktif dalam permintaan, dan alamat email mereka akan diubah tanpa izin.

## Demo di DVWA

1. **Setup Awal**:

   - Buka DVWA di dua jendela browser: satu di mode biasa dan satu di mode private.
   - Login sebagai **admin** di jendela private.
   - Login sebagai **smithy** (akun hacker) di jendela biasa.

2. **Tujuan**:

   - Mengubah password admin menggunakan akun smithy.

3. **Langkah-Langkah**:

   - Login sebagai smithy dan buka menu "CSRF".
   - Masukkan username dan password untuk smithy, lalu klik "Change" untuk melihat bahwa password dapat diubah menggunakan parameter GET.

   ![csrfchange](/images/csrfchange.png)
   ![csrfget](/images/csrfget.png)

4. **Membuat Exploit**:

   - Buat file HTML dengan konten berikut:
     ```html {filename="index.html"}
     <h1>You won 1000 bitcoins!</h1>
     <a
       href="http://localhost:4280/vulnerabilities/csrf/?password_new=smithy&password_conf=smithy&change=Change"
       >Click here to claim your reward!</a
     >
     ```

5. **Menjalankan Server Lokal**:

   - Simpan file HTML tersebut dan jalankan server lokal:
     ```bash
     python3 -m http.server 8000
     ```
   - Periksa alamat IP lokal dengan `ifconfig` atau `ipconfig`.

6. **Serangan**:

   - Buka file HTML di browser admin (korban) menggunakan IP lokal, misalnya: `http://192.168.8.120:8000/index.html`.
     ![phising](/images/phising.png)
   - Klik link di halaman tersebut. Password admin akan otomatis berubah menjadi "smithy".
     ![success](/images/success.png)

7. **Validasi**:

   - Login kembali sebagai admin menggunakan password baru ("smithy") di browser hacker.
   - Admin tidak dapat login dengan password lama.

8. **Pencegahan**:
   - Gunakan CSRF token untuk memvalidasi setiap permintaan.

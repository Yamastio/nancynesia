---
title: Instalasti Lab DVWA
date: 2024-12-13
authors:
  - name: Yamastio
    link: https://github.com/yamastio
    image: https://github.com/yamastio.png
tags:
  - hacking_fundamentals
---

<!--more-->

## Apa itu DVWA?

DVWA atau Damn Vulnerable Web Application, merupakan web yang memang sengaja dibuat rentan untuk tujuan praktik hacking. Hacker pemula bisa belajar disini untuk menguji kemampuanya dengan mengeksplorasi kerentanan yang ada.

## Tujuan DVWA

Tujuanya adalah untuk membuat area praktik hacking yang legal, karena web ini memang dengan sengaja dibuat untuk kebutuhan praktik cybersecurity. DVWA sendiri dibuat dengan berbagai macam tingkat kesulitan yang bisa di pilih saat didalam web nantinya.

## Cara Instalasi DVWA dengan Docker:

1. **Install Docker** terlebih dahulu jika belum terpasang. Langkahnya instalasi bisa ke web official [Docker](https://www.docker.com/)
2. **Clone repository DVWA**:

   ```
   git clone https://github.com/digininja/DVWA.git
   ```

3. **Masuk ke folder DVWA**:

   ```
   cd DVWA
   ```

4. **Jalankan DVWA dengan Docker Compose**:

   ```
   docker compose up -d
   ```

5. **Akses DVWA** melalui browser di port yang disediakan (misalnya, `http://localhost`).
6. **Login** menggunakan username `admin` dan password `password`.
7. **Pastikan minimal setup check** sudah berhasil dan berwarna hijau, lalu klik **"Create"** atau **"Reset Database"**.
8. Setelah berhasil, Anda akan diarahkan ke halaman admin.

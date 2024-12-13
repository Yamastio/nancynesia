---
title: Web Penentration Testing
prev: /docs/hacking/hacking_fundamentals/
---

## Apa itu Web Penentration Testing

Web Penentration Testing adalah pengujian kerentanan web, dengan cara memposisikan seorang penguji seperti hacker, dari pola pikir sampai cara kerjanya, perbedaanya adalah Penentration Testing ini dilakukan atas persetujuan dan dengan izin dari pemilik sah web target.

Tujuanya adalah untuk mencari kerentanan yang ada dalam teknologi yang digunakan, lalu memberikan laporan terhadap kerentanan yang ada sehingga pemilik web mampu memberikan penanganan sebelum terjadinya serangan yang nyata.

## Fase Web Hacking

1. Reconnaisance -> Mengumpulkan informasi
2. Scanning --> Menganalisa web security
3. Exploitation --> Eksploitasi vulnerability
4. Covering Track --> Modifikasi Log Value, menghapus jejak

## Tools Web Hacking

### Google Dorking

- Teknik menggunakan layanan Advance Google Search untuk mencari informasi terkait target.
- Mencari konten yang susah dicari dengan pencarian biasa

### Robtext

- Comprehensive DNS Information
- Melakukan information gathering
- Mencari IP Address, atau jumlah IP yang digunakan pada sebuah website, karena website bisa menggunakan lebih dari satu IP Address
- Mencari Domain Names, Hostname, Routes, dll

### Knockpy

- Subdomain Enumerator
- Melakukan information gathering
- Mencari sub domain dari target
- Dengan menggunakan wordlist, untuk melakukan bruteforce

### Dirb

- Web content Scanner
- Mencari direktori tersembunyi maupun tidak tersembunyi
- Dicitonary based attack

### Nikto

- Web vulnerability scanner
- Gratis dan opensource
- Cara kerja dengan scanning web, mencari file berbahaya, software outdated, informasi terkait software, mencari subdomain

### Maltego

- Graphical Link Analysis
- Memproses realtime data mining
- Melihat social relationship
- Menentukan Infrastruktur dari sebuah internet, domain, dns, ip Address, dll
- Biasanya digunakan juga oleh para jurnalis, untuk melakukan OSINT(Open Source Inteligence)

### Burpsuite

- Web App Pentest
- Bug Bounty
- Fitur:
  - **Spyder**: Web crawler untuk melakukan pemetaan aplikasi web.
  - **Proxy**: Interceptor untuk memodifikasi request dan response.
  - **Intruder**: Automasi serangan yang dikustomisasi terhadap aplikasi web.
  - **Repeater**: Mengirim request berulang kali.
  - **Sequencer**: Mengecek entropi untuk memeriksa keamanan token acak yang dihasilkan oleh server.
  - **Decoder**: Melakukan encoding dan decoding pada parameter atau header data.
  - **Extender**: Menambahkan ekstensi eksternal untuk meningkatkan kinerja Burpsuite.
  - **Scanner**: Memindai kerentanan web (hanya tersedia di versi berbayar).

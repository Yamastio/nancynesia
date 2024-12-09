---
title: Fix Syntax Highlighting tidak aktif di Terminal Kali Linux
date: 2024-12-09
authors:
  - name: Yamastio
    link: https://github.com/yamastio
    image: https://github.com/yamastio.png
tags:
  - zsh
  - shell
  - terminal
---

<!--more-->

## Langkah untuk Menambahkan ZSH Syntax Highlighting

Berikut adalah langkah-langkah untuk menambahkan `zsh-syntax-highlighting` di Zsh agar fitur syntax highlighting dapat aktif:

### 1. Instal `zsh-syntax-highlighting`

Pastikan `zsh-syntax-highlighting` diinstal terlebih dahulu. Jalankan perintah berikut di terminal Anda:

```bash
sudo apt install zsh-syntax-highlighting
```

### 2. Tambahkan `source` di `~/.zshrc`

Untuk mengaktifkan `zsh-syntax-highlighting`, buka file `~/.zshrc` dengan editor teks favorit Anda, misalnya `nano` atau `vim`:

```bash
nano ~/.zshrc
```

Kemudian tambahkan baris berikut di akhir file `~/.zshrc`:

```bash
source /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```

Simpan dan tutup file tersebut. (Jika menggunakan `nano`, tekan `CTRL + X`, lalu `Y`, dan tekan `Enter`).

### 3. Terapkan Perubahan

Setelah menambahkan baris tersebut, jalankan perintah berikut agar perubahan diterapkan:

```bash
source ~/.zshrc
```

### 4. Mengatasi Error Jika Menggunakan Bash

Jika Anda mendapatkan error saat menjalankan `source ~/.zshrc`, berarti Anda mungkin menggunakan shell `bash`, bukan `zsh`. Berikut solusi untuk masalah ini:

1. **Masuk ke Zsh**: Anda perlu memastikan bahwa Anda menjalankan shell `zsh` saat mengaktifkan konfigurasi `~/.zshrc`. Jika Anda menggunakan `bash`, perintah-perintah Zsh tidak akan dikenali. Cobalah untuk masuk ke Zsh dengan mengetikkan perintah berikut di terminal:

   ```bash
   zsh
   ```

2. **Jalankan `source ~/.zshrc`**: Setelah masuk ke Zsh, jalankan:

   ```bash
   source ~/.zshrc
   ```

### 5. Instal Zsh dan Ubah Shell Default

Jika Zsh belum diinstal, instal dengan perintah berikut:

```bash
sudo apt install zsh
```

Kemudian ubah shell default Anda menjadi Zsh dengan perintah:

```bash
chsh -s $(which zsh)
```

Log out dan log in kembali untuk menerapkan perubahan ini.

## Mengapa Masalah Ini Terjadi?

### Perbedaan Sintaks

Bash dan Zsh memiliki perbedaan sintaks dan fitur. Perintah seperti `autoload`, `compinit`, dan `zstyle` adalah spesifik untuk Zsh, sehingga tidak akan dikenali oleh bash.

### File Konfigurasi

`~/.zshrc` adalah file konfigurasi untuk Zsh, sedangkan bash menggunakan `~/.bashrc` atau `~/.bash_profile`.

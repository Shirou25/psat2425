# PSAT 2024/2025 - Aplikasi Penilaian Sumatif Akhir Tahun

Aplikasi web berbasis PHP untuk Penilaian Praktek DevOps siswa kelas XI TJKT 1 di SMKN 1 Banyumas pada tahun ajaran 2024/2025.

---

## Fitur Utama

- Login/logout pengguna
- Dashboard data siswa
- Tambah, edit, hapus data siswa (CRUD)
- Upload file (opsional)
- Tampilan web sederhana dan responsif

## Cara Menjalankan di AWS

### 1. Siapkan Server EC2

- Buat instance EC2 dengan sistem operasi Linux (misalnya Amazon Linux 2 atau Ubuntu).
- Pastikan security group EC2 mengizinkan akses HTTP (port 80) dan SSH (port 22).

### 2. Siapkan Database RDS MySQL

- Buat database RDS MySQL di AWS.
- Catat endpoint, nama database, username, dan password.

### 3. Konfigurasi EC2

  Untuk Amazon Linux 2:

  ```bash
  sudo yum update -y
  sudo amazon-linux-extras enable php8.0
  sudo yum install -y httpd php php-mysqlnd
  sudo systemctl start httpd
  sudo systemctl enable httpd
  

  Untuk Ubuntu:

  ```bash
  sudo apt update
  sudo apt install -y apache2 php php-mysql libapache2-mod-php
  sudo systemctl start apache2
  sudo systemctl enable apache2
  

### 4. Deploy Aplikasi

- Clone repositori ke direktori web server:

  ```bash
  cd /var/www/html
  sudo rm -rf *
  sudo git clone https://github.com/Shirou25/psat2425.git .
  ```

- Berikan izin yang sesuai (jika diperlukan):

  ```bash
  sudo chown -R apache:apache /var/www/html   # untuk Amazon Linux
  sudo chown -R www-data:www-data /var/www/html  # untuk Ubuntu
  ```

### 5. Konfigurasi Database

- Buat file `.env` di direktori `/var/www/html` dengan isi seperti berikut (ganti dengan data RDS kamu):

  ```
  DB_HOST= (endpoint rds)
  DB_NAME= (nama db database)
  DB_USER= (username)
  DB_PASS=(password0
  ```

- Pastikan database database sudah dibuat di RDS dan tabel-tabelnya sesuai kebutuhan aplikasi.

### 6. Akses Aplikasi

- Buka browser dan akses `http://your-ec2-public-ip/`

- Login dengan:

  ```
  Username: admin
  Password: 123
  ```

---

## Cara Menggunakan Aplikasi

1. Login dengan akun admin
2. Lihat data siswa di dashboard
3. Tambah data baru lewat form input
4. Edit atau hapus data siswa sesuai kebutuhan
5. Logout saat selesai

---

## Struktur Direktori

```
├── dashboard.php
├── db.php
├── delete.php
├── edit.php
├── index.php
├── input.php
├── logout.php
├── menu.php
├── style.css
└── uploads/
```

---

Aplikasi Penilaian Sumatif Akhir Tahun

Aplikasi web berbasis PHP untuk Penilaian Praktek DevOps siswa kelas XI TJKT 1 di SMKN 1 Banyumas tahun ajaran 2024/2025.

---

## Fitur Utama

* Login/logout pengguna
* Dashboard data siswa
* CRUD data siswa (Tambah, Edit, Hapus)
* Upload file (opsional)
* Tampilan web sederhana dan responsif

---

## Cara Menjalankan di AWS

### 1. Siapkan Server EC2

* Buat instance EC2 dengan OS Linux (misal: Amazon Linux 2 atau Ubuntu).
* Pastikan Security Group mengizinkan akses:

  * HTTP (port 80)
  * SSH (port 22)

### 2. Siapkan Database RDS MySQL

* Buat database RDS MySQL di AWS.
* Catat informasi berikut:

  * Endpoint
  * Nama database
  * Username
  * Password

### 3. Konfigurasi EC2 (Contoh untuk Ubuntu)

* Pilih:

  * Name = (nama instance)
  * Application and OS Images = Ubuntu
  * Instance type = t2.micro atau t2.nano
  * Key pair = vockey
  * Security groups = SSH, HTTP, HTTPS (akses dari 0.0.0.0/0)
* Pada **Advanced details > User data** isi dengan script berikut:

```
#!/bin/bash
sudo apt update -y
sudo apt install -y apache2 php php-mysql libapache2-mod-php mysql-client
sudo rm -rf /var/www/html/{*,.*}
sudo git clone https://github.com/Shirou25/psat2425.git /var/www/html
sudo chmod -R 777 /var/www/html
echo DB_USER=(username) > /var/www/html/.env
echo DB_PASS=(password) >> /var/www/html/.env
echo DB_NAME=(database) >> /var/www/html/.env
echo DB_HOST=(endpoint rds) >> /var/www/html/.env
```

### 4. Konfigurasi Database RDS

* Pilih opsi:

  * Template = Free Tier
  * Engine = MySQL
  * Availability = Single-AZ
  * DB cluster identifier = (nama db)
  * Master username = (username)
  * Master password = (password)
  * Public access = No
  * Security groups = Pilih SG yang mengizinkan inbound MySQL (port 3306) dari anywhere (0.0.0.0/0)

---

### 5. Akses Aplikasi

* Buka browser dan akses:
  `http://<public-ip-ec2>/`
* Login menggunakan:

  ```
  Username: admin  
  Password: 123  
  ```

---

## Cara Menggunakan Aplikasi

1. Login dengan akun admin
2. Lihat data siswa di dashboard
3. Tambah data siswa baru melalui form input
4. Edit atau hapus data siswa sesuai kebutuhan
5. Logout setelah selesai

---

## Struktur Direktori Aplikasi

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

Kalau mau, saya bisa bantu juga buatkan file README.md ini dalam format markdown siap pakai, atau mau tambahan dokumentasi lain?


---

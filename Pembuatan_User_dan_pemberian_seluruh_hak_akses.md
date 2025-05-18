
# Panduan GRANT ALL PRIVILEGES dan Pembuatan Database oleh User Baru di MySQL (XAMPP CLI)

## Tujuan Pembelajaran
Peserta didik mampu:
- Membuat user baru di MySQL melalui command line (CLI).
- Memberikan hak akses penuh (GRANT ALL PRIVILEGES).
- Menguji apakah user dapat membuat dan mengakses database.

---

## Langkah-Langkah

### 1. Masuk ke MySQL melalui Command Line
```bash
mysql -u root -p
```

### 2. Membuat User Baru
```sql
CREATE USER 'siswa11'@'localhost' IDENTIFIED BY 'siswa123';
```

### 3. Memberikan Hak Akses Penuh ke Semua Database
```sql
GRANT ALL PRIVILEGES ON *.* TO 'siswa11'@'localhost' WITH GRANT OPTION;
```

### 4. Refresh Privileges
```sql
FLUSH PRIVILEGES;
```

### 5. Keluar dari MySQL
```sql
EXIT;
```

### 6. Uji Login dengan User Baru
```bash
mysql -u siswa11 -p
```

### 7. Buat Database Baru
```sql
CREATE DATABASE db_latihan_siswa;
```

Jika berhasil, maka `siswa11` sudah memiliki hak akses penuh dan bisa membuat database.

---

## Catatan Penting

- `WITH GRANT OPTION` memungkinkan user memberikan hak akses ke user lain.
- Jika tidak ingin memberikan akses penuh, gunakan hak akses yang lebih spesifik seperti:
  ```sql
  GRANT SELECT, INSERT, UPDATE ON nama_database.* TO 'siswa11'@'localhost';
  ```

---

## Evaluasi

1. Apa yang terjadi jika kita tidak menggunakan `FLUSH PRIVILEGES` setelah GRANT?
2. Buat user baru bernama `tes_user` dan beri hak SELECT saja ke database `db_perpus`.
3. Coba login sebagai `tes_user` dan akses tabel dari database `db_perpus`.

---

*Dokumen ini disusun untuk keperluan pembelajaran SMK RPL mata pelajaran Basis Data.*

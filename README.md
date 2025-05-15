### **Panduan Praktik DCL di Xampp Shell**
#### **A. Persiapan**
1. **Pastikan XAMPP sudah terinstall**:
   - Jalankan XAMPP, start **Apache** dan **MySQL**.
   - Buka **Xampp Shell** (via menu XAMPP atau `C:\xampp\mysql\bin\mysql.exe`).

2. **Login ke MySQL**:
   ```bash
   mysql -u root -p
   ```
   - Tekan Enter (password default kosong).

---

#### **B. Praktek Perintah DCL**
##### **1. Membuat User Baru**
```sql
CREATE USER 'siswa_smk'@'localhost' IDENTIFIED BY 'password123';
```
- **Penjelasan**: 
  - Membuat user baru bernama `siswa_smk` dengan password `password123`.
  - `@'localhost'` berarti user hanya bisa akses dari komputer lokal.

##### **2. Memberikan Hak Akses (GRANT)**
- **Contoh 1**: Beri akses **SELECT** (hanya baca data) ke database `sekolah`.
  ```sql
  GRANT SELECT ON sekolah.* TO 'siswa_smk'@'localhost';
  ```

- **Contoh 2**: Beri akses **penuh** ke tabel `siswa` dalam database `sekolah`.
  ```sql
  GRANT ALL PRIVILEGES ON sekolah.siswa TO 'siswa_smk'@'localhost';
  ```

##### **3. Mencabut Hak Akses (REVOKE)**
- Cabut akses **INSERT** dari user `siswa_smk`:
  ```sql
  REVOKE INSERT ON sekolah.* FROM 'siswa_smk'@'localhost';
  ```

##### **4. Melihat Hak Akses User**
```sql
SHOW GRANTS FOR 'siswa_smk'@'localhost';
```
- Hasilnya akan menampilkan daftar izin yang dimiliki user.

##### **5. Menghapus User**
```sql
DROP USER 'siswa_smk'@'localhost';
```

---

#### **C. Simulasi Kasus Nyata**
**Scenario**:  
- User `guru` hanya boleh **melihat** (`SELECT`) dan **menambah** (`INSERT`) data di tabel `nilai`, tapi tidak boleh menghapus.

**Langkah**:
```sql
-- 1. Buat user guru
CREATE USER 'guru'@'localhost' IDENTIFIED BY 'guru123';

-- 2. Beri akses SELECT dan INSERT
GRANT SELECT, INSERT ON sekolah.nilai TO 'guru'@'localhost';

-- 3. Pastikan tidak ada akses DELETE
REVOKE DELETE ON sekolah.nilai FROM 'guru'@'localhost';
```

---

#### **D. Verifikasi**
1. **Login sebagai user baru** (uji hak akses):
   ```bash
   mysql -u siswa_smk -p
   ```
   - Masukkan password (`password123`).

2. **Coba akses database**:
   ```sql
   USE sekolah;
   SELECT * FROM siswa;  -- Jika GRANT SELECT diberikan, ini akan berhasil.
   DELETE FROM siswa;    -- Akan gagal jika tidak diizinkan.
   ```

---

#### **E. Tips untuk Siswa**
1. **Jangan gunakan `root`** untuk praktik sehari-hari. Biasakan pakai user dengan hak terbatas.
2. **Password harus kuat**: Contoh: `SiswaSMK_2024!`.
3. **Error umum**:
   - `Access denied`: Pastikan hak akses sudah diberikan dengan `GRANT`.
   - `User already exists`: Hapus dulu dengan `DROP USER`.

---

#### **F. Tugas Praktik Mandiri**
1. Buat user `admin_perpus` dengan hak akses **SELECT, INSERT, UPDATE** di database `perpustakaan`.
2. Cabut akses **UPDATE** setelahnya.
3. Verifikasi dengan login sebagai `admin_perpus`.

---

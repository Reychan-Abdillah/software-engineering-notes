
# AUTO_INCREMENT, DELETE, dan TRUNCATE

## 1. Memahami AUTO_INCREMENT

`AUTO_INCREMENT` adalah atribut MySQL yang membuat nilai angka pada kolom tertentu dihasilkan secara otomatis ketika record baru dimasukkan.

Contoh:

```sql
CREATE TABLE products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100)
);
```

Ketika data baru dimasukkan tanpa menentukan ID, MySQL akan menghasilkan nilai ID secara otomatis.

### Apakah AUTO_INCREMENT selalu berurutan?

Tidak.

Misalnya:

| id | name |
|---:|---|
| 1 | Keyboard |
| 2 | Mouse |
| 3 | Monitor |
| 7 | Headset |

ID tidak harus berurutan tanpa celah.

Jika sebuah record dihapus, nilai ID tersebut tidak otomatis digunakan kembali.

AUTO_INCREMENT bertujuan menghasilkan identitas unik, bukan nomor urut berdasarkan jumlah baris.

---

## 2. DELETE — Menghapus Baris Data

```sql
DELETE FROM products
WHERE id = 1;
```

Menghapus baris dengan ID 1.

Untuk menghapus seluruh baris:

```sql
DELETE FROM products;
```

Karakteristik DELETE:
- Bisa menggunakan WHERE.
- Bisa menghapus sebagian atau seluruh baris.
- Struktur tabel tetap ada.
- Tidak otomatis mereset AUTO_INCREMENT.
- Dapat dibatalkan dengan ROLLBACK jika dijalankan dalam transaksi yang belum di-commit dan menggunakan transactional storage engine seperti InnoDB.

---

## 3. TRUNCATE — Mengosongkan Tabel

```sql
TRUNCATE TABLE products;
```

Menghapus seluruh baris dalam tabel sekaligus.

Karakteristik TRUNCATE:
- Mengosongkan seluruh isi tabel.
- Tidak mendukung WHERE.
- Struktur tabel tetap tersedia.
- Mereset penghitung AUTO_INCREMENT ke nilai awal.
- Termasuk DDL (Data Definition Language).
- Tidak dapat dibatalkan menggunakan ROLLBACK seperti DELETE dalam transaksi biasa karena TRUNCATE menyebabkan implicit commit di MySQL.

---

## 4. Perbandingan DELETE dan TRUNCATE

| Aspek | DELETE | TRUNCATE |
|---|---|---|
| Kategori SQL | DML | DDL |
| Menghapus data | Ya | Ya |
| Menghapus seluruh baris | Bisa | Ya |
| Menghapus baris tertentu | Bisa menggunakan WHERE | Tidak bisa |
| Struktur tabel | Tetap ada | Tetap ada |
| Reset AUTO_INCREMENT | Tidak otomatis | Ya |
| Rollback dalam transaksi InnoDB | Bisa sebelum commit | Tidak bisa dalam transaksi biasa |
| Kinerja untuk mengosongkan tabel besar | Umumnya lebih berat | Umumnya lebih cepat |

TRUNCATE merupakan operasi DDL yang dioptimalkan untuk mengosongkan tabel. Jangan menganggapnya sekadar DELETE yang dijalankan satu per satu.

---

## 5. Kapan Menggunakan DELETE dan TRUNCATE?

Gunakan DELETE ketika:
- Hanya ingin menghapus baris tertentu.
- Ingin menggunakan kondisi WHERE.
- Membutuhkan kemungkinan ROLLBACK sebelum transaksi di-commit.

Gunakan TRUNCATE ketika:
- Ingin mengosongkan seluruh tabel.
- Tidak membutuhkan kondisi WHERE.
- Memang ingin mereset penghitung AUTO_INCREMENT.

Perhatian: TRUNCATE dapat ditolak apabila tabel masih direferensikan oleh foreign key dari tabel lain.

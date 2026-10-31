
# MySQL — Transactions & Data Recovery

## 1. Memahami Autocommit

MySQL umumnya menggunakan autocommit secara default.

Artinya, perubahan data akan otomatis di-commit setelah sebuah statement berhasil dijalankan, kecuali transaksi manual sedang digunakan atau autocommit dinonaktifkan.

## 2. COMMIT

Digunakan untuk menyimpan perubahan dalam transaksi.

```sql
COMMIT;
```

## 3. ROLLBACK

Digunakan untuk membatalkan perubahan yang belum di-commit dalam transaksi yang masih aktif.

```sql
ROLLBACK;
```

ROLLBACK tidak bisa digunakan untuk membatalkan perubahan yang sudah di-commit.

Kemampuan rollback juga bergantung pada transactional storage engine, seperti InnoDB.

## 4. BACKUP

Backup adalah salinan database yang dibuat untuk membantu pemulihan ketika data hilang atau rusak.

Pemulihan dapat dilakukan menggunakan backup yang tersedia.

## 5. BINARY LOG

Binary log mencatat perubahan yang terjadi pada MySQL Server apabila binary logging diaktifkan.

Binary log dapat digunakan bersama backup untuk melakukan point-in-time recovery.

Namun, pemulihan hanya dapat dilakukan jika backup dan rangkaian binary log yang diperlukan tersedia dan valid.

## 6. Catatan Penting

- ROLLBACK hanya membatalkan perubahan yang belum di-commit dalam transaksi yang masih aktif.
- BACKUP menyediakan salinan data untuk pemulihan.
- BINARY LOG membantu merekonstruksi perubahan setelah backup sampai titik waktu tertentu.
- Mengaktifkan binary log saja tidak menjamin data yang sudah hilang dapat dipulihkan.

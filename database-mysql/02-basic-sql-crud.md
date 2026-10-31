
# Basic SQL — CRUD Operations



Materi tentang INSERT, SELECT, WHERE, UPDATE, dan DELETE sebaiknya berada di file tersendiri karena ini adalah materi penggunaan bahasa SQL untuk mengelola data.



## 1. Memahami CRUD

CRUD merupakan empat operasi dasar untuk mengelola data dalam database.

| Operasi | SQL | Fungsi |
|---|---|---|
| Create | INSERT | Menambahkan data. |
| Read | SELECT | Membaca data. |
| Update | UPDATE | Memperbarui data. |
| Delete | DELETE | Menghapus data. |

---

## 2. INSERT — Menambahkan Data

Digunakan untuk memasukkan data baru ke dalam tabel.

```sql
INSERT INTO products (name, price, stock)
VALUES ('Laptop', 8000000, 5);
```

Penjelasan:

- `INSERT INTO products`: menentukan tabel tujuan.
- `(name, price, stock)`: menentukan kolom yang akan diisi.
- `VALUES`: menentukan nilai untuk masing-masing kolom.

Kolom `id` tidak perlu diisi karena menggunakan `AUTO_INCREMENT`.

---

## 3. SELECT — Membaca Data

Digunakan untuk mengambil data dari tabel.

Mengambil seluruh kolom:

```sql
SELECT * FROM products;
```

Mengambil kolom tertentu:

```sql
SELECT name, price FROM products;
```

Tanda `*` berarti seluruh kolom yang tersedia.

---

## 4. WHERE — Menentukan Kondisi

`WHERE` digunakan untuk menentukan kondisi agar hanya baris yang memenuhi kondisi tersebut yang diproses.

Contoh:

```sql
SELECT * FROM products
WHERE price > 1700000;
```

Menampilkan produk yang harganya lebih dari 1.700.000.

WHERE juga bisa digunakan bersama SELECT, UPDATE, dan DELETE.

---

## 5. UPDATE — Memperbarui Data

Digunakan untuk mengubah nilai data yang sudah tersimpan.

```sql
UPDATE products
SET price = 150000
WHERE id = 1;
```

Artinya, memperbarui harga produk dengan ID 1 menjadi 150.000.

### Mengapa WHERE penting?

Tanpa WHERE, seluruh baris dalam tabel akan terkena perubahan.

Contoh:

```sql
UPDATE products
SET price = 150000;
```

Query tersebut akan mengubah harga seluruh produk menjadi 150.000.

Biasakan memeriksa data menggunakan SELECT sebelum menjalankan UPDATE.

---

## 6. DELETE — Menghapus Data

Digunakan untuk menghapus baris data dari tabel.

```sql
DELETE FROM products
WHERE id = 1;
```

Hanya menghapus produk dengan ID 1.

### Risiko DELETE tanpa WHERE

```sql
DELETE FROM products;
```

Query tersebut menghapus seluruh baris dalam tabel `products`.

Namun, struktur tabel tetap ada.

### Praktik aman

Sebelum menjalankan UPDATE atau DELETE, periksa terlebih dahulu data yang akan terkena perubahan.

```sql
SELECT * FROM products
WHERE id = 1;
```

Pastikan kondisi dan data yang dipilih sudah benar.

---

## 7. Arah Pembelajaran Berikutnya

Setelah memahami CRUD, pelajari:

1. ORDER BY — mengurutkan data.
2. LIMIT — membatasi jumlah hasil.
3. OFFSET — menentukan posisi awal data yang ditampilkan.
4. JOIN — menggabungkan data dari beberapa tabel.

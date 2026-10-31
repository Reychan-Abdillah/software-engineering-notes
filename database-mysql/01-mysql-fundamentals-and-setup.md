
# MySQL Fundamentals — Database & Table Setup



Catatan ini berfokus pada pengenalan MySQL, struktur database, dan persiapan database untuk aplikasi CRUD.



## 1. Mengenal MySQL Server

**MySQL Server** adalah sistem database yang menerima koneksi dari aplikasi client, menjalankan query SQL, mengelola database, serta mengembalikan hasil query.

Aplikasi yang bisa berkomunikasi dengan MySQL Server antara lain:
- MySQL Workbench
- Backend Node.js
- Aplikasi lain yang menggunakan driver MySQL

**MySQL Workbench** adalah aplikasi GUI untuk mengelola MySQL Server. Kita bisa membuat database, membuat tabel, menjalankan query SQL, dan melihat data melalui Workbench.

Catatan: MySQL Workbench bukan MySQL Server. Keduanya memiliki fungsi berbeda.

---

## 2. Memahami Database, Table, Row, dan Column

Sebelum menggunakan MySQL, pahami empat istilah dasar berikut:

- **Database:** tempat untuk mengelompokkan dan menyimpan tabel-tabel yang digunakan oleh aplikasi.
- **Table:** struktur untuk menyimpan kumpulan data dengan kolom-kolom tertentu.
- **Column:** atribut atau jenis informasi yang disimpan pada setiap baris.
- **Row:** satu baris data atau satu record di dalam tabel.

Contoh:

Dalam aplikasi CRUD, terdapat database `crud_app` yang memiliki tabel `products`.

Tabel `products` memiliki kolom:
- `id`
- `name`
- `price`
- `stock`

Contoh satu row:

| id | name | price | stock |
|---:|---|---:|---:|
| 1 | Keyboard | 150000 | 10 |

Baris tersebut merupakan satu record produk.

---

## 3. Persiapan Database

Tahapan persiapan database untuk proyek CRUD App:

1. Menginstal MySQL Server.
2. Menginstal MySQL Workbench.
3. Membuat koneksi ke MySQL Server.
4. Membuat database `crud_app`.
5. Membuat tabel `products`.
6. Memeriksa struktur tabel.
7. Memasukkan beberapa data contoh.

---

## 4. Membuat dan Menggunakan Database

### Membuat database

```sql
CREATE DATABASE crud_app;
```

Membuat database baru bernama `crud_app`.

### Melihat daftar database

```sql
SHOW DATABASES;
```

Menampilkan daftar database yang tersedia di MySQL Server.

### Memilih database

```sql
USE crud_app;
```

Memilih `crud_app` sebagai database aktif untuk koneksi saat ini.

Query berikutnya akan menggunakan database tersebut jika tidak secara eksplisit menyebut database lain.

---

## 5. Membuat Tabel

Setelah database dibuat dan dipilih, kita bisa membuat tabel untuk menyimpan data produk.

```sql
CREATE TABLE products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) NOT NULL,
    stock INT NOT NULL
);
```

### Penjelasan struktur tabel

| Kolom | Tipe Data | Fungsi |
|---|---|---|
| `id` | `INT` | Menyimpan identitas numerik produk. |
| `name` | `VARCHAR(100)` | Menyimpan nama produk maksimal 100 karakter. |
| `price` | `DECIMAL(10,2)` | Menyimpan harga dengan dua angka desimal. |
| `stock` | `INT` | Menyimpan jumlah stok produk. |

### Memahami atribut penting

- **AUTO_INCREMENT:** membuat MySQL menghasilkan nilai angka secara otomatis ketika record baru dimasukkan.
- **PRIMARY KEY:** menetapkan identitas unik setiap baris. Nilainya tidak boleh duplikat dan tidak boleh `NULL`.
- **NOT NULL:** mewajibkan kolom memiliki nilai dan tidak boleh berisi `NULL`.
- **DECIMAL(10,2):** memiliki presisi total 10 digit, dengan 2 digit di belakang koma. Cocok untuk nilai uang karena presisinya tetap.

---

## 6. Mengubah Struktur Tabel

Struktur tabel yang sudah dibuat bisa diubah menggunakan `ALTER TABLE`.

Contoh menambahkan kolom `status_produk`:

```sql
ALTER TABLE products
ADD COLUMN status_produk VARCHAR(20) NOT NULL DEFAULT 'aktif';
```

Penjelasan:

- `ALTER TABLE products`: mengubah struktur tabel `products`.
- `ADD COLUMN`: menambahkan kolom baru.
- `status_produk VARCHAR(20)`: membuat kolom dengan tipe data teks maksimal 20 karakter.
- `NOT NULL`: kolom tidak boleh berisi `NULL`.
- `DEFAULT 'aktif'`: menggunakan nilai `aktif` apabila INSERT tidak memberikan nilai untuk kolom tersebut.

---

## 7. Memeriksa Struktur Database

### Melihat daftar tabel

```sql
SHOW TABLES;
```

Menampilkan tabel yang tersedia di database aktif.

### Melihat struktur tabel

```sql
DESCRIBE products;
```

Menampilkan informasi seperti:
- Nama kolom.
- Tipe data.
- Apakah kolom boleh berisi `NULL`.
- Informasi primary key.
- Atribut seperti `AUTO_INCREMENT`.

---

## 8. Arah Pembelajaran Berikutnya

Setelah memahami database dan struktur tabel, pelajari:

1. SQL CRUD: INSERT, SELECT, UPDATE, DELETE.
2. WHERE dan operator kondisi.
3. ORDER BY untuk mengurutkan data.
4. LIMIT dan OFFSET untuk membatasi hasil dan pagination.
5. Relasi antar tabel dan database design.

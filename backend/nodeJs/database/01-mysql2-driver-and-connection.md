
# Node.js MySQL2 — Driver & Database Connection

## 1. Apa itu MySQL2?

`mysql2` adalah package Node.js yang menyediakan driver untuk berkomunikasi dengan MySQL Server.

Driver bertugas menjadi perantara komunikasi antara aplikasi Node.js dan MySQL Server.

Dengan mysql2, aplikasi Node.js dapat:
- Membuat koneksi ke MySQL Server.
- Mengirim query SQL.
- Menerima hasil query.
- Menambahkan, membaca, mengubah, dan menghapus data.

## 2. Menginstal MySQL2

Jalankan perintah berikut di folder backend:

```bash
npm install mysql2
```

## 3. Callback API dan Promise API

MySQL2 menyediakan API berbasis callback dan Promise.

### Callback API

```javascript
import mysql from "mysql2";
```

Menggunakan callback untuk menangani hasil operasi asynchronous.

### Promise API

```javascript
import mysql from "mysql2/promise";
```

Menggunakan Promise sehingga operasi asynchronous dapat ditangani dengan async/await.

`mysql2/promise` bukan package npm yang berbeda. Itu adalah entry point Promise API dari package mysql2 yang sama.

## 4. createConnection()

Digunakan untuk membuat satu koneksi langsung antara aplikasi Node.js dan MySQL Server.

Contoh:

```javascript
import mysql from "mysql2/promise";

const db = await mysql.createConnection({
    host: "127.0.0.1",
    user: "root",
    password: "PASSWORD_MYSQL",
    database: "crud_app"
});
```

Penjelasan konfigurasi:

| Properti | Fungsi |
|---|---|
| `host` | Alamat MySQL Server. |
| `user` | Username MySQL. |
| `password` | Password MySQL. |
| `database` | Database yang ingin digunakan. |

## 5. createPool()

Digunakan untuk membuat kumpulan koneksi database yang dapat digunakan kembali oleh aplikasi.

Berbeda dengan createConnection yang membuat satu koneksi langsung, createPool mengelola sejumlah koneksi agar dapat digunakan oleh banyak operasi aplikasi.

Connection pool berguna ketika aplikasi melayani banyak request secara bersamaan.

## 6. Perbandingan createConnection dan createPool

| Aspek | createConnection | createPool |
|---|---|---|
| Koneksi | Satu koneksi langsung | Mengelola kumpulan koneksi |
| Penggunaan | Latihan dan proses sederhana | Aplikasi yang membutuhkan pengelolaan koneksi berulang |
| Pengelolaan | Koneksi dikelola secara langsung | Pool mengelola peminjaman dan penggunaan kembali koneksi |

Catatan: Untuk tahap belajar koneksi dan query dasar, kita menggunakan createConnection terlebih dahulu. Connection pooling akan dipelajari lebih lanjut saat mengembangkan backend API.

## 7. Menutup Koneksi

```javascript
await db.end();
```

Digunakan untuk mengakhiri sesi koneksi yang dibuat menggunakan createConnection.

Perintah ini tidak mematikan MySQL Server dan tidak menghapus database.

Untuk connection pool, pengelolaan penutupannya menggunakan metode pool yang sesuai, misalnya `pool.end()`.

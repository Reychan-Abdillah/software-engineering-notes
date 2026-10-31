
# Node.js MySQL2 — Executing SQL Queries

## 1. Mengimpor Koneksi Database

Koneksi yang dibuat di `db.js` dapat digunakan oleh file lain melalui export dan import.

Contoh:

```javascript
// db.js
export default db;
```

Mengimpor koneksi:

```javascript
// index.js
import db from "./db.js";
```

## 2. Menjalankan Query dengan db.execute()

`db.execute()` digunakan untuk mengirim query SQL dari aplikasi Node.js ke MySQL Server melalui driver mysql2.

Contoh SELECT:

```javascript
const [rows] = await db.execute(
    "SELECT * FROM products"
);
```

Penjelasan:
- `db.execute()`: menjalankan query SQL.
- `await`: menunggu operasi asynchronous selesai.
- `rows`: variabel yang menampung data hasil SELECT.

## 3. Memahami Hasil execute()

Dengan Promise API, execute mengembalikan hasil operasi beserta informasi field ketika tersedia.

Untuk SELECT:

```javascript
const [rows, fields] = await db.execute(
    "SELECT * FROM products"
);
```

- `rows`: kumpulan baris hasil query.
- `fields`: metadata mengenai kolom hasil query.

Untuk INSERT, elemen pertama berisi informasi hasil operasi, yang biasanya disimpan dalam variabel `result`.

```javascript
const [result] = await db.execute(
    "INSERT INTO products (name, price, stock) VALUES (?, ?, ?)",
    ["Keyboard", 150000, 10]
);
```

## 4. Parameterized Query

Parameterized query menggunakan placeholder `?` untuk memisahkan nilai input dari struktur SQL.

Contoh:

```javascript
const [result] = await db.execute(
    "INSERT INTO products (name, price, stock) VALUES (?, ?, ?)",
    ["Keyboard", 150000, 10]
);
```

Urutan nilainya:
- Placeholder pertama: nama produk.
- Placeholder kedua: harga.
- Placeholder ketiga: stok.

Nilai akan diikat sesuai urutan placeholder.

Keuntungan:
- Memisahkan input pengguna dari struktur query.
- Membantu mencegah SQL Injection.
- Membuat query dengan nilai dinamis lebih terstruktur.

## 5. Menangani Error

Operasi database dapat gagal, sehingga perlu ditangani.

```javascript
try {
    const [rows] = await db.execute(
        "SELECT * FROM products"
    );

    console.log(rows);

} catch (error) {
    console.error("Query gagal:", error.message);
}
```

- `try`: menjalankan operasi yang berpotensi gagal.
- `catch`: menangani error yang terjadi.

## 6. Menutup Koneksi

```javascript
await db.end();
```

Mengakhiri koneksi database yang sebelumnya dibuat dengan createConnection.

Dalam script sederhana, koneksi dapat ditutup setelah seluruh query selesai.

Biasanya penutupan koneksi ditempatkan dalam finally agar tetap dijalankan setelah proses try atau catch selesai.

```javascript
try {
    const [rows] = await db.execute(
        "SELECT * FROM products"
    );

    console.log(rows);

} catch (error) {
    console.error(error.message);

} finally {
    await db.end();
}
```

Catatan: Dalam aplikasi backend berbasis Express, pengelolaan koneksi biasanya menggunakan connection pool. Kita tidak menutup seluruh pool setelah setiap request.

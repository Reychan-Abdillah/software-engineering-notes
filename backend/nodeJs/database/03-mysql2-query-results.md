
# MySQL2 — Understanding Query Results

Ketika Node.js menjalankan query menggunakan `mysql2/promise`, kita bisa menerima informasi hasil operasi database.

## 1. Menjalankan INSERT

```javascript
const [result] = await db.execute(
    "INSERT INTO products (name, price, stock) VALUES (?, ?, ?)",
    ["Keyboard", 150000, 10]
);
```

Untuk operasi INSERT, elemen pertama yang dikembalikan berisi informasi hasil operasi.

## 2. result.insertId

```javascript
console.log(result.insertId);
```

Mengembalikan nilai ID yang dihasilkan oleh AUTO_INCREMENT untuk data yang baru dimasukkan.

Contoh:

```text
16
```

Angka tersebut merupakan ID record baru yang diberikan oleh MySQL Server, bukan angka yang dibuat oleh JavaScript.

Properti ini relevan ketika INSERT menghasilkan nilai AUTO_INCREMENT.

## 3. result.affectedRows

```javascript
console.log(result.affectedRows);
```

Menampilkan jumlah baris yang terpengaruh oleh query.

Contoh INSERT satu produk:

```text
1
```

Artinya satu baris berhasil ditambahkan.

Nilai affectedRows juga tersedia untuk operasi seperti UPDATE dan DELETE, dengan makna jumlah baris yang terpengaruh oleh operasi tersebut.

## 4. Perbedaan insertId dan affectedRows

| Properti | Fungsi |
|---|---|
| `result.insertId` | ID AUTO_INCREMENT yang dihasilkan untuk INSERT. |
| `result.affectedRows` | Jumlah baris yang terpengaruh oleh operasi. |

Catatan:

Untuk SELECT, elemen pertama dari hasil execute berisi kumpulan baris data, biasanya kita beri nama `rows`.

Untuk INSERT, elemen pertama berisi informasi hasil operasi, biasanya kita beri nama `result`.

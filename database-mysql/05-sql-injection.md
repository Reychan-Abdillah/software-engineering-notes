### Materi: Parameterized Query & SQL Injection

#### 1. Cara Aman (Parameterized Queries)
```javascript
const [result] = await db.execute(
    "INSERT INTO products (name, price, stock) VALUES (?, ?, ?)",
    ["Keyboard", 150000, 10]
);
```

#### 2. Bagaimana SQL Injection Bekerja?
Ketika kita mengambil input langsung dari pengguna tanpa validasi dan menggabungkannya ke dalam perintah database.

**Contoh TIDAK AMAN (String Concatenation):**
```javascript
const name = userInput;
const sql = `SELECT * FROM products WHERE name = '${name}'`;
const [rows] = await db.query(sql);
```     
Masalahnya: Input langsung digabungkan ke dalam query SQL. Pengguna yang berniat jahat dapat menyelipkan perintah SQL di dalam input tersebut.

**Simulasi Serangan:**
Jika user memasukkan input: `' OR '1' = '1'`
Maka query akhir yang dieksekusi database menjadi:
```sql
SELECT * FROM products WHERE name = '' OR '1' = '1'
```
Karena `'1'='1'` selalu bernilai TRUE, database akan mengabaikan kondisi nama dan Query dapat mengembalikan seluruh baris yang memenuhi kondisi OR tersebut. Jika hasilnya kemudian diekspos oleh aplikasi, hal ini dapat menyebabkan kebocoran data.

#### 3. Mengapa Parameterized Queries Aman?
Pada parameterized queries, proses pengiriman dibagi menjadi dua tahap dengan jalur terpisah:
1. **Tahap 1 (Kirim Struktur):** Aplikasi mengirimkan template query: `SELECT * FROM products WHERE name = ?`. Database menganalisis, menyusun rencana eksekusi, dan mengunci struktur query ini. Posisi `?` dikunci mati sebagai tempat data, bukan tempat perintah.
2. **Tahap 2 (Kirim Data):** Aplikasi mengirimkan nilai variabelnya. Database memasukkan nilai tersebut ke posisi `?` tanpa melakukan kompilasi ulang. Semua karakter khusus (seperti kutip `'` atau kata `OR`) otomatis dianggap sebagai teks biasa (literal value).

⚠️ *Catatan: Placeholder `?` hanya bisa digunakan untuk nilai data. Tidak bisa digunakan untuk nama tabel atau nama kolom.*

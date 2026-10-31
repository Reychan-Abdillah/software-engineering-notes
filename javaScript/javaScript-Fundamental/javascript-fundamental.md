Statement(pernyataan) dalam javascript adalah sebuah instruksi atau perintah lengkap yang memberi tahu komputer atau browser untuk melakukan suatu aksi tertentu
contoh
1. Deklarasi variabel(declaration variabel)
perintah untuk membuat wadah penyimpanan data baru
let nama = "reyhan"
const pi = 3.14

2. Penugasan (Assignement Statement)
Perintah untuk memasukan atau mengubah nilai di dalam variabel
nama = "andi"


3. Pemanggilan Fungsi (Function Call Statement)
Perintah untuk menjalankan sebuah blok kode atau fungsi yang sudah dibuat.
javascript
console.log("Halo, selamat datang!");
alert("Data berhasil disimpan!");


4. Percabangan (Conditional Statement)
Perintah untuk menentukan arah jalannya program berdasarkan kondisi tertentu.
• Contoh if-else:javascript
let nilai = 80;

if (nilai >= 75) {
    console.log("Lulus");
} else {
    console.log("Tidak Lulus");
}


Contoh switch-case:javascript
let warna = "merah";
switch(warna) {
    case "merah":
        console.log("Berhenti");
        break;
    case "hijau":
        console.log("Jalan");
        break;
}


5. Perulangan (Loop Statement)
Perintah untuk mengeksekusi blok kode berulang kali selama kondisi terpenuhi.
• Contoh for loop:javascript
for (let i = 1; i <= 3; i++) {
    console.log("Perulangan ke-" + i);
}
Contoh while loop:javascript
let hitung = 0;
while (hitung < 3) {
    console.log("Hitung: " + hitung);
    hitung++;
}

Dimana letak statement dan expression?
let total = 10 + 20
let total = adalah statement(karena melakukan aksi deklarasi(pernyataan ringkas) dan penyimpanan nilai).

jadi pada intinya statement adalah satu kalimat perintah utuh yang melakukan tindakan dalam pemrograman
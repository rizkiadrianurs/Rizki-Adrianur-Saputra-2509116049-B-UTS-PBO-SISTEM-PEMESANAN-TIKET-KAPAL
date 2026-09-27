# Minpro 2 PBO — Sistem Pemesanan Tiket Kapal

**Nama**  : Rizki Adrianur Saputra
**NIM**   : 2509116049
**Kelas** : B

---

## 1. Deskripsi Proyek

Program ini merupakan **Sistem Pemesanan Tiket Kapal** berbasis Java yang dijalankan melalui console/CLI. Program ini merupakan pengembangan dari Minpro 1 dengan menambahkan konsep **Inheritance**, **Encapsulation**, **validasi input**, **dummy data**, **struktur MVC**, dan **Polymorphism**.

Program ini digunakan untuk mengelola data pemesanan tiket kapal, dengan fitur:

- Menambahkan data pemesanan.
- Menampilkan seluruh data pemesanan.
- Mengubah data pemesanan.
- Menghapus data pemesanan.
- Mengakhiri program melalui menu keluar.

Data pemesanan disimpan sementara selama program berjalan menggunakan `ArrayList<Pemesanan>`. Saat program pertama kali dijalankan, `ArrayList` sudah berisi **2 dummy data** sehingga menu Tampilkan Pemesanan langsung menampilkan data tanpa perlu input dari awal.

### Struktur Folder

```
Sistem_pemesanan_tiket_Kapal
└── Source Packages
    ├── controller
    │   └── PemesananController.java
    ├── main
    │   └── Sistem_pemesanan_tiket_Kapal.java
    ├── model
    │   ├── Kapal.java
    │   ├── KapalEkonomi.java
    │   ├── KapalVIP.java
    │   ├── Pemesanan.java
    │   └── Penumpang.java
    └── view
        └── PemesananView.java
```

### Struktur Kelas

| Kelas | Tanggung Jawab |
|---|---|
| `Kapal` | **Superclass.** Menyimpan data umum kapal berupa nama kapal, tujuan, dan harga tiket. |
| `KapalEkonomi` | **Subclass** dari `Kapal`. Menambahkan atribut `fasilitasEkonomi`. |
| `KapalVIP` | **Subclass** dari `Kapal`. Menambahkan atribut `fasilitasVIP`. |
| `Penumpang` | Menyimpan data penumpang berupa nama, NIK, dan umur. |
| `Pemesanan` | Menggabungkan data `Penumpang` dan `Kapal`, jumlah tiket, serta menghitung total harga. |
| `PemesananView` | Menampilkan menu, menerima input, dan memvalidasi input pengguna. |
| `PemesananController` | Menjalankan alur program dan mengelola proses CRUD data pemesanan. |
| `Sistem_pemesanan_tiket_Kapal` | Class utama yang berisi method `main`. |

---

## 2. Alur Program

### Program Dimulai dan Pengisian Dummy Data

Program dijalankan melalui method `main` pada kelas `Sistem_pemesanan_tiket_Kapal`. Method tersebut membuat objek `PemesananController` lalu memanggil `jalankanProgram()`.

Saat objek `PemesananController` dibuat, constructor memanggil method `isiDummyData()` yang menambahkan 2 data awal ke dalam `ArrayList`:

| ID | Penumpang | Kapal | Tujuan | Jenis | Jumlah Tiket |
|---|---|---|---|---|---|
| 101 | Andi | KM Bukit Siguntang | Balikpapan | VIP | 2 |
| 102 | Budi | KM Lambelu | Makassar | Ekonomi | 1 |

### Menu Utama

Program menampilkan menu utama secara berulang menggunakan perulangan `do-while`. Perulangan akan terus berjalan sampai pengguna memilih menu Keluar.

| No. | Menu | Fungsi |
|---|---|---|
| 1 | **Tambah Pemesanan** | Menambahkan data pemesanan tiket kapal. |
| 2 | **Tampilkan Pemesanan** | Menampilkan seluruh data pemesanan yang tersimpan. |
| 3 | **Ubah Pemesanan** | Mengubah data pemesanan yang telah tersimpan. |
| 4 | **Hapus Pemesanan** | Menghapus data pemesanan yang dipilih. |
| 5 | **Keluar** | Mengakhiri program. |

### 1. Tambah Pemesanan (Menu 1)

- Pengguna memasukkan ID pemesanan. Sistem memeriksa format ID dan memastikan ID belum dipakai. Jika sudah dipakai, sistem menampilkan pesan "ID sudah digunakan." dan meminta input ulang.
- Pengguna memasukkan nama penumpang, NIK, dan umur.
- Sistem menampilkan tiga pilihan kapal beserta tujuan, jenis, dan harga tiket. Pengguna memilih salah satu.
- Berdasarkan pilihan, method `buatKapal()` pada controller membuat objek `KapalVIP` (pilihan 1) atau `KapalEkonomi` (pilihan 2 dan 3).
- Pengguna memasukkan jumlah tiket.
- Sistem membuat objek `Penumpang` dan `Pemesanan`, lalu menambahkannya ke `ArrayList` `daftarPemesanan`.
- Sistem menampilkan pesan "Pemesanan berhasil ditambahkan." beserta total harga dari `getTotalHarga()`.

**Pilihan kapal:**

| No. | Kapal | Tujuan | Jenis | Harga | Fasilitas |
|---|---|---|---|---|---|
| 1 | KM Bukit Siguntang | Balikpapan | VIP | Rp150000 | Kabin pribadi |
| 2 | KM Lambelu | Makassar | Ekonomi | Rp200000 | Kursi penumpang |
| 3 | KM Dorolonda | Parepare | Ekonomi | Rp175000 | Kursi penumpang |

### 2. Tampilkan Pemesanan (Menu 2)

- Sistem memeriksa isi `ArrayList` `daftarPemesanan`.
- Jika belum terdapat data, sistem menampilkan pesan "Belum ada data pemesanan."
- Jika terdapat data, sistem menggunakan perulangan `for` untuk mengambil setiap objek `Pemesanan`.
- Sistem menampilkan ID pemesanan, nama penumpang, NIK, umur, informasi kapal, jumlah tiket, dan total harga.
- Informasi kapal ditampilkan melalui method `tampilkanInfo()`. Hasil tampilan berbeda untuk kapal VIP dan Ekonomi (lihat bagian Polymorphism).

### 3. Ubah Pemesanan (Menu 3)

- Pengguna memasukkan ID pemesanan yang ingin diubah.
- Sistem mencari data berdasarkan `idPemesanan` pada `ArrayList`.
- Jika ID ditemukan, pengguna memasukkan data baru berupa nama penumpang, NIK, umur, pilihan kapal, dan jumlah tiket. Semua input baru divalidasi.
- Data `Penumpang` diperbarui menggunakan `setNama()`, `setNik()`, dan `setUmur()`.
- Data kapal dan jumlah tiket pada `Pemesanan` diperbarui menggunakan `setKapal()` dan `setJumlahTiket()`.
- Sistem menampilkan pesan "Data berhasil diubah."
- Jika ID tidak ditemukan, sistem menampilkan pesan "ID Pemesanan tidak ditemukan."

### 4. Hapus Pemesanan (Menu 4)

- Pengguna memasukkan ID pemesanan yang ingin dihapus.
- Sistem mencari data berdasarkan `idPemesanan`.
- Jika ID ditemukan, sistem menampilkan nama penumpang lalu meminta konfirmasi (`1` = Ya, `2` = Tidak).
- Jika pengguna memilih `1`, objek `Pemesanan` dihapus dari `ArrayList` menggunakan `remove()` dan sistem menampilkan "Data berhasil dihapus."
- Jika pengguna memilih `2`, sistem menampilkan "Penghapusan dibatalkan."
- Jika ID tidak ditemukan, sistem menampilkan pesan "ID Pemesanan tidak ditemukan."

### 5. Keluar (Menu 5)

- Pengguna memilih menu **5. Keluar**.
- Sistem menampilkan pesan "Program selesai." dan "Terima kasih."
- Nilai `pilihan` menjadi `5`, sehingga kondisi pada perulangan `do-while` tidak terpenuhi dan program berhenti.

### Cara Kerja Konsep OOP dalam Sistem

**Encapsulation** — Semua atribut kelas (`Kapal`, `KapalVIP`, `KapalEkonomi`, `Penumpang`, `Pemesanan`) bersifat `private`, hanya dapat diakses melalui getter/setter yang di dalamnya juga terdapat validasi (contoh: `setHargaTiket()` menolak nilai ≤ 0).

**Inheritance** — Program memiliki 1 superclass (`Kapal`) dan 2 subclass (`KapalEkonomi`, `KapalVIP`) yang mewarisi atribut dan method superclass menggunakan `extends`, serta memanggil constructor superclass dengan `super(namaKapal, tujuan, hargaTiket)`.

**Polymorphism (Method Overriding)** — Method `tampilkanInfo()` didefinisikan di `Kapal`, lalu di-override di `KapalEkonomi` dan `KapalVIP` agar menampilkan fasilitas sesuai jenis kapal. Pemanggilan `p.getKapal().tampilkanInfo()` pada `PemesananView` otomatis memilih versi method yang sesuai dengan jenis objek sebenarnya saat runtime.

**Validasi Input** — Diterapkan di dua lapisan: pada view (saat mengetik) dan pada setter model (lapisan pengaman data). Input tidak valid akan meminta pengguna mengulang, dan `try-catch` digunakan untuk menangani `NumberFormatException`.

**Dummy Data** — Method `isiDummyData()` dipanggil di constructor `PemesananController` sehingga `ArrayList` sudah berisi 2 data saat program pertama kali dijalankan.

**Struktur MVC** — Program dipisah ke dalam package `model`, `view`, `controller`, dan `main` agar logika data, tampilan, dan alur program tidak tercampur (lihat tabel Struktur Kelas).

---

## 3. Penjelasan Gambar (Screenshot Output)

### Menu Utama

<img width="403" height="238" alt="Screenshot menu utama" src="https://github.com/user-attachments/assets/0bda7e13-9d02-411f-a5cd-a475a39341f4" />

Sistem menampilkan 5 menu utama, yaitu Tambah Pemesanan, Tampilkan Pemesanan, Ubah Pemesanan, Hapus Pemesanan, dan Keluar.

### Tambah Pemesanan

<img width="495" height="571" alt="image" src="https://github.com/user-attachments/assets/c3aec39e-03c5-44d4-bd4f-3f72a6fda8f7" />

Pengguna memasukkan data penumpang, memilih kapal, dan menentukan jumlah tiket. Sistem menyimpan data serta menghitung total harga secara otomatis.

### Tampilkan Pemesanan

<img width="393" height="997" alt="image" src="https://github.com/user-attachments/assets/b6837b5b-68f7-45d7-9151-e1a8bf909c69" />

Data dummy langsung tampil tanpa perlu menambah data terlebih dahulu. Informasi kapal VIP dan Ekonomi ditampilkan dengan fasilitas yang berbeda (hasil dari polymorphism method `tampilkanInfo()`).

### Ubah Pemesanan

<img width="512" height="545" alt="image" src="https://github.com/user-attachments/assets/f470d58c-5cde-4c0e-8a46-ce6e891a78db" />

Pengguna memasukkan ID pemesanan yang ingin diperbarui. Setelah data baru dimasukkan, sistem memperbarui informasi pemesanan dan menampilkan pesan "Data berhasil diubah."

**Output setelah perubahan:**

<img width="412" height="258" alt="image" src="https://github.com/user-attachments/assets/c9ec51dc-a76f-490b-b3fc-0278f00f0a6d" />

### Hapus Pemesanan

<img width="358" height="257" alt="image" src="https://github.com/user-attachments/assets/69bed670-a2fd-4bde-a9ac-f15ce10b6b83" />

Pengguna memasukkan ID pemesanan dan mengonfirmasi penghapusan. Jika pengguna memilih "Ya", sistem menghapus data dari `ArrayList` dan menampilkan pesan "Data berhasil dihapus."

**Output setelah perubahan:**

<img width="436" height="782" alt="image" src="https://github.com/user-attachments/assets/d567e4d3-e13f-4afb-a167-e62530fe79ae" />

### Keluar

<img width="678" height="410" alt="image" src="https://github.com/user-attachments/assets/e96bbc89-6a94-4b55-924d-9572432a0415" />

Pengguna memilih menu Keluar untuk mengakhiri program. Sistem menghentikan perulangan dan menampilkan pesan "Program selesai." dan "Terima kasih."

### Encapsulation — Contoh Atribut `private`

<img width="360" height="125" alt="image" src="https://github.com/user-attachments/assets/d8868de2-a462-4db4-9e51-5f5f921cbecc" />

Atribut pada `model/Kapal.java` bersifat `private` sehingga tidak dapat diakses langsung dari luar class.

**Getter/setter dengan validasi pada `KapalVIP`:**

<img width="705" height="197" alt="image" src="https://github.com/user-attachments/assets/3833dadd-c846-4ba1-9b11-e5971c454637" />

**Getter/setter dengan validasi pada `KapalEkonomi`:**

<img width="773" height="192" alt="image" src="https://github.com/user-attachments/assets/537040b6-d201-40a3-805e-ead19f1467cb" />

### Inheritance — Superclass dan Subclass

<img width="396" height="70" alt="image" src="https://github.com/user-attachments/assets/638afb04-5daf-4078-ad26-aa994e261164" />

`KapalEkonomi` dan `KapalVIP` mewarisi atribut dan method dari `Kapal` menggunakan kata kunci `extends`.

### Validasi Input

**ID Pemesanan** — tidak boleh kosong, harus 3 angka, dan tidak boleh duplikat.

<img width="382" height="128" alt="image" src="https://github.com/user-attachments/assets/557744d3-42f1-402b-916f-6cb00b325ef1" />

**Nama Penumpang** — tidak boleh kosong, hanya huruf dan spasi.

<img width="425" height="130" alt="image" src="https://github.com/user-attachments/assets/9f1ce51c-e3ed-4ee3-8d3b-95a7498e3c4c" />

**NIK** — harus tepat 16 digit dan hanya berisi angka.

<img width="437" height="125" alt="image" src="https://github.com/user-attachments/assets/0e8a59cb-1f21-4885-8267-cf13de718d9c" />

**Umur** — tidak boleh kosong, maksimal 3 digit, harus lebih dari 0.

<img width="307" height="175" alt="image" src="https://github.com/user-attachments/assets/8afa5d18-335e-40bf-b7d6-44b640767a14" />

**Pilihan Kapal** — hanya menerima input 1 sampai 3.

<img width="538" height="435" alt="image" src="https://github.com/user-attachments/assets/05d93148-8d87-4345-ad64-eb514f014339" />

**Jumlah Tiket** — harus berupa angka dan lebih dari 0.

<img width="355" height="48" alt="image" src="https://github.com/user-attachments/assets/a35157f7-bd26-4ba7-9981-7f559be4c448" />

### Dummy Data

<img width="510" height="458" alt="image" src="https://github.com/user-attachments/assets/be1ee4eb-a703-45cc-9756-ed4eda8f3079" />

`isiDummyData()` mengisi `ArrayList` dengan 2 data (ID `101` dan `102`) sejak program pertama kali dijalankan.

### Struktur MVC

<img width="417" height="317" alt="image" src="https://github.com/user-attachments/assets/66d8f145-e3d9-4a9a-a63e-57558b6c1764" />

Program dipisah ke dalam package `model`, `view`, `controller`, dan `main`.

### Polymorphism — Hasil Override `tampilkanInfo()`

**Fasilitas VIP:**

<img width="673" height="142" alt="image" src="https://github.com/user-attachments/assets/b2e9af3d-045a-47e7-bc7f-7f78574d1269" />

**Fasilitas Ekonomi:**

<img width="702" height="141" alt="image" src="https://github.com/user-attachments/assets/bb86fdb9-0372-43e7-91f9-8f67b38e7714" />

Method `tampilkanInfo()` yang dipanggil melalui variabel bertipe `Kapal` (`p.getKapal().tampilkanInfo()`) otomatis menjalankan versi override sesuai objek aslinya (`KapalVIP` atau `KapalEkonomi`) — inilah bentuk polymorphism pada program ini.

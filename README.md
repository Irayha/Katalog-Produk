# Tampilan

<p align="center">
  <img src="assets/Cuplikan layar 2026-11-19 180239.png" alt="Preview Aplikasi " width="350"/>
  

</p>

---


# Katalog Produk 

Aplikasi desktop sederhana berbasis **JavaFX** untuk mengelola katalog produk. Data disimpan di database **SQLite** lokal dan ditampilkan sebagai kartu produk (foto, nama, harga, ID).

## Fitur

- **Tambah** produk (nama, harga, foto)
- **Lihat** katalog dalam bentuk kartu
- **Edit** produk: data dimuat ke form, lalu klik *Perbarui*
- **Hapus** produk dengan dialog konfirmasi
- Validasi input: nama wajib diisi, harga harus angka bulat lebih dari 0, foto wajib dipilih
- Penyimpanan permanen di SQLite (tidak hilang saat aplikasi ditutup)

## Struktur Proyek

```
KatalogProduk/
├── pom.xml
└── src/main/
    ├── java/
    │   ├── main/MainApp.java                    # Entry point aplikasi
    │   ├── model/Produk.java                    # Model + validasi data produk
    │   ├── data/ProdukRepository.java           # Akses data (add, update, delete, getAll)
    │   ├── db/Database.java                     # Koneksi & pembuatan tabel SQLite
    │   └── controller/KatalogController.java    # Logika UI
    └── resources/
        ├── image/                               # Foto produk (roti, susu, kopi)
        └── view/
            ├── katalog.fxml                     # Layout tampilan
            └── styles/app.css                   # Styling
```

## Cara Menjalankan

### Langkah

1. Ekstrak proyek lalu masuk ke folder `KatalogProduk`.
2. Jalankan:

   ```bash
   mvn clean javafx:run
   ```

Bisa juga dibuka lewat IDE (NetBeans, IntelliJ IDEA, atau VS Code) sebagai proyek Maven, lalu jalankan kelas `main.MainApp`.

## Database

- File database dibuat otomatis saat aplikasi pertama kali dijalankan di `data/katalog.db`, relatif terhadap folder tempat aplikasi dijalankan (`user.dir`).
- Lokasi lengkap file database dicetak di konsol dengan awalan `DATABASE AKTIF:`.
- Struktur tabel:

  ```sql
  CREATE TABLE IF NOT EXISTS produk (
      id    INTEGER PRIMARY KEY,
      nama  TEXT    NOT NULL CHECK(length(trim(nama)) > 0),
      harga INTEGER NOT NULL CHECK(harga > 0),
      foto  TEXT    NOT NULL CHECK(length(trim(foto)) > 0)
  );
  ```

- Untuk mengosongkan data, hapus file `data/katalog.db` saat aplikasi tidak berjalan.

## Cara Penggunaan

1. **Tambah produk**: isi *Nama produk*, *Harga (Rp)*, dan pilih *Foto contoh*, lalu klik **Simpan**.
2. **Edit produk**: klik **Edit** pada kartu produk, ubah datanya di form, lalu klik **Perbarui**. Klik **Batal** untuk membatalkan.
3. **Hapus produk**: klik **Hapus** pada kartu produk, lalu konfirmasi dengan **OK**.


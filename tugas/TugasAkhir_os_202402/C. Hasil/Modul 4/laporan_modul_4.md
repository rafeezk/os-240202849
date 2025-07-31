# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi
**Semester**: Genap / Tahun Ajaran 2024–2025
**Nama**: `Ahmad Rafie Ramadhani Azzaki`
**NIM**: `240202849`
**Modul yang Dikerjakan**:
`(Modul 4 – Subsistem Kernel Alternatif (xv6-public))`

---

## 📌 Deskripsi Singkat Tugas
Modul ini bertujuan untuk memperluas subsistem kernel pada sistem operasi `xv6` dengan dua fitur utama:

`System Call chmod(path, mode)` untuk mengatur mode akses file `(read-only atau read-write)`.

`Pseudo-device /dev/random`, sebuah driver sederhana yang menghasilkan byte acak.

Fitur ini membantu memperkenalkan konsep dasar perizinan file dan implementasi driver device di kernel.

## 🛠️ Rincian Implementasi
Menambahkan field short mode pada struct inode di `fs.h` untuk menyimpan mode akses file.

Mengimplementasikan system call `chmod()` di `sysfile.c` untuk mengatur mode file.

Mendaftarkan `chmod()` ke syscall melalui file `syscall.h`, `syscall.c`, `user.h`, dan `usys.S`.

Memodifikasi `file.c` untuk memblokir operasi tulis `(write())` jika inode berada dalam mode read-only.

Membuat program uji `chmodtest.c` untuk memastikan proteksi tulis berjalan.

Membuat driver baru `/dev/random` di file `random.c` menggunakan generator acak berbasis seed.

Mendaftarkan driver random di array `devsw[]` pada `file.c` menggunakan dev major 3.

Menambahkan pembuatan device node `/dev/random` pada `init.c` menggunakan mknod.

Menambahkan program uji `randomtest.c` untuk membaca dan menampilkan byte acak.

Menambahkan dua program tersebut ke Makefile `(_chmodtest, _randomtest)`.

## ✅ Uji Fungsionalitas
Program uji yang digunakan:

`chmodtest`: untuk menguji apakah file read-only tidak bisa ditulis.

`randomtest`: untuk menguji bahwa `/dev/random` menghasilkan byte acak.

## 📷 Hasil Uji
### 📍 Output chmodtest:
nginx
Copy
Edit
Write blocked as expected
### 📍 Output randomtest:
Copy
Edit
241 6 82 99 12 201 44 73
- 📎 Catatan: Output randomtest akan berbeda-beda karena bersifat acak.

## ⚠️ Kendala yang Dihadapi
Lupa mendaftarkan syscall `chmod()` di `syscall.c`, menyebabkan error saat kompilasi.

Lupa memanggil `ilock()` sebelum mengakses inode, menyebabkan `kernel panic`.

Saat pertama menguji `/dev/random`, file tidak ditemukan karena mknod belum ditambahkan di `init.c`.

## 📚 Referensi
xv6 Book (MIT)

xv6-public GitHub Repository

Diskusi praktikum dan dokumentasi kernel xv6

Stack Overflow untuk debugging syscall dan device driver

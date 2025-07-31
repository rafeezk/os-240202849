# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi
**Semester**: Genap / Tahun Ajaran 2024–2025
**Nama**: `Ahmad Rafie Ramadhani Azzaki`
**NIM**: `240202849`
**Modul yang Dikerjakan**:
`(Modul 5 – Audit dan Keamanan Sistem (xv6-public))`

---

## 📌 Deskripsi Singkat Tugas
Modul 5 ini bertujuan untuk menambahkan fitur audit log pada `xv6`. Semua pemanggilan system call akan dicatat ke dalam struktur `audit_log`, dan log ini hanya dapat diakses oleh proses dengan `PID 1` melalui system call baru `get_audit_log()`. Fitur ini penting untuk keamanan dan analisis aktivitas sistem.

## 🛠️ Rincian Implementasi
Berikut langkah-langkah implementasi yang saya lakukan:

Menambahkan struktur `audit_entry` dan array `audit_log[]` di `syscall.c`.

Memodifikasi fungsi `syscall()` untuk mencatat setiap pemanggilan system call yang valid.

Menambahkan system call baru `get_audit_log()` di:

`syscall.h` (penambahan nomor syscall)

`user.h` dan `usys.S` (deklarasi syscall)

`sysproc.c` (implementasi syscall dengan validasi PID)

`syscall.c` (pendaftaran syscall)

Menambahkan file program uji audit.c untuk mengambil dan menampilkan isi audit log.

Menambahkan `_audit` ke dalam target `UPROGS` di Makefile.

## ✅ Uji Fungsionalitas
Program uji yang digunakan:

`audit`: Menampilkan isi audit log.

Jika dijalankan sebagai proses biasa (bukan PID 1), maka akan ditolak.

Jika dijalankan oleh `PID 1` (sebagai init), maka isi audit log akan ditampilkan.

Untuk pengujian, file `init.c` dimodifikasi agar menjalankan audit secara langsung, sehingga audit menjadi proses dengan `PID 1`.

## 📷 Hasil Uji
### 📍 Contoh Output saat audit dijalankan sebagai `PID 1`:

csharp
Copy
Edit
=== Audit Log ===
[0] PID=1 SYSCALL=5 TICK=12
[1] PID=1 SYSCALL=6 TICK=13
[2] PID=1 SYSCALL=10 TICK=14
...
### 📍 Contoh Output saat dijalankan sebagai proses biasa:

nginx
Copy
Edit
Access denied or error.
Jika ada dokumentasi visual:

scss
Copy
Edit
![hasil audit](./screenshots/audit_output.png)

## 📸 Screenshoot

<img width="727" height="313" alt="modul5" src="https://github.com/user-attachments/assets/d73bb4a5-f7f6-496c-8622-a05f5353e37f" />

## ⚠️ Kendala yang Dihadapi
Awalnya lupa menambahkan validasi `PID` pada `sys_get_audit_log()`, sehingga semua proses dapat mengakses audit log.

Salah alokasi pointer buf di `syscall` menyebabkan kernel panic ketika proses non-init mencoba memanggil `get_audit_log`.

Harus memodifikasi `init.c` untuk menjadikan audit sebagai proses `PID 1` agar uji berhasil.

## 📚 Referensi
Buku xv6 MIT: xv6 book (rev11)

xv6-public GitHub: https://github.com/mit-pdos/xv6-public

Dokumentasi praktikum Sistem Operasi Fasilkom

Diskusi rekan praktikum dan Stack Overflow
---


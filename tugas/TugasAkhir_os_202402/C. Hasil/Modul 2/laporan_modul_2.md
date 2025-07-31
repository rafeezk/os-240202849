# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi
**Semester**: Genap / Tahun Ajaran 2024–2025
**Nama**: `Ahmad Rafie Ramadhani Azzaki`
**NIM**: `240202849`
**Modul yang Dikerjakan**:
`(Modul 2 — Penjadwalan CPU Lanjutan (Priority Scheduling Non-Preemptive))`

---

## 📌 Deskripsi Singkat Tugas
Modul 2 – Penjadwalan CPU Lanjutan `(Priority Scheduling Non-Preemptive)`:
Mengubah algoritma penjadwalan proses default Round Robin pada xv6 menjadi algoritma Priority Scheduling Non-Preemptive. Proses dengan prioritas numerik terkecil dijalankan lebih dahulu, dan proses lain menunggu meskipun sudah dalam status RUNNABLE.

## 🛠️ Rincian Implementasi
Menambahkan field priority pada struct proc di `proc.h`

Menginisialisasi nilai default priority = 60 di `allocproc()` pada `proc.c`

Membuat system call baru `set_priority(int)`:

Menambahkan nomor syscall di `syscall.h`

Mendeklarasikan fungsi di `user.h`

Menambahkan entri syscall di `usys.S` dan `syscall.c`

Mengimplementasikan fungsi syscall `sys_set_priority()` di `sysproc.c`

Memodifikasi fungsi `scheduler()` di `proc.c` agar memilih proses RUNNABLE dengan prioritas tertinggi (angka terkecil)

Membuat program uji `ptest.c` untuk menguji urutan eksekusi berdasarkan prioritas

Menambahkan ptest ke dalam Makefile agar dapat dieksekusi dari shell xv6

## ✅ Uji Fungsionalitas
Program uji:

`ptest`: menguji sistem dengan dua proses child berprioritas berbeda.

Child 2 memiliki prioritas 10

Child 1 memiliki prioritas 90

Hasil yang diharapkan: Child 2 selesai lebih dulu karena prioritas lebih tinggi.

## 📷 Hasil Uji
### 📍 Output dari program ptest:
nginx
Copy
Edit
Child 2 selesai
Child 1 selesai
Parent selesai
Hasil menunjukkan bahwa proses dengan prioritas lebih tinggi (angka lebih kecil) dieksekusi terlebih dahulu, sesuai dengan mekanisme Non-Preemptive Priority Scheduling.

## 📸 Screenshoot
<img width="712" height="375" alt="modul2" src="https://github.com/user-attachments/assets/374ba036-ac3f-4a6b-a055-e052a8d673ea" />

## ⚠️ Kendala yang Dihadapi
Awalnya lupa menginisialisasi nilai priority di `allocproc()` menyebabkan proses memiliki nilai sampah dan scheduler tidak bekerja dengan benar.

Salah urutan dalam menulis syscall menyebabkan error linking karena `set_priority` tidak dikenali oleh user space.

Debugging scheduler cukup sulit karena tidak ada output langsung; harus diuji menggunakan program eksplisit seperti `ptest`.

## 📚 Referensi
Buku xv6 (MIT): https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf

Repositori xv6-public: https://github.com/mit-pdos/xv6-public

Dokumentasi dan slide praktikum Sistem Operasi 2024–2025

Stack Overflow dan diskusi GitHub terkait scheduler xv6
* Stack Overflow, GitHub Issues, diskusi praktikum

---


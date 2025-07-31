# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi
**Semester**: Genap / Tahun Ajaran 2024–2025
**Nama**: `Ahmad Rafie Ramadhani Azzaki`
**NIM**: `240202849`
**Modul yang Dikerjakan**:
`(Modul 3 — Manajemen Memori Tingkat Lanjut (xv6-public x86))`

---

## 📌 Deskripsi Singkat Tugas
Pada modul ini, saya mengimplementasikan dua fitur utama dalam manajemen memori sistem operasi:

`Copy-on-Write (CoW)` pada `fork()`, agar proses anak hanya menyalin halaman memori saat menulis `(write)`.

`Shared Memory (System V style)` melalui dua system call baru: `shmget(int key)` dan `shmrelease(int key)` untuk berbagi memori antar proses.

## 🛠️ Rincian Implementasi
1. Copy-on-Write Fork
Menambahkan array `ref_count[]` di `vm.c` untuk mencatat referensi tiap halaman fisik.

Menambahkan flag `PTE_COW` di `mmu.h` untuk menandai halaman Copy-on-Write.

Mengganti fungsi `copyuvm()` menjadi `cowuvm()` di `vm.c` agar anak dan induk berbagi halaman read-only.

Menangani page fault di `trap.c` untuk menyalin halaman secara fisik hanya saat proses mencoba menulis.

Mengubah `fork()` di `proc.c` agar menggunakan `cowuvm()`.

2. Shared Memory ala System V
Menambahkan array `shmtab[]` di `vm.c` untuk menyimpan key, frame, dan refcount.

Mengimplementasikan `sys_shmget()` dan `sys_shmrelease()` di `sysproc.c`.

Menambahkan system call `shmget()` dan `shmrelease()`:

Registrasi di `syscall.c`, `syscall.h`, `usys.S`, dan `user.h`.

## ✅ Uji Fungsionalitas
Program uji yang digunakan:

`cowtest.c`: Menguji fungsi `fork()` dan memori `CoW`.

`shmtest.c`: Menguji penggunaan shared memory antar proses.

## 📷 Hasil Uji
### 📍 Output `cowtest.c`
yaml
Copy
Edit
Child sees: Y
Parent sees: X
Hasil menunjukkan bahwa proses anak menulis ke salinan memorinya sendiri (halaman disalin karena CoW).

### 📍 Output shmtest.c
less
Copy
Edit
Child reads: A
Parent reads: B
Menunjukkan bahwa halaman shared memory berhasil diakses bersama dan perubahan dari anak terlihat di induk.

## 📸 Screenshoot

<img width="1145" height="348" alt="modul3(1)" src="https://github.com/user-attachments/assets/66a8500c-e19c-42a5-9dff-deb092259aa0" />

<img width="1142" height="426" alt="modul3(2)" src="https://github.com/user-attachments/assets/562e5818-5746-44c8-9628-bc79a1343450" />

## ⚠️ Kendala yang Dihadapi
Debugging page fault cukup rumit karena perlu mengecek flag `PTE_COW`, validitas `PTE`, dan alokasi `kalloc()` yang bisa gagal.

Lupa memanggil `decref()` saat halaman ditimpa menyebabkan memory leak.

Salah pemetaan alamat shared memory menyebabkan overwrite memori stack.

📚 Referensi
Buku xv6 MIT (rev11)

Repositori xv6-public GitHub

Diskusi praktikum dan Stack Overflow

# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi
**Semester**: Genap / Tahun Ajaran 2024–2025
**Nama**: `Ahmad Rafie Ramadhani Azzaki`
**NIM**: `240202849`
**Modul yang Dikerjakan**:
`(Modul 1 – System Call dan Instrumentasi Kernel)`

---

📌 Deskripsi Singkat Tugas
Modul ini mengharuskan mahasiswa untuk menambahkan dua system call baru pada kernel xv6-public (x86), yaitu:

getpinfo(struct pinfo *ptable): Untuk mendapatkan informasi semua proses aktif dalam sistem.

getreadcount(): Untuk menghitung jumlah pemanggilan read() sejak sistem boot.

🛠️ Rincian Implementasi
Langkah-langkah implementasi:

Menambahkan struktur pinfo di proc.h untuk menyimpan daftar proses aktif.

Menambahkan counter global readcount di sysproc.c.

Menambahkan definisi syscall baru di syscall.h, syscall.c, user.h, dan usys.S.

Mengimplementasikan fungsi sys_getpinfo() dan sys_getreadcount() di sysproc.c.

Menambahkan readcount++ di awal fungsi sys_read() pada sysfile.c.

Membuat dua program uji ptest.c dan rtest.c untuk menguji fungsi yang telah ditambahkan.

Mendaftarkan program uji ke dalam Makefile.

✅ Uji Fungsionalitas
Program uji yang digunakan:

ptest: Menguji apakah system call getpinfo() dapat mengambil informasi proses aktif.

rtest: Menguji apakah getreadcount() dapat menghitung jumlah pemanggilan fungsi read().

📷 Hasil Uji
📍 Contoh Output ptest:
yaml
Copy
Edit
PID	MEM	NAME
1	4096	init
2	2048	sh
3	2048	ptest
📍 Contoh Output rtest:
mathematica
Copy
Edit
Read Count Sebelum: 4
hello
Read Count Setelah: 5

📸 Screenshoot
<img width="802" height="367" alt="modul1" src="https://github.com/user-attachments/assets/aa85da42-ed05-45f5-ad71-d83992a9fced" />

⚠️ Kendala yang Dihadapi
Awalnya sempat salah dalam implementasi argptr() di sys_getpinfo, sehingga pointer ptable tidak dapat diakses kernel.

Kesalahan kecil saat menambahkan entri di Makefile menyebabkan program ptest tidak dikenali sampai file Makefile diperbaiki.

Kernel panic terjadi ketika membaca pointer user-space yang tidak valid.

📚 Referensi
Buku xv6 (MIT): https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf

Repositori xv6: https://github.com/mit-pdos/xv6-public

Diskusi dan dokumentasi praktikum dari asisten

Stack Overflow untuk debugging pointer syscall

Dokumentasi argptr() dan sistem memory kernel-user space dalam xv6public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---


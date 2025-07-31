# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi
**Semester**: Genap / Tahun Ajaran 2024–2025
**Nama**: `<Hanifah>`
**NIM**: `<240202864>`
**Modul yang Dikerjakan**:
`(Modul 1 – System Call dan Instrumentasi Kernel)`

---

## 📌 Deskripsi Singkat Tugas
* **Modul 1 – System Call dan Instrumentasi Kernel**:
System Call
System Call adalah antarmuka (interface) yang digunakan oleh program aplikasi untuk berkomunikasi dengan kernel sistem operasi. Melalui system call, program dapat meminta layanan penting seperti akses file, manajemen proses, komunikasi antar proses, dan penggunaan perangkat keras. Contohnya termasuk read(), write(), fork(), dan exec(). System call menjembatani kebutuhan program user-space dengan fungsi-fungsi inti sistem di kernel-space.
Instrumentasi Kernel
Instrumentasi kernel adalah proses menambahkan kode atau alat bantu untuk memantau, menganalisis, dan mencatat aktivitas di dalam kernel. Tujuannya adalah untuk debugging, profiling performa, dan pengawasan keamanan. Dengan instrumentasi, pengembang dapat mengetahui bagaimana kernel menangani system call, manajemen memori, atau scheduling. Contoh alat instrumentasi meliputi ftrace, perf, SystemTap, dan eBPF

---
## 🛠️ Rincian Implementasi

* Menambahkan dua system call baru di file `sysproc.c` dan `syscall.c`
* Mengedit `user.h`, `usys.S`, dan `syscall.h` untuk mendaftarkan syscall
* Menambahkan struktur `struct pinfo` di `proc.h`
* Menambahkan counter `readcount` di kernel
* Membuat dua program uji: `ptest.c` dan `rtest.c`
---

## ✅ Uji Fungsionalitas


* `ptest`: untuk menguji `getpinfo()`
* `rtest`: untuk menguji `getReadCount()`

---

## 📷 Hasil Uji


### 📍 Output `ptest`:

```
$ ptest  
PID     MEM     NAME  
1       12288   init  
2       16384   sh  
3       12288   ptest
```

### 📍 Output `rtest`:

```
$ rtest  
Read Count Sebelum: 12  
hello  
Read Count Setelah: 13  
$ $   
```

Jika ada screenshot:

<img width="1366" height="768" alt="OS Modul 1" src="https://github.com/user-attachments/assets/a598a199-8389-43b8-bdab-f414a9cdd8f5" />



---

## ⚠️ Kendala yang Dihadapi


* Salah implementasi `page fault` menyebabkan panic
* Salah memetakan alamat shared memory ke USERTOP
* Proses biasa bisa akses audit log (belum ada validasi PID)

---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---

# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi
**Semester**: Genap / Tahun Ajaran 2024–2025
**Nama**: `<Hanifah>`
**NIM**: `<240202864>`
**Modul yang Dikerjakan**:
`(Modul 3 — Manajemen Memori Tingkat Lanjut (xv6-public x86))`

---

## 📌 Deskripsi Singkat Tugas

* **Modul 3 — Manajemen Memori Tingkat Lanjut (xv6-public x86)**:  
  Manajemen memori tingkat lanjut dalam xv6-public mencakup berbagai teknik pengelolaan memori yang digunakan untuk meningkatkan efisiensi, keamanan, dan isolasi antar proses. Meskipun xv6 adalah sistem operasi pembelajaran yang sederhana, banyak konsep inti dari sistem operasi modern tetap diimplementasikan.
---

## 🛠️ Rincian Implementasi

### Modul 3:
Copy-on-Write Fork

*Menambahkan fungsi baru cowuvm() di vm.c untuk membuat page table dengan halaman read-only bersama.  
*Memodifikasi fork() di proc.c untuk memanggil cowuvm() alih-alih copyuvm().  
*Menambahkan penanganan page fault di trap.c untuk mendeteksi penulisan ke halaman read-only, lalu melakukan salin halaman (copy-on-write).  
*Menambahkan bit PTE_COW di mmu.h untuk menandai halaman copy-on-write.  
*Memodifikasi freevm() dan reference count untuk mendukung halaman bersama.  

Shared Memory

*Mendefinisikan MAX_SHM di param.h dan membuat tabel global shmtab untuk menyimpan informasi shared memory.  
*Menambahkan deklarasi dan implementasi sys_shmget() dan sys_shmrelease() di sysproc.c.  
*Memanggil mappages() untuk memetakan frame shared memory ke alamat virtual di dekat USERTOP.  
*Menambahkan prototipe fungsi di defs.h dan memastikan myproc() digunakan alih-alih variabel proc.  
*Mendefinisikan USERTOP di memlayout.h.  
---

## ✅ Uji Fungsionalitas

Program uji yang digunakan:

*cowtest — menguji apakah fork() tidak langsung menyalin memori, tapi baru menyalin saat ada penulisan.
*shmtest — menguji apakah dua proses dapat berbagi segmen memori yang sama melalui shmget() dan shmrelease().


---

## 📷 Hasil Uji

### 📍 Output `cowtest`:

```
Child sees: Y
Parent sees: X
```

### 📍  Output `shmtest`:

```
Child reads: A
Parent reads: B
```

Jika ada screenshot:

<img width="983" height="381" alt="OS Modul 3A" src="https://github.com/user-attachments/assets/ebf2d8c2-8f76-42b0-816b-3d41b6d4e528" />

<img width="1017" height="355" alt="OS Modul 3B" src="https://github.com/user-attachments/assets/c3921809-8b01-425a-9e22-39863a6bc03f" />


---

## ⚠️ Kendala yang Dihadapi

*cowuvm awalnya tidak dikenali karena salah penempatan deklarasi (harus di defs.h).  
*Error proc undeclared di sysproc.c karena harus menggunakan myproc() bukan variabel global proc.  
*USERTOP belum didefinisikan sehingga harus ditambahkan di memlayout.h.  
*Beberapa error kompiler karena MAX_SHM dan shmtab belum dideklarasikan di file header yang tepat.  
*Penanganan page fault harus hati-hati agar tidak memicu panic kernel.  


---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---


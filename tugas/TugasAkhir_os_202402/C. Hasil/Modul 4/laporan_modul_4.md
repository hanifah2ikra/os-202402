# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi
**Semester**: Genap / Tahun Ajaran 2024–2025
**Nama**: `<Hanifah>`
**NIM**: `<240202864>`
**Modul yang Dikerjakan**:
`Modul 4 – Subsistem Kernel Alternatif (xv6-public)`

---

## 📌 Deskripsi Singkat Tugas

* **Modul 4 – Subsistem Kernel Alternatif (xv6-public)**:
 Subsistem kernel alternatif dalam xv6-public merujuk pada bagian-bagian modular dari kernel yang dapat dimodifikasi, diperluas, atau diganti untuk mengeksplorasi berbagai konsep sistem operasi. Meskipun xv6 adalah sistem sederhana, ia tetap memiliki subsistem inti seperti:

- Manajemen Proses (Process Management) : Menangani pembuatan (fork), terminasi (exit), penjadwalan, dan status proses.  
- Manajemen Memori (Memory Management) : Menyediakan virtual memory, alokasi/dealokasi halaman, dan translasi alamat.  
- Sistem Berkas (File System) : Sistem file berbasis inode yang mendukung file, direktori, dan pipe.  
- Sistem Call Interface : Jembatan antara program user dan layanan kernel.  
- Penjadwalan CPU (Scheduler): Awalnya menggunakan round-robin, namun dapat dimodifikasi (misalnya menjadi priority scheduling).  

Dengan membuka dan memodifikasi subsistem ini, pengguna dapat membangun alternatif subsistem kernel seperti:
-Scheduler berbasis priority, multilevel queue, atau lottery scheduling  
-Sistem memori dengan Copy-on-Write, paging, atau memory swapping  
-Mekanisme interupsi dan interrupt handling yang lebih kompleks  
-Sistem file alternatif yang mendukung fitur baru seperti journaling atau permission  


---

## 🛠️ Rincian Implementasi

### Modul 4:

1. system call chmod(path, mode) Untuk menguji kemampuan membatasi akses tulis pada file, dilakukan modifikasi agar file bisa dibuat tidak bisa ditulis dengan syscall chmod(). 🔧 Modifikasi File:

-sysfile.c: Menambahkan syscall sys_chmod() untuk mengatur writable flag pada inode.  
-fs.c: Fungsi writei() diperbarui supaya menolak penulisan jika inode tidak writable.  
-file.c: Memastikan filewrite() menggunakan logika write blocking dari writei().  
-user.h: Mendeklarasikan prototipe chmod() agar dapat dipanggil dari user-space.  
-usys.S: Menambahkan entri syscall chmod agar dapat dipanggil dari program user.  
-syscall.c: Menambahkan entri syscall SYS_chmod ke dalam array syscalls[].  
-syscall.h: Menambahkan #define SYS_chmod untuk syscall nomor baru.  
-defs.h: Menambahkan deklarasi fungsi sys_chmod() agar bisa dipanggil kernel internal.  
-fs.h: Menambahkan field baru pada struktur inode untuk menyimpan status writable.  
-sleeplock.h dan spinlock.h dimodifikasi dengan penambahan header guard untuk mencegah duplikasi saat kompilasi dan menjaga kestabilan sistem saat file digunakan di berbagai bagian kernel.  
-chmodtest.c: Program pengujian untuk membuat file, mengubah statusnya menjadi read-only, dan mencoba menulis ke file tersebut.  
-Pada chmodtest.c, ditambahkan baris printf(1, "hallo\n"); sebagai indikator awal bahwa program berhasil dieksekusi sebelum melakukan pengujian menggunakan syscall chmod().  
-Mendaftarkan program uji ke Makefile  

2. Device Acak (/dev/random) Fitur ini menambahkan device khusus bernama /dev/random yang menghasilkan byte acak saat dibaca,yang menyerupai fungsi random device pada sistem Linux. 🔧 Modifikasi File:

-random.c: Menyediakan fungsi randomread() untuk menghasilkan angka acak.  
-fs.c dan file.c: Menghubungkan device /dev/random lewat array devsw[] agar saat dibaca, sistem tahu harus menjalankan fungsi randomread() untuk menghasilkan angka acak.  
-sysfile.c: Mendukung pembuatan device /dev/random melalui mknod().  
-defs.h: Menambahkan deklarasi fungsi diskwrite, diskread, dan randomread untuk mendukung implementasi device /dev/random  
-init.c: Menambahkan perintah mknod("/dev/random", 1, 3); supaya device dibuat otomatis ketika boot.  
-randomtest.c: Program pengujian yang membaca angka acak dari /dev/random dan menampilkannya.  
-Mendaftarkan program uji ke Makefile  
---

## ✅ Uji Fungsionalitas

*chmodtest: untuk memastikan file read-only tidak bisa ditulis.  
*randomtest: untuk menguji apakah pembacaan dari device /dev/random menghasilkan angka acak seperti yang diharapkan.

---

## 📷 Hasil Uji

### 📍  Output `chmodtest`:

```
$ chmodtest
Write blocked as expected
```

### 📍 Output `randomtest`:

```
$ randomtest
Silakan ketik sesuatu: hello
Kamu mengetik: hello

104 101 108 108 111 10 0 0 
$ 
```

Jika ada screenshot:

![OS Modul 4](https://github.com/user-attachments/assets/836b0c74-b6a4-45c6-b1f3-b4f202329314)


---

## ⚠️ Kendala yang Dihadapi

* Salah menambahkan validasi write protection di writei() sehingga file read-only masih bisa ditulisi.
* Tidak melakukan pengecekan return value dari write() di chmodtest.c sehingga error tidak terdeteksi saat penulisan ditolak.
* Lupa mendaftarkan system call chmod di syscall.c, syscall.h, dan usys.S sehingga system call tidak dikenal saat runtime.
* Tidak menambahkan perintah mknod("/dev/random", 1, 3); di init.c menyebabkan device /dev/random tidak tersedia saat booting.
* Tidak mendaftarkan randomread ke devsw[] pada file.c menyebabkan pembacaan /dev/random tidak memanggil fungsi yang benar.
* Lupa mendeklarasikan randomread() di fs.h dan defs.h sehingga menyebabkan error saat linking.

---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---


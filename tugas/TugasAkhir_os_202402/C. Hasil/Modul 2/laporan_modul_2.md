# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi
**Semester**: Genap / Tahun Ajaran 2024–2025
**Nama**: `<Hanifah>`
**NIM**: `<240202864>`
**Modul yang Dikerjakan**:
`(Modul 2 — Penjadwalan CPU Lanjutan (Priority Scheduling Non-Preemptive))`

---

## 📌 Deskripsi Singkat Tugas

* **Modul 2 — Penjadwalan CPU Lanjutan (Priority Scheduling Non-Preemptive) **:
Priority Scheduling Non-Preemptive
Priority Scheduling Non-Preemptive adalah algoritma penjadwalan CPU di mana setiap proses diberikan prioritas, dan CPU akan dijalankan oleh proses dengan prioritas tertinggi yang tersedia. Dalam versi non-preemptive, setelah sebuah proses sudah mendapatkan CPU, proses tersebut akan terus berjalan hingga selesai, tanpa bisa diinterupsi oleh proses lain yang mungkin memiliki prioritas lebih tinggi.

## 🛠️ Rincian Implementasi

Tuliskan secara ringkas namun jelas apa yang Anda lakukan:

### Contoh untuk Modul 2:

*mengubah algoritma penjadwalan xv6 menjadi non-preemptive priority scheduling
*Telah menambahkan satu syscall baru: set_priority()
*Menyesuaikan struktur kernel, user API, dan scheduler
*Sistem menjadi lebih deterministik, namun dengan risiko starvation
---

## ✅ Uji Fungsionalitas

*ptest.c untuk menguji apakah proses dengan prioritas lebih tinggi dieksekusi lebih dulu. Child 2 diberi prioritas 0, Child 1 prioritas 10.

---

## 📷 Hasil Uji

### 📍 Contoh Output `ptest`:

```
$ ptest
Child 2 selesai
Child 1 selesai
Parent selesai
$ 
```

Jika ada screenshot:

<img width="1366" height="768" alt="OS Modul 2" src="https://github.com/user-attachments/assets/00182c6c-1c74-45ed-a003-1ba8226359e2" />


---

## ⚠️ Kendala yang Dihadapi

Tuliskan kendala (jika ada), misalnya:

* Sering salah meletakkan program
* Awalnya output menunjukkan urutan proses tidak sesuai prioritas karena delay sleep() belum diatur dengan benar untuk menghindari tabrakan antar proses.

---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---


# Sejarah dan Evolusi Sistem Operasi

## Sistem Komputer Didedikasikan

Pada awal perkembangan komputer, sistem komputer dirancang untuk tujuan tertentu dan digunakan secara eksklusif. Seiring waktu, berbagai perangkat keras dan perangkat lunak tambahan mulai dikembangkan untuk meningkatkan efisiensi dan fungsionalitas.

### Pengembangan Perangkat Keras
Beberapa perangkat keras penting yang mulai digunakan meliputi:

- Pembaca kartu
- Printer baris
- Pita magnetik

### Pengembangan Perangkat Lunak
**Assembler, Loader, dan Linker**

Perangkat lunak seperti assembler, loader, dan linker membantu menyusun dan memuat program ke dalam memori komputer secara lebih efisien.

**Perpustakaan Fungsi Umum**

Perpustakaan fungsi umum memungkinkan pemrogram untuk:

- Menggunakan kembali kode tanpa harus menulis ulang dari awal
- Meningkatkan efisiensi dan konsistensi pengembangan perangkat lunak

### Driver Perangkat

Driver perangkat sangat penting untuk menangani operasi I/O (input/output), karena setiap perangkat memiliki karakteristik unik yang memerlukan pemrograman khusus.

**Karakteristik Driver Perangkat:**
- Subrutin khusus ditulis untuk setiap perangkat I/O
- Menangani elemen penting seperti buffer, flag, register, serta bit kontrol dan status
- Mempermudah operasi seperti membaca karakter dari pembaca pita kertas

### Kompiler dan Bahasa Pemrograman

Munculnya kompiler untuk bahasa pemrograman seperti FORTRAN dan COBOL membuat pemrograman menjadi lebih mudah, meskipun meningkatkan kompleksitas sistem secara keseluruhan.

**Proses Menjalankan Program FORTRAN:**
1. Memuat kompiler FORTRAN dari pita magnetik
2. Membaca program dari kartu dan menulisnya ke pita lain
3. Mengkompilasi menjadi bahasa assembly
4. Menggunakan assembler untuk menghasilkan kode mesin
5. Melakukan linking dengan rutin dari perpustakaan
6. Menghasilkan bentuk biner yang siap dijalankan
7. Memuat program ke memori dan melakukan debugging dari konsol
   
## Sistem Komputer Bersama

Dengan meningkatnya kompleksitas sistem komputer, diperlukan pendekatan baru dalam pengoperasiannya.

### Operator Profesional

Solusi awal adalah dengan mempekerjakan operator komputer untuk mengelola proses:

**Manfaat:**
- Programmer tidak lagi mengoperasikan mesin secara langsung
- Operator dapat langsung memulai pekerjaan berikutnya setelah satu selesai
- Proses setup menjadi lebih cepat dan efisien

**Keterbatasan:**
- Operator tidak dapat melakukan debugging program yang error
- Debugging dilakukan berdasarkan dump memori dan register
- Proses ini membuat debugging menjadi lebih sulit bagi programmer

### Sistem Batch

Solusi berikutnya adalah mengelompokkan pekerjaan sejenis ke dalam batch untuk mengurangi waktu setup.

**Contoh:**
Jika operator menerima urutan pekerjaan: FORTRAN → COBOL → FORTRAN, maka akan lebih efisien jika kedua pekerjaan FORTRAN dijalankan berurutan sebagai satu batch. Ini mengurangi kebutuhan untuk memuat ulang lingkungan FORTRAN, sehingga menghemat waktu setup.

## Sistem Operasi Bersejarah

### Sistem Atlas

Dikembangkan di Universitas Manchester (akhir 1950-an hingga awal 1960-an), Atlas adalah salah satu sistem operasi paling inovatif pada masanya.

#### Fitur Utama Atlas
- Menyediakan fitur yang kini menjadi standar sistem operasi modern
- Driver perangkat menjadi komponen penting
- Panggilan sistem melalui instruksi khusus (kode tambahan)
- Sistem batch dengan spooling

**Spooling:**
Memungkinkan penjadwalan pekerjaan sesuai ketersediaan perangkat periferal seperti:

- Pita magnetik
- Pembaca dan pukulan pita kertas
- Printer baris
- Pembaca dan pukulan kartu

#### Manajemen Memori Atlas
- Menggunakan **drum** sebagai memori utama
- **Memori inti** kecil digunakan sebagai cache
- Menerapkan **demand paging** untuk memindahkan data antara memori inti dan drum secara otomatis

### Sistem XDS-940

Dikembangkan di Universitas California, Berkeley pada awal 1960-an, sistem ini memiliki pendekatan berbeda dari Atlas.

#### Fitur Utama
- Menggunakan **paging** untuk manajemen memori
- Mendukung **time-sharing**, memungkinkan banyak pengguna menggunakan sistem secara bersamaan

#### Manajemen Memori
- Paging digunakan untuk **relokasi**, bukan demand paging
- Memori virtual per proses: **16-KB kata**
- Memori fisik: **64-KB kata**
- Setiap halaman terdiri dari **2-KB kata**
- Tabel halaman disimpan dalam register
- Memori fisik yang lebih besar memungkinkan beberapa proses berjalan secara simultan

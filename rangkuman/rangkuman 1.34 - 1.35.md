## 1.	PROSES TRANSISI ANTARA MODE PENGGUNA DAN MODE KERNEL DALAM SISTEM:
### a. Timer
Digunakan untuk mencegah loop tak terbatas dan mencegah proses memonopoli sumber daya dengan menghentikan proses yang berjalan terlalu lama.

### b. Interupsi Waktu
Timer diatur untuk menghitung mundur berdasarkan jam fisik dan, ketika penghitung mencapai nol, menghasilkan interupsi. Hal ini memungkinkan sistem operasi untuk mendapatkan kembali kendali atas proses.

### c. Pengaturan Proses
Dengan melakukan interupsi, sistem operasi dapat menghentikan proses yang melebihi waktu yang dialokasikan atau menjadwalkan proses lain, sehingga menjaga kestabilan dan efisiensi sistem.

## 2.	MANAJEMEN PROSES
### a. Definisi Proses
Sebuah proses adalah program yang sedang dieksekusi. Meskipun program adalah entitas pasif, proses merupakan entitas aktif yang menjalankan tugas tertentu di dalam sistem.

### b. Kebutuhan Sumber Daya
Untuk menyelesaikan tugasnya, suatu 	memerlukan berbagai sumber daya seperti CPU, memori, perangkat /O, file, serta data inisialisasi.

### c. Terminasi Proses
Saat sebuah proses selesai, sumber daya yang telah digunakan harus dikembalikan (direklamasi) agar dapat dipakai kembali oleh proses lain.

### d. Eksekusi Proses
#### -Single-threaded Process: Proses dengan satu utas memiliki satu program counter yang menunjuk ke instruksi berikutnya secara berurutan hingga semua instruksi selesai.


#### -Multi-threaded Process: Proses dengan banyak utas memiliki program counter masing-masing, memungkinkan eksekusi beberapa utas secara bersamaan.

## 3.	AKTIFITAS MANAJEMEN PROSES
### a. Pembuatan dan Penghapusan Proses
Sistem operasi bertanggung jawab membuat dan menghapus proses untuk pengguna dan sistem.

### b. Penangguhan dan Pelanjutan Proses
Proses dapat ditangguhkan dan dilanjutkan sesuai kebutuhan.

### c. Sinkronisasi Proses
Sistem operasi menyediakan mekanisme untuk menjaga koordinasi antar proses.

### d. Komunikasi Proses
Mekanisme komunikasi antar proses disediakan agar proses dapat saling bertukar data.

## 4.	MANAJEMEN MEMORI
### a. Untuk menjalankan program, instruksi dan data yang diperlukan harus ada di memori.

### b. Manajemen memori mengatur apa yang berada di memori dan kapan.

### c. Tujuannya adalah mengoptimalkan pemanfaatan CPU dan meningkatkan respons sistem.

### d. Aktivitasnya mencakup pelacakan penggunaan memori, pemindahan data/proses antara memori dan penyimpanan, serta alokasi dan dealokasi ruang memori sesuai kebutuhan.

## 5.	MANAJEMEN FILE-SISTEM
### a. Abstraksi Penyimpanan
Sistem operasi mengubah properti fisik perangkat penyimpanan (seperti disk drive dan tape drive) menjadi unit logis yang disebut file.

### b. Karakteristik Perangkat
Tiap perangkat memiliki kecepatan akses, kapasitas, laju transfer data, dan metode akses (sekuensial atau acak).

### c. Pengorganisasian File
File biasanya diatur ke dalam direktori dan dilengkapi dengan kontrol akses agar hanya pihak tertentu yang dapat mengaksesnya.

## 6.	MANAJEMEN PENYIMPANAN MASSAL
### a. Penyimpanan Data
Disk digunakan untuk menyimpan data yang tidak muat di memori utama atau untuk jangka panjang.

### b. Pentingnya Manajemen
Pengelolaan yang tepat sangat krusial, karena kecepatan operasi komputer bergantung pada kinerja subsistem disk.

### c. Aktivitas OS
Meliputi mounting/unmounting, pengelolaan ruang kosong, alokasi penyimpanan, penjadwalan disk, partisi, dan perlindungan.

## 7.	CACHING
### a. Prinsip Dasar
Caching adalah proses menyalin data yang sedang digunakan dari penyimpanan yang lebih lambat ke penyimpanan yang lebih cepat secara sementara.

### b. Penerapan Berlapis
Prinsip ini diterapkan pada berbagai level komputer, termasuk di perangkat keras, sistem operasi, dan perangkat lunak.

### c. Mekanisme Operasi
Saat data dibutuhkan, sistem pertama-tama memeriksa cache. Jika data sudah ada di sana, data diakses secara langsung dengan cepat. Jika tidak ada, data disalin ke cache dan kemudian digunakan.

### d. Ukuran dan Manajemen
Cache memiliki kapasitas yang lebih kecil dibandingkan penyimpanan utamanya, sehingga kebijakan penggantian dan manajemen ukuran cache menjadi aspek penting dalam desain sistem.

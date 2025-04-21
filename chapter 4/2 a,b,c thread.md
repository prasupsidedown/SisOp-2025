# Programming Exercise

## a. Penerapan Thread pada `SumTask.java`

- **Deskripsi:**  
  SumTask.java adalah contoh implementasi multithreading di Java, biasanya digunakan untuk menghitung penjumlahan angka dalam sebuah array menggunakan beberapa thread untuk mempercepat proses.

- **Keunggulan:**  

- Meningkatkan efisiensi pemrosesan pada sistem multi-core
- Pembagian tugas secara otomatis berdasarkan ukuran data
- Pengelolaan thread dilakukan secara internal oleh framework

## b. Penerapan Thread di Linux (`thrd-posix.c`)

- **Pendekatan:**  
  Menggunakan pustaka **POSIX thread (pthread)**.  
  - Fungsi `pthread_create()` digunakan untuk membuat thread baru.  
  - Fungsi `pthread_join()` digunakan untuk menunggu thread selesai.  

- **Keunggulan:**  
  Ini adalah metode standar untuk **multithreading** di sistem **UNIX-like**, cocok untuk aplikasi server dan pemrosesan paralel.

## c. Penerapan **`thrd-win32.c` (Windows)**

- **Pendekatan:**  
  Menggunakan **Windows API** dengan fungsi `CreateThread()` untuk membuat thread baru.  
  - Thread dijalankan dengan **fungsi callback**.  
  - Sinkronisasi dilakukan dengan `WaitForSingleObject()`.

- **Perbedaan:**  
  Meski fungsionalitasnya mirip dengan **POSIX**, struktur dan parameter Windows API lebih spesifik dan berbasis **handle** sistem operasi Windows.

## Kesimpulan

Java (SumTask.java) menggunakan pendekatan berbasis objek dengan class Thread atau Runnable, yang memudahkan manajemen thread secara intuitif dan terstruktur. Cocok untuk aplikasi lintas platform karena dijalankan di atas Java Virtual Machine (JVM).

Linux (thrd-posix.c) menggunakan POSIX Threads (pthreads), yang merupakan API standar di sistem operasi Unix/Linux. Pendekatan ini bersifat low-level, memberikan kontrol lebih mendalam terhadap manajemen thread.

Windows (thrd-win32.c) menggunakan Win32 API (seperti CreateThread atau _beginthreadex) untuk mengelola thread di sistem Windows. Sama seperti POSIX, ini adalah pendekatan low-level, namun khusus untuk platform Windows.

Meskipun konsep thread di ketiga sistem ini sama (menjalankan beberapa proses secara paralel), implementasinya bergantung pada platform. Java lebih mudah dan portable, sedangkan Linux dan Windows memberikan kontrol lebih besar dengan pendekatan native sesuai OS-nya.

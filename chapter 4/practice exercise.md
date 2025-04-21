# PRACTICE EXERCISE: Konsep dan Implementasi Multithreading dalam Pemrograman

## **4.1 Provide three programming examples in which multithreading provides better performance than a single-threaded solution.**
Multithreading sering kali meningkatkan efisiensi dibandingkan solusi single-threaded. Berikut adalah tiga contoh penerapan multithreading:

- **Web Server**  
  Server berbasis multithreading dapat menangani banyak permintaan secara bersamaan, sedangkan server single-thread hanya bisa menangani satu permintaan dalam satu waktu. Hal ini meningkatkan kecepatan dan efisiensi dalam melayani pengguna.

- **Aplikasi GUI (Graphical User Interface)**  
  Dengan memisahkan proses latar belakang, seperti pengunduhan file, dari tampilan utama aplikasi, multithreading memungkinkan aplikasi tetap responsif tanpa gangguan kinerja.

- **Komputasi Paralel (Sorting, Matrix Multiplication)**  
  Tugas yang membutuhkan pemrosesan data besar dapat dibagi ke beberapa thread, sehingga mempercepat eksekusi dibandingkan jika dilakukan dalam satu alur pemrosesan.

---

## **4.2 Using Amdahl’s Law, calculate the speedup gain of an application that has a 60 percent parallel component for (a) two processing cores and (b) four processing cores.**
Amdahl’s Law mengukur peningkatan kecepatan eksekusi berdasarkan jumlah inti pemrosesan:

\[
\text{Speedup} = \frac{1}{(1-P) + \frac{P}{N}}
\]

Dimana:
- \( P = 0.6 \) (60% dari aplikasi dapat berjalan paralel)
- \( N \) = jumlah core yang tersedia

### **(a) Dengan 2 Core:**
\[
\text{Speedup} = \frac{1}{(1-0.6) + \frac{0.6}{2}} = \frac{1}{0.4 + 0.3} = \frac{1}{0.7} \approx 1.43
\]

### **(b) Dengan 4 Core:**
\[
\text{Speedup} = \frac{1}{(1-0.6) + \frac{0.6}{4}} = \frac{1}{0.4 + 0.15} = \frac{1}{0.55} \approx 1.82
\]

---

## **4.3 Does the multithreaded web server described in Section 4.1 exhibit task or data parallelism?r**
Multithreaded web server menerapkan **task parallelism**, karena setiap thread menangani permintaan pengguna yang berbeda. Meskipun tugasnya serupa, eksekusinya tetap bersifat independen.

---

## **4.4 What are two differences between user-level threads and kernel-level threads? Under what circumstances is one type better than the other?**
### **User-Level Thread**
- Dieksekusi di ruang pengguna (**user space**) tanpa keterlibatan kernel.
- Lebih cepat dalam switching antar thread karena tidak membutuhkan panggilan sistem (**system call**).
- Tidak dapat berjalan paralel pada sistem multi-core karena kernel hanya mengenali satu thread dalam suatu proses.

### **Kernel-Level Thread**
- Dikelola langsung oleh sistem operasi di **kernel space**.
- Mendukung eksekusi paralel di sistem multi-core karena setiap thread dikenali oleh kernel.
- Switching antar thread lebih lambat karena membutuhkan interaksi dengan sistem operasi.

**Keunggulan:**  
User-Level Thread lebih efisien pada sistem single-core, sedangkan Kernel-Level Thread lebih unggul pada sistem multi-core atau saat membutuhkan pengelolaan I/O yang kompleks.

---

## **4.5 Describe the actions taken by a kernel to context-switch between kernel-level threads.**
Saat sistem melakukan pergantian konteks antar thread pada tingkat kernel, langkah-langkah yang dilakukan adalah:
1. **Menyimpan Status Thread**  
   Register, counter, stack pointer, dan informasi eksekusi dari thread yang berjalan disimpan.
2. **Memperbarui Status Thread**  
   Kernel mencatat kondisi thread dalam tabel sistem.
3. **Menjadwalkan Thread Baru**  
   Scheduler memilih thread berikutnya untuk dieksekusi.
4. **Memuat Konteks Thread Baru**  
   Sistem memuat register dan data yang diperlukan oleh thread yang baru dipilih.
5. **Menjalankan Thread Baru**  
   Eksekusi dimulai berdasarkan konteks yang telah dimuat.

---

## **4.6 What resources are used when a thread is created? How do they differ from those used when a process is created?**
### **Thread**
- Memiliki **stack**, **register**, **program counter**, dan **thread ID** sendiri.
- Berbagi **memori**, **file descriptor**, serta data lainnya dengan thread lain dalam satu proses.

### **Proses**
- Membutuhkan **memori terpisah**, **file descriptor baru**, serta tabel proses independen.
- Lebih berat dibanding thread dalam hal alokasi sumber daya, sehingga switching antar proses lebih mahal.

Karena perbedaan tersebut, thread lebih ringan dan efisien dibandingkan dengan proses dalam hal pembuatan dan pergantian konteks.

---

## **4.7 Assume that an operating system maps user-level threads to the kernel using the many-to-many model and that the mapping is done through LWPs. Furthermore, the system allows developers to create real-time threads for use in real-time systems. Is it necessary to bind a real-time thread to an LWP? Explain.**
Dalam sistem yang menggunakan **many-to-many model**, user-level threads dipetakan ke kernel melalui **Lightweight Process (LWP)**. Untuk thread **real-time**, binding ke LWP diperlukan agar sistem operasi dapat menjadwalkan eksekusinya secara prioritas tinggi.

Tanpa binding ke LWP:
- Thread real-time dapat mengalami penundaan oleh thread lain.
- Kernel tidak dapat mengenali thread sebagai proses dengan tingkat urgensi tinggi.

Dengan binding ke LWP:
- Thread memiliki jalur langsung ke kernel.
- Sistem dapat memastikan eksekusi **real-time** tanpa penundaan yang tidak diinginkan.

# FLOPS IOPS

## 1. BenchmarkFLOPS32.c
Program ini dirancang untuk mengukur performa CPU dalam menjalankan operasi floating-point 32-bit (FLOPS). Dengan memanfaatkan threading, program ini mampu menjalankan perhitungan secara paralel di seluruh inti CPU. Tujuannya adalah untuk menghitung throughput CPU, baik secara keseluruhan maupun per inti, dalam satuan Gigaflops.

Hasil benchmark ditampilkan di konsol dan juga disimpan dalam file log untuk keperluan analisis lebih lanjut. Program ini sangat berguna untuk melakukan benchmark performa dan perbandingan efisiensi antar CPU.

## 2. BenchmarkFLOPS64.c
Program ini digunakan untuk mengukur kemampuan CPU dalam menangani operasi floating-point 64-bit secara paralel. Dengan menggunakan beberapa thread, perhitungan dilakukan secara simultan di berbagai inti CPU, memungkinkan evaluasi throughput maksimal dalam Gigaflops.

Benchmark ini memberikan gambaran mengenai kinerja CPU dalam menangani operasi floating-point berpresisi tinggi. Semua hasil dicetak ke konsol dan dicatat ke dalam log untuk analisis kinerja lebih mendalam.

## 3. BenchmarkIOPS32.c
Program ini bertujuan untuk mengukur performa CPU dalam melaksanakan operasi integer 32-bit (IOPS). Dengan memanfaatkan multithreading, proses benchmarking dilakukan secara paralel di beberapa inti CPU, memaksimalkan potensi multi-core processing.

Fungsi utama bertanggung jawab menjalankan operasi integer secara berulang-ulang untuk memberikan beban kerja tinggi, sementara fungsi koordinasi mengelola thread, menghitung hasil, dan menentukan throughput CPU dalam satuan Gigaiops. Output dicetak ke konsol dan disimpan dalam file log untuk referensi dan analisis performa.

## 4. enchmarkIOPS64.c
Program ini digunakan untuk mengevaluasi kinerja CPU dalam menjalankan operasi integer 64-bit (IOPS). Program menerima input jumlah core yang digunakan, kemudian membuat thread yang masing-masing menjalankan operasi integer intensif secara paralel.

Fungsi inti menjalankan perhitungan matematika kompleks dengan tipe data 64-bit selama durasi tertentu, memberikan beban kerja tinggi pada CPU. Setelah eksekusi selesai, program menghitung throughput total dan per inti CPU dalam Gigaiops, lalu menampilkannya di konsol serta menyimpannya dalam file log.

Benchmark ini memberikan informasi penting tentang kemampuan CPU dalam menangani beban kerja integer, baik dalam mode single-threaded maupun multi-threaded.

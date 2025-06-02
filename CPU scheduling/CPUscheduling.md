# **Penjadwalan CPU: Analisis Berbagai Algoritma Penjadwalan**

## **5.17 Studi Kasus: Perbandingan Algoritma Penjadwalan CPU**

### **Data Proses Awal**
Berikut adalah daftar proses dengan durasi burst time (waktu eksekusi) dan prioritas masing-masing:

| Proses | Burst Time (ms) | Prioritas |
|--------|------------------|-----------|
| P₁     | 5                | 4         |
| P₂     | 3                | 1         |
| P₃     | 1                | 2         |
| P₄     | 7                | 2         |
| P₅     | 4                | 3         |

> **Catatan:**  
Semua proses tiba pada waktu **0**, dalam urutan: **P₁, P₂, P₃, P₄, P₅**.  
Prioritas yang lebih tinggi ditunjukkan oleh angka yang lebih besar.

---

## **a. Diagram Gantt untuk Setiap Algoritma Penjadwalan**

### **1. First-Come, First-Served (FCFS)**

```
|  P₁  |  P₂  |  P₃  |  P₄  |  P₅  |
0     5     8     9     16    20
```

### **2. Shortest Job First (SJF) - Non-Preemptive**

```
|  P₃  |  P₂  |  P₅  |  P₁  |  P₄  |
0     1     4     8     13    20
```

### **3. Non-Preemptive Priority**

```
|  P₁  |  P₅  |  P₃  |  P₄  |  P₂  |
0     5     9     10    17    20
```

### **4. Round Robin (Quantum = 2 ms)**

```
| P₁ | P₂ | P₃ | P₄ | P₅ | P₁ | P₂ | P₄ | P₅ | P₄ |
0    2    4    5    7    9    11   12   14   16   20
```

---

## **b. Waktu Turnaround untuk Setiap Proses**

### **1. FCFS**
| Proses | Turnaround |
|--------|------------|
| P₁     | 5          |
| P₂     | 8          |
| P₃     | 9          |
| P₄     | 16         |
| P₅     | 20         |

**Rata-rata:** 11.6 ms

### **2. SJF**
| Proses | Turnaround |
|--------|------------|
| P₁     | 13         |
| P₂     | 4          |
| P₃     | 1          |
| P₄     | 20         |
| P₅     | 8          |

**Rata-rata:** 9.2 ms

### **3. Priority**
| Proses | Turnaround |
|--------|------------|
| P₁     | 5          |
| P₂     | 20         |
| P₃     | 10         |
| P₄     | 17         |
| P₅     | 9          |

**Rata-rata:** 12.2 ms

### **4. Round Robin**
| Proses | Turnaround |
|--------|------------|
| P₁     | 11         |
| P₂     | 12         |
| P₃     | 5          |
| P₄     | 20         |
| P₅     | 16         |

**Rata-rata:** 12.8 ms

---

## **c. Waktu Tunggu untuk Setiap Proses**

### **1. FCFS**
| Proses | Tunggu |
|--------|--------|
| P₁     | 0      |
| P₂     | 5      |
| P₃     | 8      |
| P₄     | 9      |
| P₅     | 16     |

**Rata-rata:** 7.6 ms

### **2. SJF**
| Proses | Tunggu |
|--------|--------|
| P₁     | 8      |
| P₂     | 1      |
| P₃     | 0      |
| P₄     | 13     |
| P₅     | 4      |

**Rata-rata:** 5.2 ms

### **3. Priority**
| Proses | Tunggu |
|--------|--------|
| P₁     | 0      |
| P₂     | 17     |
| P₃     | 9      |
| P₄     | 10     |
| P₅     | 5      |

**Rata-rata:** 8.2 ms

### **4. Round Robin**
| Proses | Tunggu |
|--------|--------|
| P₁     | 6      |
| P₂     | 9      |
| P₃     | 4      |
| P₄     | 13     |
| P₅     | 12     |

**Rata-rata:** 8.8 ms

---

## **d. Algoritma Terbaik Berdasarkan Rata-Rata Waktu Tunggu**

### ✅ **Shortest Job First (SJF)** dengan rata-rata **5.2 ms**

---

## **5.18 Studi Kasus: Penjadwalan Preemptive Prioritas + Round Robin**

### **Data Proses**
| Proses | Prioritas | Burst | Kedatangan |
|--------|-----------|-------|------------|
| P₁     | 8         | 15    | 0          |
| P₂     | 3         | 20    | 0          |
| P₃     | 4         | 20    | 20         |
| P₄     | 4         | 20    | 25         |
| P₅     | 5         | 5     | 45         |
| P₆     | 5         | 15    | 55         |

> Gunakan RR (q=10ms) jika prioritas sama. Preempt = pindah ke belakang antrian.

### **Diagram Gantt**

```
| P₁ | P₁ | P₃ | P₃ | P₃ | P₅ | P₆ | P₆ | P₄ | P₄ | P₂ |
0   10   20   30   40   50   60   70   80   90   100  110
```

### **Waktu Turnaround**
| Proses | Turnaround |
|--------|------------|
| P₁     | 15         |
| P₂     | 110        |
| P₃     | 20         |
| P₄     | 65         |
| P₅     | 5          |
| P₆     | 15         |

### **Waktu Tunggu**
| Proses | Tunggu |
|--------|--------|
| P₁     | 0      |
| P₂     | 90     |
| P₃     | 0      |
| P₄     | 45     |
| P₅     | 0      |
| P₆     | 0      |

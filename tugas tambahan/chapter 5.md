# Penjadwalan CPU: Priority Scheduling (Preemptive)

## Alur Program

### Alur Umum Program:

1. **Inisialisasi Proses**

   * Input: waktu kedatangan, burst time, prioritas
   * Set `sisa_waktu = burst_time`

2. **Simulasi Waktu**

   * Mulai dari `waktu = 0` sampai semua proses selesai
     
3. **Pemilihan Proses**

   * Setiap satuan waktu:

     1. Cari proses yang sudah datang (waktu_kedatangan ≤ waktu_sekarang)
     2. Pilih proses dengan prioritas tertinggi (angka terkecil)
     3. Hentikan proses berjalan jika ada proses baru dengan prioritas lebih tinggi
       
4. **Eksekusi Proses**

   * Jalankan proses terpilih selama 1 satuan waktu
   * Kurangi `sisa_waktu`
   * Proses selesai ketika `sisa_waktu = 0`

5. **Perhitungan Akhir**

   * Turnaround Time (TAT) = Waktu Selesai - Waktu Kedatangan
   * Waiting Time (WT) = TAT - Burst Time
   * Hitung rata-rata TAT dan WT

---

## Implementasi dalam Bahasa C

```c
#include <stdio.h>

#define MAX 10

typedef struct {
    int id, arrival, burst, remaining, priority;
    int finish, turnaround, waiting;
} Process;

int main() {
    Process p[3] = {
        {1, 0, 4, 4, 2},
        {2, 1, 3, 3, 1},
        {3, 2, 1, 1, 3}
    };
    int time = 0, completed = 0;
    int n = 3;

    while (completed < n) {
        int highest = -1;
        for (int i = 0; i < n; i++) {
            if (p[i].arrival <= time && p[i].remaining > 0) {
                if (highest == -1 || p[i].priority < p[highest].priority) {
                    highest = i;
                }
            }
        }

        if (highest != -1) {
            p[highest].remaining--;
            if (p[highest].remaining == 0) {
                p[highest].finish = time + 1;
                completed++;
            }
        }
        time++;
    }

    float totalTAT = 0, totalWT = 0;

    printf("Proses | Arrival | Burst | Priority | Finish | TAT | WT\n");
    for (int i = 0; i < n; i++) {
        p[i].turnaround = p[i].finish - p[i].arrival;
        p[i].waiting = p[i].turnaround - p[i].burst;
        totalTAT += p[i].turnaround;
        totalWT += p[i].waiting;
        printf("P%d     |   %d      |   %d   |    %d     |   %d    |  %d  | %d\n",
               p[i].id, p[i].arrival, p[i].burst, p[i].priority,
               p[i].finish, p[i].turnaround, p[i].waiting);
    }

    printf("\nAverage TAT: %.2f\n", totalTAT / n);
    printf("Average WT : %.2f\n", totalWT / n);

    return 0;
}
```
---

## Fitur Utama

* Simulasi per satuan waktu
* Preemptive (bisa menghentikan proses berjalan)
* Pelacakan waktu selesai yang akurat
* Perhitungan metrik setelah semua proses selesai

#  Shortest Job First (SJF) Without Arrival Time (Non-Preemptive)

Program ini mengimplementasikan algoritma **Shortest Job First (SJF)** *tanpa mempertimbangkan arrival time* dan bersifat **non-preemptive**. Proses dieksekusi berdasarkan burst time terpendek dari semua proses yang tersedia.

---

##  Deskripsi

- Proses dijalankan berdasarkan **durasi eksekusi terpendek (burst time)**.
- **Tanpa arrival time**: diasumsikan semua proses tiba pada waktu 0.
- **Non-preemptive**: proses yang berjalan tidak bisa dihentikan sampai selesai.

---

## Kode Program

```c
#include <stdio.h>

int main() {
    int n, i, j, temp;
    int process[10], burst_time[10], waiting_time[10], turnaround_time[10];
    int total_wt = 0, total_tat = 0;

    printf("Masukkan jumlah proses: ");
    scanf("%d", &n);

    for (i = 0; i < n; i++) {
        printf("Masukkan burst time untuk proses %d: ", i + 1);
        scanf("%d", &burst_time[i]);
        process[i] = i + 1;
    }

    // Sorting burst time
    for (i = 0; i < n - 1; i++) {
        for (j = i + 1; j < n; j++) {
            if (burst_time[i] > burst_time[j]) {
                temp = burst_time[i];
                burst_time[i] = burst_time[j];
                burst_time[j] = temp;

                temp = process[i];
                process[i] = process[j];
                process[j] = temp;
            }
        }
    }

    waiting_time[0] = 0;

    for (i = 1; i < n; i++) {
        waiting_time[i] = waiting_time[i - 1] + burst_time[i - 1];
    }

    for (i = 0; i < n; i++) {
        turnaround_time[i] = waiting_time[i] + burst_time[i];
        total_wt += waiting_time[i];
        total_tat += turnaround_time[i];
    }

    printf("\nProses\tBT\tWT\tTAT\n");
    for (i = 0; i < n; i++) {
        printf("P%d\t%d\t%d\t%d\n", process[i], burst_time[i], waiting_time[i], turnaround_time[i]);
    }

    printf("\nRata-rata Waiting Time: %.2f", (float)total_wt / n);
    printf("\nRata-rata Turnaround Time: %.2f\n", (float)total_tat / n);

    return 0;
}
```

##  Contoh Output

```text
Masukkan jumlah proses: 4
Masukkan burst time untuk proses 1: 6
Masukkan burst time untuk proses 2: 8
Masukkan burst time untuk proses 3: 7
Masukkan burst time untuk proses 4: 3

Proses  BT  WT  TAT
P4      3   0   3
P1      6   3   9
P3      7   9   16
P2      8   16  24

Rata-rata Waiting Time: 7.00
Rata-rata Turnaround Time: 13.00
```

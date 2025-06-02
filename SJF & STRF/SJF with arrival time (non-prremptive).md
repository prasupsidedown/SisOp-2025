#  Shortest Job First (SJF) Non-Preemptive dengan Arrival Time

Program ini mengimplementasikan algoritma penjadwalan CPU **Shortest Job First (SJF) Non-Preemptive**, di mana proses dengan burst time terpendek akan dieksekusi lebih dahulu **setelah proses tersebut tiba** (diperhitungkan berdasarkan arrival time).

---

##  Deskripsi Singkat

- Algoritma ini bersifat **non-preemptive**, artinya proses yang sedang berjalan tidak dapat diganggu oleh proses lain.
- Setiap proses memiliki waktu kedatangan (*arrival time*) dan waktu eksekusi (*burst time*).
- Tujuan algoritma ini adalah **meminimalkan waktu tunggu (waiting time)** dan **waktu penyelesaian (turnaround time)**.

---

##  Struktur Input

- `Arrival Time`: Waktu ketika proses masuk ke sistem.
- `Burst Time`: Waktu yang dibutuhkan proses untuk menyelesaikan eksekusi.

---

##  Cuplikan Kode

```c
#include <stdio.h>

int main() {
    int n, temp;
    int arrival_time[10], burst_time[10], process[10];
    int waiting_time[10], turnaround_time[10];
    int total_waiting = 0, total_turnaround = 0;

    printf("Masukkan jumlah proses: ");
    scanf("%d", &n);

    for(int i = 0; i < n; i++) {
        printf("Proses %d:\n", i+1);
        printf("Arrival Time: ");
        scanf("%d", &arrival_time[i]);
        printf("Burst Time: ");
        scanf("%d", &burst_time[i]);
        process[i] = i+1;
    }

    // Sorting berdasarkan arrival time
    for(int i = 0; i < n; i++) {
        for(int j = i+1; j < n; j++) {
            if(arrival_time[i] > arrival_time[j]) {
                temp = arrival_time[i];
                arrival_time[i] = arrival_time[j];
                arrival_time[j] = temp;

                temp = burst_time[i];
                burst_time[i] = burst_time[j];
                burst_time[j] = temp;

                temp = process[i];
                process[i] = process[j];
                process[j] = temp;
            }
        }
    }

    int time = arrival_time[0];
    for(int i = 0; i < n; i++) {
        if(time < arrival_time[i]) {
            time = arrival_time[i];
        }
        waiting_time[i] = time - arrival_time[i];
        time += burst_time[i];
        turnaround_time[i] = waiting_time[i] + burst_time[i];

        total_waiting += waiting_time[i];
        total_turnaround += turnaround_time[i];
    }

    printf("\nProses\tAT\tBT\tWT\tTAT\n");
    for(int i = 0; i < n; i++) {
        printf("P%d\t%d\t%d\t%d\t%d\n", process[i], arrival_time[i], burst_time[i], waiting_time[i], turnaround_time[i]);
    }

    printf("\nRata-rata Waiting Time: %.2f", (float)total_waiting / n);
    printf("\nRata-rata Turnaround Time: %.2f\n", (float)total_turnaround / n);

    return 0;
}
```

##  Contoh Output

```text
Masukkan jumlah proses: 3
Proses 1:
Arrival Time: 0
Burst Time: 4
Proses 2:
Arrival Time: 2
Burst Time: 3
Proses 3:
Arrival Time: 4
Burst Time: 2

Proses  AT  BT  WT  TAT
P1      0   4   0   4
P2      2   3   2   5
P3      4   2   3   5

Rata-rata Waiting Time: 1.67
Rata-rata Turnaround Time: 4.67
```

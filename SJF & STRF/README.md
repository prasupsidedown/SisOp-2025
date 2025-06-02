#  1. Shortest Job First (SJF) Non-Preemptive With Arrival Time

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

##  Kode Program

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

#  2. Shortest Job First (SJF) Without Arrival Time (Non-Preemptive)

Program ini mengimplementasikan algoritma *Shortest Job First (SJF)* tanpa mempertimbangkan arrival time dan bersifat *non-preemptive*. Proses dieksekusi berdasarkan burst time terpendek dari semua proses yang tersedia.

---

##  Deskripsi

- Proses dijalankan berdasarkan *durasi eksekusi terpendek (burst time)*.
- *Tanpa arrival time*: diasumsikan semua proses tiba pada waktu 0.
- *Non-preemptive*: proses yang berjalan tidak bisa dihentikan sampai selesai.

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
Rata-rata Turnaround Time: 13.00
```

#  3. Shortest Remaining Time First (SRTF) – Preemptive

Program ini mengimplementasikan algoritma *Shortest Remaining Time First (SRTF), yaitu versi **preemptive* dari Shortest Job First (SJF). Proses dengan sisa waktu burst paling pendek akan selalu diprioritaskan untuk dieksekusi.

---

##  Deskripsi

- Proses baru yang datang dengan burst time lebih pendek dari proses yang sedang berjalan akan langsung *menggantikan* proses tersebut.
- Arrival time dipertimbangkan.
- Cocok untuk sistem *real-time* atau *interactive*.

---

##  Kode Program

```c
#include <stdio.h>
#include <limits.h>

int main() {
    int n;
    int arrival[10], burst[10], remaining[10];
    int waiting[10], turnaround[10];
    int complete = 0, time = 0, shortest;
    int min_remaining = INT_MAX;
    int finish_time;
    float avg_wait = 0, avg_turnaround = 0;

    printf("Masukkan jumlah proses: ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++) {
        printf("Proses %d:\n", i + 1);
        printf("Arrival Time: ");
        scanf("%d", &arrival[i]);
        printf("Burst Time: ");
        scanf("%d", &burst[i]);
        remaining[i] = burst[i];
    }

    while (complete != n) {
        shortest = -1;
        min_remaining = INT_MAX;

        for (int i = 0; i < n; i++) {
            if (arrival[i] <= time && remaining[i] > 0 && remaining[i] < min_remaining) {
                min_remaining = remaining[i];
                shortest = i;
            }
        }

        if (shortest == -1) {
            time++;
            continue;
        }

        remaining[shortest]--;
        if (remaining[shortest] == 0) {
            complete++;
            finish_time = time + 1;
            waiting[shortest] = finish_time - burst[shortest] - arrival[shortest];
            if (waiting[shortest] < 0) waiting[shortest] = 0;
            turnaround[shortest] = burst[shortest] + waiting[shortest];
        }

        time++;
    }

    printf("\nProses\tAT\tBT\tWT\tTAT\n");
    for (int i = 0; i < n; i++) {
        printf("P%d\t%d\t%d\t%d\t%d\n", i + 1, arrival[i], burst[i], waiting[i], turnaround[i]);
        avg_wait += waiting[i];
        avg_turnaround += turnaround[i];
    }

    printf("\nRata-rata Waiting Time: %.2f", avg_wait / n);
    printf("\nRata-rata Turnaround Time: %.2f\n", avg_turnaround / n);

    return 0;
}
```

##  Contoh Output

```text
Masukkan jumlah proses: 4
Proses 1:
Arrival Time: 0
Burst Time: 8
Proses 2:
Arrival Time: 1
Burst Time: 4
Proses 3:
Arrival Time: 2
Burst Time: 9
Proses 4:
Arrival Time: 3
Burst Time: 5

Proses  AT  BT  WT  TAT
P1      0   8   9   17
P2      1   4   0   4
P3      2   9   15  24
P4      3   5   4   9

Rata-rata Waiting Time: 7.00
Rata-rata Turnaround Time: 13.50
```

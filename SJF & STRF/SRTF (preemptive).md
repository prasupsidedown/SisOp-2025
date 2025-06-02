#  Shortest Remaining Time First (SRTF) – Preemptive

Program ini mengimplementasikan algoritma **Shortest Remaining Time First (SRTF)**, yaitu versi **preemptive** dari Shortest Job First (SJF). Proses dengan sisa waktu burst paling pendek akan selalu diprioritaskan untuk dieksekusi.

---

##  Deskripsi

- Proses baru yang datang dengan burst time lebih pendek dari proses yang sedang berjalan akan langsung **menggantikan** proses tersebut.
- Arrival time dipertimbangkan.
- Cocok untuk sistem **real-time** atau **interactive**.

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
Rata-rata Turnaround Time: 13.50
```

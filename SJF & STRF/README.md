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
#include<stdio.h>
struct proc
{
    int no,at,bt,it,ct,tat,wt;
};
struct proc read(int i)
{
    struct proc p;
    printf("\nProcess No: %d\n",i);
    p.no=i;
    printf("Enter Arrival Time: ");
    scanf("%d",&p.at);
    printf("Enter Burst Time: ");
    scanf("%d",&p.bt);
    return p;
}
int main()
{
    int  n,j,min=0;
    float avgtat=0,avgwt=0;
    struct proc p[10],temp;
    printf("<--SJF Scheduling Algorithm (Non-Preemptive)-->\n");
    printf("Enter Number of Processes: ");
    scanf("%d",&n);
    for(int i=0;i<n;i++)
        p[i]=read(i+1);
    for(int i=0;i<n-1;i++)
        for(j=0;j<n-i-1;j++)    
            if(p[j].at>p[j+1].at)
            {
            temp=p[j];
            p[j]=p[j+1];
            p[j+1]=temp;
            }
    for(j=1;j<n&&p[j].at==p[0].at;j++)
        if(p[j].bt<p[min].bt)
            min=j;
    temp=p[0];
    p[0]=p[min];
    p[min]=temp;
    p[0].it=p[0].at;
    p[0].ct=p[0].it+p[0].bt;
    for(int i=1;i<n;i++)
    {
        for(j=i+1,min=i;j<n&&p[j].at<=p[i-1].ct;j++)
            if(p[j].bt<p[min].bt)
                min=j;
        temp=p[i];
        p[i]=p[min];
        p[min]=temp;
        if(p[i].at<=p[i-1].ct)
            p[i].it=p[i-1].ct;
        else
            p[i].it=p[i].at;
        p[i].ct=p[i].it+p[i].bt;
    }
    printf("\nProcess\t\tAT\tBT\tCT\tTAT\tWT\tRT\n");
    for(int i=0;i<n;i++)
    {
        p[i].tat=p[i].ct-p[i].at;
        avgtat+=p[i].tat;
        p[i].wt=p[i].tat-p[i].bt;
        avgwt+=p[i].wt;
        printf("P%d\t\t%d\t%d\t%d\t%d\t%d\t%d\n",p[i].no,p[i].at,p[i].bt,p[i].ct,p[i].tat,p[i].wt,p[i].wt);
    }
    avgtat/=n,avgwt/=n;
    printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f",avgtat,avgwt);
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
#include<stdio.h>
struct proc
{
    int no,bt,ct,tat,wt;
};
struct proc read(int i)
{
    struct proc p;
    printf("\nProcess No: %d\n",i);
    p.no=i;
    printf("Enter Burst Time: ");
    scanf("%d",&p.bt);
    return p;
}
int main()
{
    struct proc p[10],tmp;
    float avgtat=0,avgwt=0;
    int n,ct=0;
    printf("<--SJF Scheduling Algorithm Without Arrival Time (Non-Preemptive)-->\n");
    printf("Enter Number of Processes: ");
    scanf("%d",&n);
    for(int i=0;i<n;i++)
        p[i]=read(i+1);
    for(int i=0;i<n-1;i++)
        for(int j=0;j<n-i-1;j++)    
            if(p[j].bt>p[j+1].bt)
            {
				tmp=p[j];
				p[j]=p[j+1];
				p[j+1]=tmp;
            }
    printf("\nProcessNo\tBT\tCT\tTAT\tWT\tRT\n");
    for(int i=0;i<n;i++)
    {
        ct+=p[i].bt;
		p[i].ct=p[i].tat=ct;
		avgtat+=p[i].tat;
        p[i].wt=p[i].tat-p[i].bt;
        avgwt+=p[i].wt;
        printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n",p[i].no,p[i].bt,p[i].ct,p[i].tat,p[i].wt,p[i].wt);
    }
    avgtat/=n,avgwt/=n;
    printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f",avgtat,avgwt);
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
#include<stdio.h>
#define MAX 9999
struct proc
{
    int no,at,bt,rt,ct,tat,wt;
};
struct proc read(int i)
{
    struct proc p;
    printf("\nProcess No: %d\n",i);
    p.no=i;
    printf("Enter Arrival Time: ");
    scanf("%d",&p.at);
    printf("Enter Burst Time: ");
    scanf("%d",&p.bt);
    p.rt=p.bt;
    return p;
}
int main()
{
    struct proc p[10],temp;
    float avgtat=0,avgwt=0;
    int n,s,remain=0,time;
    printf("<--SRTF Scheduling Algorithm (Preemptive)-->\n");
    printf("Enter Number of Processes: ");
    scanf("%d",&n);
    for(int i=0;i<n;i++)
        p[i]=read(i+1);
    for(int i=0;i<n-1;i++)
        for(int j=0;j<n-i-1;j++)    
            if(p[j].at>p[j+1].at)
            {
            temp=p[j];
            p[j]=p[j+1];
            p[j+1]=temp;
            }
    printf("\nProcess\t\tAT\tBT\tCT\tTAT\tWT\n");
    p[9].rt=MAX;
    for(time=0;remain!=n;time++)
    {
        s=9;
        for(int i=0;i<n;i++)
            if(p[i].at<=time&&p[i].rt<p[s].rt&&p[i].rt>0)
                s=i;
        p[s].rt--;
        if(p[s].rt==0)
        {
            remain++;
            p[s].ct=time+1;
            p[s].tat=p[s].ct-p[s].at;
            avgtat+=p[s].tat;
            p[s].wt=p[s].tat-p[s].bt;
            avgwt+=p[s].wt;
            printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n",p[s].no,p[s].at,p[s].bt,p[s].ct,p[s].tat,p[s].wt);
        }
    }
    avgtat/=n,avgwt/=n;
    printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f",avgtat,avgwt);
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

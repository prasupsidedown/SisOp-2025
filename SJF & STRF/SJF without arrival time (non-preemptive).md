1) SJF without arrival time (non-preemptive) 

program : 
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

Analisa : 
Program ini pakai algoritma SJF non-preemptive tanpa arrival time. Cara kerjanya: input jumlah dan burst time proses, lalu proses diurutkan dari yang burst time-nya paling kecil. 
Setelah itu, dihitung completion time, turnaround time, dan waiting time. Hasilnya ditampilkan dalam tabel, plus rata-rata TAT dan WT.

contoh output : 

ProcessNo   BT   CT   TAT   WT   RT
P1          3    3    3     0    0
P2          5    8    8     3    3

Kesimpulan : 
Program ini menyimulasikan algoritma SJF Non-Preemptive tanpa arrival time dengan cara mengurutkan proses berdasarkan burst time terkecil dan menghitung waktu eksekusinya. 
Hasilnya mencakup completion time, turnaround time, waiting time, dan response time.

> [!NOTE]- FCFS Algorithm
> ```c
> #include <stdio.h>
> 
> int main() {
>     int n, i;
>     printf("Enter the number of processes: ");
>     scanf("%d", &n);
> 
>     int bt[n], wt[n], tat[n];
> 
>     printf("Enter Burst Times:\n");
>     for (i = 0; i < n; i++) {
>         printf("Process %d: ", i + 1);
>         scanf("%d", &bt[i]);
>     }
> 
>     wt[0] = 0;
>     tat[0] = bt[0];
> 
>     for (i = 1; i < n; i++) {
>         wt[i] = wt[i - 1] + bt[i - 1];
>         tat[i] = wt[i] + bt[i];
>     }
> 
>     printf("\nFCFS Scheduling:\n");
>     printf("Process\tBT\tWT\tTAT\n");
>     for (i = 0; i < n; i++) {
>         printf("P%d\t%d\t%d\t%d\n", i + 1, bt[i], wt[i], tat[i]);
>     }
> 
>     return 0;
> }
> ```


💡 Key Terms

| Term                  | Meaning                                      |
| --------------------- | -------------------------------------------- |
| Burst Time (BT)       | Time a process needs to complete             |
| Waiting Time (WT)     | Time a process waits in queue before it runs |
| Turnaround Time (TAT) | Time from arrival to finish (WT + BT)        |


> [!NOTE]- SJF Algorithm
> ```c
> #include <stdio.h>
> 
> void swap(int *a, int *b) {
>     int temp = *a; *a = *b; *b = temp;
> }
> 
> int main() {
>     int n, i, j;
>     printf("Enter the number of processes: ");
>     scanf("%d", &n);
> 
>     int bt[n], p[n], wt[n], tat[n];
> 
>     for (i = 0; i < n; i++) {
>         p[i] = i + 1;
>         printf("Enter burst time for process %d: ", i + 1);
>         scanf("%d", &bt[i]);
>     }
> 
>     // Sort burst times using bubble sort for SJF (non-preemptive)
>     for (i = 0; i < n-1; i++) {
>         for (j = 0; j < n-i-1; j++) {
>             if (bt[j] > bt[j + 1]) {
>                 swap(&bt[j], &bt[j + 1]);
>                 swap(&p[j], &p[j + 1]);
>             }
>         }
>     }
> 
>     wt[0] = 0;
>     tat[0] = bt[0];
> 
>     for (i = 1; i < n; i++) {
>         wt[i] = wt[i - 1] + bt[i - 1];
>         tat[i] = wt[i] + bt[i];
>     }
> 
>     printf("\nSJF Scheduling:\n");
>     printf("Process\tBT\tWT\tTAT\n");
>     for (i = 0; i < n; i++) {
>         printf("P%d\t%d\t%d\t%d\n", p[i], bt[i], wt[i], tat[i]);
>     }
> 
>     return 0;
> }
> 
> ```


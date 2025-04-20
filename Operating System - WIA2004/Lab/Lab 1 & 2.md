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

> [!NOTE]- Other SJF Code
> ```c
> #include <stdio.h>
> #include <stdbool.h>
> 
> struct Process {
>     int pid;        // Process ID
>     int burst;      // Burst time
>     int arrival;    // Arrival time (assuming all arrive at 0 for simplicity)
>     int waiting;    // Waiting time
>     int turnaround; // Turnaround time
> };
> 
> void sortProcesses(struct Process p[], int n) {
>     // Sort processes by burst time (SJF)
>     // If burst times are equal, maintain FCFS order
>     for (int i = 0; i < n - 1; i++) {
>         for (int j = 0; j < n - i - 1; j++) {
>             if (p[j].burst > p[j + 1].burst) {
>                 // Swap processes
>                 struct Process temp = p[j];
>                 p[j] = p[j + 1];
>                 p[j + 1] = temp;
>             }
>         }
>     }
> }
> 
> void calculateTimes(struct Process p[], int n) {
>     // Calculate waiting and turnaround times
>     p[0].waiting = 0;
>     p[0].turnaround = p[0].burst;
>     
>     for (int i = 1; i < n; i++) {
>         p[i].waiting = p[i - 1].turnaround + p[i - 1].waiting;
>         p[i].turnaround = p[i].waiting + p[i].burst;
>     }
> }
> 
> void printResults(struct Process p[], int n) {
>     float avg_waiting = 0, avg_turnaround = 0;
>     
>     printf("\nProcess\tBurst Time\tWaiting Time\tTurnaround Time\n");
>     for (int i = 0; i < n; i++) {
>         printf("%d\t%d\t\t%d\t\t%d\n", 
>                p[i].pid, p[i].burst, p[i].waiting, p[i].turnaround);
>         
>         avg_waiting += p[i].waiting;
>         avg_turnaround += p[i].turnaround;
>     }
>     
>     avg_waiting /= n;
>     avg_turnaround /= n;
>     
>     printf("\nAverage Waiting Time: %.2f", avg_waiting);
>     printf("\nAverage Turnaround Time: %.2f\n", avg_turnaround);
> }
> 
> int main() {
>     int n;
>     
>     printf("Enter the number of processes: ");
>     scanf("%d", &n);
>     
>     struct Process processes[n];
>     
>     // Input process details
>     for (int i = 0; i < n; i++) {
>         processes[i].pid = i + 1;
>         printf("Enter burst time for process %d: ", i + 1);
>         scanf("%d", &processes[i].burst);
>         processes[i].arrival = 0; // Assuming all processes arrive at time 0
>     }
>     
>     // Sort processes by burst time (SJF)
>     sortProcesses(processes, n);
>     
>     // Calculate waiting and turnaround times
>     calculateTimes(processes, n);
>     
>     // Print results
>     printResults(processes, n);
>     
>     return 0;
> }
> ```
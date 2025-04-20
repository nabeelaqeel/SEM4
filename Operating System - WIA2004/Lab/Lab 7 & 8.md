> [!NOTE]- FIFO Page Replacement Algorithm
> ```c
> #include <stdio.h>
> 
> void fifo(int pages[], int n, int frames) {
>     int temp[frames], page_faults = 0, s = 0, i, j, k;
>     
>     for(i = 0; i < frames; i++)
>         temp[i] = -1;  // Initialize frames to -1 (empty)
>     
>     printf("Page\tFrames\tFault\n");
>     for(i = 0; i < n; i++) {
>         s = 0;
>         for(j = 0; j < frames; j++) {
>             if(temp[j] == pages[i]) {
>                 s = 1;  // Page found in frame
>                 break;
>             }
>         }
>         
>         if(s == 0) {  // Page fault occurred
>             temp[page_faults % frames] = pages[i];  // Replace using FIFO
>             page_faults++;
>         }
>         
>         printf("%d\t", pages[i]);
>         for(k = 0; k < frames; k++)
>             printf("%d ", temp[k]);
>         printf("\t%s\n", s == 0 ? "F" : "H");
>     }
>     printf("\nTotal Page Faults: %d\n", page_faults);
> }
> 
> int main() {
>     int pages[] = {7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2};
>     int n = sizeof(pages)/sizeof(pages[0]);
>     int frames = 3;
>     
>     fifo(pages, n, frames);
>     return 0;
> }
> ```

> [!NOTE]- Dining Philosophers Problem
> ```c
> #include <stdio.h>
> #include <pthread.h>
> #include <semaphore.h>
> #include <unistd.h>
> 
> #define N 5  // Number of philosophers
> #define LEFT (phil_num + N - 1) % N
> #define RIGHT (phil_num + 1) % N
> 
> sem_t mutex;
> sem_t S[N];
> 
> void* philosopher(void* num) {
>     int phil_num = *(int*)num;
>     
>     while(1) {
>         printf("Philosopher %d is thinking\n", phil_num+1);
>         sleep(1);
>         
>         sem_wait(&mutex);
>         sem_wait(&S[LEFT]);
>         sem_wait(&S[RIGHT]);
>         
>         printf("Philosopher %d takes fork %d and %d\n", 
>               phil_num+1, LEFT+1, phil_num+1);
>         printf("Philosopher %d is eating\n", phil_num+1);
>         sleep(1);
>         
>         sem_post(&S[RIGHT]);
>         sem_post(&S[LEFT]);
>         sem_post(&mutex);
>     }
> }
> 
> int main() {
>     int i, a[N];
>     pthread_t tid[N];
>     
>     sem_init(&mutex, 0, 1);
>     for(i = 0; i < N; i++)
>         sem_init(&S[i], 0, 1);
>     
>     for(i = 0; i < N; i++) {
>         a[i] = i;
>         pthread_create(&tid[i], NULL, philosopher, &a[i]);
>     }
>     
>     for(i = 0; i < N; i++)
>         pthread_join(tid[i], NULL);
>     
>     return 0;
> }
> ```


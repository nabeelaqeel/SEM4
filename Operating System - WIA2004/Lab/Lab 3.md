
> [!NOTE]- File Allocation Strategies
> ```c
> #include <stdio.h>
> 
> int main() {
>     int n, i, start, len;
>     
>     printf("Enter no. of blocks: ");
>     scanf("%d", &n);
>     
>     int b[n];
>     for(i=0; i<n; i++) b[i] = 0; // 0 means free
>     
>     printf("Enter starting block & length: ");
>     scanf("%d %d", &start, &len);
>     
>     if(start+len > n) {
>         printf("Not enough space!\n");
>         return 0;
>     }
>     
>     for(i=start; i<start+len; i++) {
>         if(b[i] == 1) {
>             printf("Block %d already allocated!\n", i);
>             return 0;
>         }
>         b[i] = 1; // 1 means allocated
>     }
>     
>     printf("File allocated to blocks: ");
>     for(i=start; i<start+len; i++) 
>         printf("%d ", i);
>     
>     return 0;
> }
> ```


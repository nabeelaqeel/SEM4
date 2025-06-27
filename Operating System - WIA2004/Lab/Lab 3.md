
> [!NOTE]- File Allocation Strategies : Sequential
> ```c
> #include <stdio.h>
> #include <stdlib.h>
> #include <stdbool.h>
> #include <string.h>
> 
> #define MAX_FILES 100
> #define MAX_BLOCKS 1000
> #define MAX_FILENAME 50
> 
> typedef struct {
>     char name[MAX_FILENAME];
>     int start_block;
>     int length;
>     bool allocated;
> } File;
> 
> // Global variables
> int disk[MAX_BLOCKS];  // Disk blocks (0 = free, 1 = allocated)
> File files[MAX_FILES];  // File table
> int num_files = 0;
> 
> // Function prototypes
> void initializeDisk();
> void displayMenu();
> void allocateFile();
> void deleteFile();
> void displayFiles();
> void displayDiskStatus();
> 
> int main() {
>     int choice;
>     
>     initializeDisk();
>     
>     while (1) {
>         displayMenu();
>         printf("Enter your choice: ");
>         scanf("%d", &choice);
>         
>         switch (choice) {
>             case 1:
>                 allocateFile();
>                 break;
>             case 2:
>                 deleteFile();
>                 break;
>             case 3:
>                 displayFiles();
>                 break;
>             case 4:
>                 displayDiskStatus();
>                 break;
>             case 5:
>                 printf("Exiting program...\n");
>                 return 0;
>             default:
>                 printf("Invalid choice! Please try again.\n");
>         }
>         
>         printf("\nPress Enter to continue...");
>         getchar();
>         getchar();  // Consume newline
>     }
>     
>     return 0;
> }
> 
> void initializeDisk() {
>     for (int i = 0; i < MAX_BLOCKS; i++) {
>         disk[i] = 0;  // Initialize all blocks as free
>     }
>     
>     for (int i = 0; i < MAX_FILES; i++) {
>         files[i].allocated = false;
>     }
>     
>     printf("Disk initialized with %d blocks.\n", MAX_BLOCKS);
> }
> 
> void displayMenu() {
>     printf("\n\n====== SEQUENTIAL FILE ALLOCATION SIMULATOR ======\n");
>     printf("1. Allocate a new file\n");
>     printf("2. Delete a file\n");
>     printf("3. Display file table\n");
>     printf("4. Display disk status\n");
>     printf("5. Exit\n");
> }
> 
> void allocateFile() {
>     char filename[MAX_FILENAME];
>     int size, start_block = -1;
>     
>     if (num_files >= MAX_FILES) {
>         printf("Error: File table is full!\n");
>         return;
>     }
>     
>     printf("Enter file name: ");
>     scanf("%s", filename);
>     
>     // Check if file already exists
>     for (int i = 0; i < num_files; i++) {
>         if (files[i].allocated && strcmp(files[i].name, filename) == 0) {
>             printf("Error: File '%s' already exists!\n", filename);
>             return;
>         }
>     }
>     
>     printf("Enter file size (number of blocks): ");
>     scanf("%d", &size);
>     
>     if (size <= 0 || size > MAX_BLOCKS) {
>         printf("Error: Invalid file size!\n");
>         return;
>     }
>     
>     // Find contiguous blocks for the file (Sequential allocation)
>     int current_start = -1;
>     int current_length = 0;
>     
>     for (int i = 0; i < MAX_BLOCKS; i++) {
>         if (disk[i] == 0) {  // Free block
>             if (current_start == -1) {
>                 current_start = i;
>             }
>             current_length++;
>             
>             if (current_length == size) {
>                 start_block = current_start;
>                 break;
>             }
>         } else {  // Allocated block
>             current_start = -1;
>             current_length = 0;
>         }
>     }
>     
>     if (start_block == -1) {
>         printf("Error: Not enough contiguous space available on disk!\n");
>         return;
>     }
>     
>     // Allocate the blocks
>     for (int i = start_block; i < start_block + size; i++) {
>         disk[i] = 1;  // Mark as allocated
>     }
>     
>     // Update file table
>     strcpy(files[num_files].name, filename);
>     files[num_files].start_block = start_block;
>     files[num_files].length = size;
>     files[num_files].allocated = true;
>     num_files++;
>     
>     printf("File '%s' allocated successfully!\n", filename);
>     printf("Start block: %d, Size: %d blocks\n", start_block, size);
> }
> 
> void deleteFile() {
>     char filename[MAX_FILENAME];
>     int file_index = -1;
>     
>     printf("Enter file name to delete: ");
>     scanf("%s", filename);
>     
>     // Find the file
>     for (int i = 0; i < num_files; i++) {
>         if (files[i].allocated && strcmp(files[i].name, filename) == 0) {
>             file_index = i;
>             break;
>         }
>     }
>     
>     if (file_index == -1) {
>         printf("Error: File '%s' not found!\n", filename);
>         return;
>     }
>     
>     // Free the allocated blocks
>     for (int i = files[file_index].start_block; 
>          i < files[file_index].start_block + files[file_index].length; 
>          i++) {
>         disk[i] = 0;  // Mark as free
>     }
>     
>     // Update file table
>     printf("File '%s' deleted successfully!\n", files[file_index].name);
>     files[file_index].allocated = false;
>     
>     // Compact the file table (optional)
>     if (file_index < num_files - 1) {
>         for (int i = file_index; i < num_files - 1; i++) {
>             files[i] = files[i + 1];
>         }
>     }
>     num_files--;
> }
> 
> void displayFiles() {
>     if (num_files == 0) {
>         printf("No files are currently allocated.\n");
>         return;
>     }
>     
>     printf("\n========== FILE TABLE ==========\n");
>     printf("%-20s %-15s %-15s\n", "Filename", "Start Block", "Size (blocks)");
>     printf("----------------------------------------\n");
>     
>     for (int i = 0; i < num_files; i++) {
>         if (files[i].allocated) {
>             printf("%-20s %-15d %-15d\n", 
>                    files[i].name, 
>                    files[i].start_block, 
>                    files[i].length);
>         }
>     }
> }
> 
> void displayDiskStatus() {
>     int total_blocks = MAX_BLOCKS;
>     int allocated_blocks = 0;
>     int free_blocks = 0;
>     
>     for (int i = 0; i < MAX_BLOCKS; i++) {
>         if (disk[i] == 1) {
>             allocated_blocks++;
>         } else {
>             free_blocks++;
>         }
>     }
>     
>     printf("\n========== DISK STATUS ==========\n");
>     printf("Total blocks: %d\n", total_blocks);
>     printf("Allocated blocks: %d (%.2f%%)\n", 
>            allocated_blocks, 
>            (float)allocated_blocks / total_blocks * 100);
>     printf("Free blocks: %d (%.2f%%)\n", 
>            free_blocks, 
>            (float)free_blocks / total_blocks * 100);
>     
>     // Display a simple visual representation of the disk
>     printf("\nDisk Map (each character represents 10 blocks):\n");
>     printf("[");
>     for (int i = 0; i < MAX_BLOCKS; i += 10) {
>         int block_group_usage = 0;
>         for (int j = i; j < i + 10 && j < MAX_BLOCKS; j++) {
>             if (disk[j] == 1) {
>                 block_group_usage++;
>             }
>         }
>         
>         if (block_group_usage == 0) {
>             printf(" ");  // Empty
>         } else if (block_group_usage < 5) {
>             printf("░");  // Partially filled
>         } else if (block_group_usage < 10) {
>             printf("▒");  // Mostly filled
>         } else {
>             printf("█");  // Completely filled
>         }
>     }
>     printf("]");
> }
> ```

> [!NOTE]- File Allocation Strategies : Index
> ```c
> #include <stdio.h>
> #include <stdlib.h>
> #include <stdbool.h>
> #include <string.h>
> 
> #define MAX_FILES 10
> #define MAX_BLOCKS 100
> #define MAX_FILENAME 50
> #define INDEX_BLOCK_ENTRIES 10  // Number of block pointers an index block can hold
> 
> typedef struct {
>     char name[MAX_FILENAME];
>     int index_block;       // Block number of the index block
>     int length;            // Size of file in blocks
>     bool allocated;
> } File;
> 
> // Global variables
> int disk[MAX_BLOCKS];      // Disk blocks (0 = free, 1 = allocated)
> int index_blocks[MAX_BLOCKS][INDEX_BLOCK_ENTRIES];  // Array to store index blocks
> File files[MAX_FILES];     // File table
> int num_files = 0;
> 
> // Function prototypes
> void initializeDisk();
> void displayMenu();
> void allocateFile();
> void deleteFile();
> void displayFiles();
> void displayDiskStatus();
> int findFreeBlock();
> 
> int main() {
>     int choice;
>     
>     initializeDisk();
>     
>     while (1) {
>         displayMenu();
>         printf("Enter your choice: ");
>         scanf("%d", &choice);
>         
>         switch (choice) {
>             case 1:
>                 allocateFile();
>                 break;
>             case 2:
>                 deleteFile();
>                 break;
>             case 3:
>                 displayFiles();
>                 break;
>             case 4:
>                 displayDiskStatus();
>                 break;
>             case 5:
>                 printf("Exiting program...\n");
>                 return 0;
>             default:
>                 printf("Invalid choice! Please try again.\n");
>         }
>         
>         printf("\nPress Enter to continue...");
>         getchar();
>         getchar();  // Consume newline
>     }
>     
>     return 0;
> }
> 
> void initializeDisk() {
>     for (int i = 0; i < MAX_BLOCKS; i++) {
>         disk[i] = 0;  // Initialize all blocks as free
>         
>         // Initialize all index block entries to -1 (invalid block number)
>         for (int j = 0; j < INDEX_BLOCK_ENTRIES; j++) {
>             index_blocks[i][j] = -1;
>         }
>     }
>     
>     for (int i = 0; i < MAX_FILES; i++) {
>         files[i].allocated = false;
>     }
>     
>     printf("Disk initialized with %d blocks.\n", MAX_BLOCKS);
> }
> 
> void displayMenu() {
>     printf("\n\n====== INDEXED FILE ALLOCATION SIMULATOR ======\n");
>     printf("1. Allocate a new file\n");
>     printf("2. Delete a file\n");
>     printf("3. Display file table\n");
>     printf("4. Display disk status\n");
>     printf("5. Exit\n");
> }
> 
> int findFreeBlock() {
>     for (int i = 0; i < MAX_BLOCKS; i++) {
>         if (disk[i] == 0) {
>             return i;
>         }
>     }
>     return -1;  // No free block found
> }
> 
> void allocateFile() {
>     char filename[MAX_FILENAME];
>     int size;
>     
>     if (num_files >= MAX_FILES) {
>         printf("Error: File table is full!\n");
>         return;
>     }
>     
>     printf("Enter file name: ");
>     scanf("%s", filename);
>     
>     // Check if file already exists
>     for (int i = 0; i < num_files; i++) {
>         if (files[i].allocated && strcmp(files[i].name, filename) == 0) {
>             printf("Error: File '%s' already exists!\n", filename);
>             return;
>         }
>     }
>     
>     printf("Enter file size (number of blocks): ");
>     scanf("%d", &size);
>     
>     if (size <= 0 || size > INDEX_BLOCK_ENTRIES) {
>         printf("Error: Invalid file size! Maximum allowed size is %d blocks.\n", INDEX_BLOCK_ENTRIES);
>         return;
>     }
>     
>     // Count free blocks to check if allocation is possible
>     int free_count = 0;
>     for (int i = 0; i < MAX_BLOCKS; i++) {
>         if (disk[i] == 0) {
>             free_count++;
>         }
>     }
>     
>     if (free_count < size + 1) {  // +1 for the index block
>         printf("Error: Not enough free blocks available for allocation!\n");
>         return;
>     }
>     
>     // First, allocate an index block
>     int index_block = findFreeBlock();
>     if (index_block == -1) {
>         printf("Error: No free blocks for index block!\n");
>         return;
>     }
>     
>     // Mark the index block as allocated
>     disk[index_block] = 1;
>     
>     // Array to store allocated data blocks
>     int data_blocks[INDEX_BLOCK_ENTRIES];
>     int allocated_blocks = 0;
>     
>     // Allocate data blocks for the file (non-contiguous)
>     for (int i = 0; i < size; i++) {
>         int block = findFreeBlock();
>         if (block == -1) {
>             printf("Error: Could not allocate all necessary blocks!\n");
>             
>             // Free any blocks we've already allocated
>             disk[index_block] = 0;
>             for (int j = 0; j < allocated_blocks; j++) {
>                 disk[data_blocks[j]] = 0;
>             }
>             return;
>         }
>         
>         // Mark the data block as allocated
>         disk[block] = 1;
>         data_blocks[allocated_blocks] = block;
>         
>         // Add pointer to the index block
>         index_blocks[index_block][i] = block;
>         allocated_blocks++;
>     }
>     
>     // Update file table
>     strcpy(files[num_files].name, filename);
>     files[num_files].index_block = index_block;
>     files[num_files].length = size;
>     files[num_files].allocated = true;
>     num_files++;
>     
>     printf("File '%s' allocated successfully!\n", filename);
>     printf("Index block: %d, Size: %d blocks\n", index_block, size);
>     printf("Data blocks allocated: ");
>     for (int i = 0; i < (size > 5 ? 5 : size); i++) {
>         printf("%d ", data_blocks[i]);
>     }
>     if (size > 5) printf("...");
>     printf("\n");
> }
> 
> void deleteFile() {
>     char filename[MAX_FILENAME];
>     int file_index = -1;
>     
>     printf("Enter file name to delete: ");
>     scanf("%s", filename);
>     
>     // Find the file
>     for (int i = 0; i < num_files; i++) {
>         if (files[i].allocated && strcmp(files[i].name, filename) == 0) {
>             file_index = i;
>             break;
>         }
>     }
>     
>     if (file_index == -1) {
>         printf("Error: File '%s' not found!\n", filename);
>         return;
>     }
>     
>     int index_block = files[file_index].index_block;
>     
>     // Free the data blocks
>     for (int i = 0; i < files[file_index].length; i++) {
>         int block = index_blocks[index_block][i];
>         if (block != -1) {
>             disk[block] = 0;  // Mark as free
>             printf("Freed data block %d\n", block);
>         }
>     }
>     
>     // Free the index block
>     disk[index_block] = 0;
>     printf("Freed index block %d\n", index_block);
>     
>     // Reset index block entries
>     for (int i = 0; i < INDEX_BLOCK_ENTRIES; i++) {
>         index_blocks[index_block][i] = -1;
>     }
>     
>     // Update file table
>     printf("File '%s' deleted successfully!\n", files[file_index].name);
>     files[file_index].allocated = false;
>     
>     // Compact the file table (optional)
>     if (file_index < num_files - 1) {
>         for (int i = file_index; i < num_files - 1; i++) {
>             files[i] = files[i + 1];
>         }
>     }
>     num_files--;
> }
> 
> void displayFiles() {
>     if (num_files == 0) {
>         printf("No files are currently allocated.\n");
>         return;
>     }
>     
>     printf("\n========== FILE TABLE ==========\n");
>     printf("%-20s %-15s %-15s %-30s\n", "Filename", "Index Block", "Size (blocks)", "Data Blocks (first 5)");
>     printf("--------------------------------------------------------------------------------\n");
>     
>     for (int i = 0; i < num_files; i++) {
>         if (files[i].allocated) {
>             printf("%-20s %-15d %-15d ", 
>                    files[i].name, 
>                    files[i].index_block, 
>                    files[i].length);
>             
>             // Display the first few data blocks (up to 5)
>             printf("[");
>             int max_display = (files[i].length > 5) ? 5 : files[i].length;
>             for (int j = 0; j < max_display; j++) {
>                 printf("%d", index_blocks[files[i].index_block][j]);
>                 if (j < max_display - 1) {
>                     printf(", ");
>                 }
>             }
>             if (files[i].length > 5) {
>                 printf(", ...");
>             }
>             printf("]\n");
>         }
>     }
> }
> 
> void displayDiskStatus() {
>     int total_blocks = MAX_BLOCKS;
>     int allocated_blocks = 0;
>     int free_blocks = 0;
>     int index_blocks_count = 0;
>     int data_blocks_count = 0;
>     
>     for (int i = 0; i < MAX_BLOCKS; i++) {
>         if (disk[i] == 1) {
>             allocated_blocks++;
>             
>             // Check if this is an index block
>             bool is_index = false;
>             for (int j = 0; j < num_files; j++) {
>                 if (files[j].allocated && files[j].index_block == i) {
>                     is_index = true;
>                     index_blocks_count++;
>                     break;
>                 }
>             }
>             
>             if (!is_index) {
>                 data_blocks_count++;
>             }
>         } else {
>             free_blocks++;
>         }
>     }
>     
>     printf("\n========== DISK STATUS ==========\n");
>     printf("Total blocks: %d\n", total_blocks);
>     printf("Allocated blocks: %d (%.2f%%)\n", 
>            allocated_blocks, 
>            (float)allocated_blocks / total_blocks * 100);
>     printf("  - Index blocks: %d\n", index_blocks_count);
>     printf("  - Data blocks: %d\n", data_blocks_count);
>     printf("Free blocks: %d (%.2f%%)\n", 
>            free_blocks, 
>            (float)free_blocks / total_blocks * 100);
>     
>     // Display a simple visual representation of the disk
>     printf("\nDisk Map (each character represents 10 blocks):\n");
>     printf("[");
>     for (int i = 0; i < MAX_BLOCKS; i += 10) {
>         int block_group_usage = 0;
>         for (int j = i; j < i + 10 && j < MAX_BLOCKS; j++) {
>             if (disk[j] == 1) {
>                 block_group_usage++;
>             }
>         }
>         
>         if (block_group_usage == 0) {
>             printf(" ");  // Empty
>         } else if (block_group_usage < 5) {
>             printf("p");  // Partially filled
>         } else if (block_group_usage < 10) {
>             printf("m");  // Mostly filled
>         } else {
>             printf("c");  // Completely filled
>         }
>     }
>     printf("]\n");
>     
>     // Advanced feature: Display fragmentation level
>     int total_fragments = 0;
>     bool in_fragment = false;
>     
>     for (int i = 0; i < MAX_BLOCKS; i++) {
>         if (disk[i] == 0 && !in_fragment) {
>             in_fragment = true;
>             total_fragments++;
>         } else if (disk[i] == 1) {
>             in_fragment = false;
>         }
>     }
>     
>     printf("Free space fragments: %d\n", total_fragments);
> }
> ```
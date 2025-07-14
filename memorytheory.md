### 1.What is memory management in system programming?
Memory management in system programming is the process of efficiently allocating, tracking, and freeing memory resources used by programs during their execution.
### 2.Define virtual memory.
Virtual memory is a memory management technique that gives an application the illusion of having a large, continuous block of memory,
### 3.Differentiate between physical memory and virtual memory.
Physical memory refers to the actual RAM hardware installed in a computer, which stores data and instructions for running programs. It has a limited size and is accessed via physical addresses.

Virtual memory, on the other hand, is an abstraction provided by the operating system that allows programs to use more memory than physically available by combining RAM with disk storage (swap space). It provides each process with its own virtual address space,
### 4.What is the role of an operating system in memory management?

The OS acts as a memory manager that allocates, protects, tracks, and optimizes memory usage to ensure smooth multitasking and system stability.
### 5.Explain the purpose of memory allocation.
| Purpose                     | Explanation                                           |
| --------------------------- | ----------------------------------------------------- |
| Provide usable memory       | Assign memory to hold variables, data, code           |
| Optimize resource usage     | Allocate only what is needed, avoid wastage           |
| Enable dynamic memory usage | Allow programs to request/release memory dynamically  |
| Ensure memory safety        | Avoid overlap or corruption between processes or data |
| Support program flexibility | Handle variable-sized data during execution           |

6.Describe the significance of memory deallocation.
| Significance                | Explanation                                     |
| --------------------------- | ----------------------------------------------- |
| Prevents memory leaks       | Releases unused memory to avoid exhaustion      |
| Improves performance        | Enables reuse of memory, maintaining efficiency |
| Ensures stability           | Prevents crashes from invalid memory access     |
| Supports dynamic allocation | Allows flexible memory usage during execution   |
| Reduces fragmentation       | Helps maintain contiguous memory regions        |


### 7.Define fragmentation in memory management.
Fragmentation occurs when free memory is broken into small, non-contiguous blocks scattered throughout the memory, making it difficult to allocate large contiguous blocks of memory even if enough total free memory exists.

### 8.What are the types of fragmentation?
two types 
### 9.Explain internal fragmentation.
Occurs when allocated memory blocks are larger than needed, causing wasted space inside the allocated block.
### 10. Explain external fragmentation.
Free memory is divided into small scattered chunks outside allocated memory blocks, so large requests may fail despite sufficient total free memory.
### 11. How is fragmentation managed in memory allocation?
### 12. Describe the concept of paging.
### 13. Explain segmentation.
### 14. What is the difference between paging and segmentation?
15. Define page table.
16. Define Memory Management Unit (MMU).
17. Explain the role of MMU in memory managem
18.Describe the translation lookaside buffer (TLB).
19. What is TLB miss? How is it handled?
20. Discuss the working principle of MMU.
21. Explain the concept of address translation in MMU.
22. How does MMU support virtual memory?
23. Describe the process of page table traversal in MMU.
24. What is page fault handling in MMU?
25. Explain the page replacement algorithms used in MMU.
26. Define page replacement algorithms.
27. Describe the FIFO page replacement algorithm.
28. Discuss the optimal page replacement algorithm.
29. Explain the LRU (Least Recently Used) page replacement algorithm.
30. What is the clock page replacement algorithm?
31. Discuss the advantages and disadvantages of each page replacement algorithm.
32. Compare and contrast different page replacement algorithms.
33. Explain the working of the NRU (Not Recently Used) page replacement algorithm.
34. Describe the working of the Second Chance page replacement algorithm.
35. Discuss the enhancements to basic page replacement algorithms.
36. Define segmentation in memory management.
37. Explain the benefits of segmentation.
38. What are the disadvantages of segmentation?
39. Describe the implementation of segmentation.
40. Discuss segmentation fault and its causes.
41. Explain the concept of segment registers.
42. What is a segment table?
43. How does segmentation support protection and sharing of memory?
44. Discuss the segmentation with paging approach.
45. Compare and contrast segmentation with paging.
46. Define memory fragmentation.
47. Explain the causes of memory fragmentation.
48. How does memory fragmentation affect system performance?
49. Discuss the techniques to reduce memory fragmentation.
50. Explain compaction as a technique for reducing fragmentation.
51. What is memory compaction?
52. Describe the working of memory compaction algorithms.
53. Discuss the challenges in implementing memory compaction.
54. Explain memory fragmentation in the context of embedded systems.
55. How does memory allocation impact memory fragmentation
56. Define memory mapping.
57. Explain the purpose of memory mapping.
58. Describe the memory mapping techniques.

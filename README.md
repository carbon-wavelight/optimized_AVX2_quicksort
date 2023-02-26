# optimized_AVX2_quicksort
A quicksort using SIMD instructions to optimize performance.

This is just a fun experiment to see what can be achieved pulling out all the stops. This project is still a work in progress.

There's a temporary generic sort in there just to check if the rest of the code works until I figure out how to get the SIMD instructions to behave with arrays not in multiples of 8. Also I'm pretty sure there's something wrong with the mask calculations. 

Proper decription (also found in main.rs):

It uses AVX2 SIMD instructions to perform partitioning.
 - The avx2_partition function takes a mutable slice of 32-bit integers and a pivot value, and uses SIMD instructions to partition the slice into two sub-slices: one with elements less than the pivot, and one with elements greater than or equal to the pivot. 
 - The function makes use of AVX2 instructions like _mm256_cmpgt_epi32 and _mm256_movemask_ps to extract the comparison results from the SIMD registers and update the indices for the two sub-slices. Ideally.

 - It uses loop unrolling and prefetching to reduce memory latency and improve cache utilization. 
 - The quicksort function checks the length of the slice and decides whether to use Quicksort or a simple insertion sort for small arrays. 
 - For larger arrays, it selects the pivot value and partitions the array using the avx2_partition function. It then recursively sorts the two sub-slices using Quicksort.
- To improve performance, the function unrolls the recursion loop and prefetches data into the CPU cache, reducing memory latency and improving cache utilization.

Why use unsafe? This program uses unsafe to directly manipulate memory and call CPU-specific instructions. 
 - The avx2_partition function uses unsafe Rust to directly load and store data from memory using AVX2 instructions. 
 - It also uses the unreachable_unchecked function to indicate to the compiler that a particular code path is unreachable, allowing it to generate more efficient machine code.

- This implementation is highly optimized for performance, but it also makes use of advanced features and techniques that may not be appropriate or safe in all contexts.

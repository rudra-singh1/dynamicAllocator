# Dynamic Memory Allocator

This project implements a custom dynamic memory allocator in C, similar to the malloc() and free() functions in the standard C library.

## Features

- Explicit free list implementation for efficient memory management
- First-fit allocation strategy
- Immediate coalescing of free blocks
- Boundary tag coalescing for O(1) time free operation
- Optimized for both space utilization and throughput

## Implementation Details

The allocator uses the following key data structures and algorithms:

- `block_info` struct to represent heap blocks, containing size/tag info and free list pointers
- Explicit free list with LIFO insertion policy  
- Boundary tags in both allocated and free blocks to enable efficient coalescing
- First-fit search for finding free blocks
- Splitting of large free blocks to reduce internal fragmentation
- Immediate coalescing of adjacent free blocks on free operations

Key functions:

- `mm_init`: Initialize the allocator
- `mm_malloc`: Allocate a block of memory  
- `mm_free`: Free an allocated block
- `coalesce_free_block`: Merge adjacent free blocks
- `request_more_space`: Expand the heap when necessary

## Usage

The allocator can be used as a drop-in replacement for malloc/free:

```c
#include "mm.h"

int main() {
  mm_init();
  
  int *arr = (int*)mm_malloc(10 * sizeof(int));
  
  // Use allocated memory
  
  mm_free(arr);
  
  return 0;
}
```

## Building and Testing

A Makefile is provided to build the allocator and run tests:

```
make         # Build allocator
make check   # Run tests
```

The test driver (`mdriver`) runs the allocator through a series of trace files to check correctness and measure performance.

## Performance 

The allocator aims to balance space utilization and throughput. On the provided trace files, it achieves:

- Space utilization: ~75%
- Throughput: ~80% of libc malloc

## Future Improvements

Potential areas for optimization:

- Segregated free lists
- Better splitting heuristics  
- Deferred coalescing



# Stack & Heap

## Links

- [Intro](https://web.mit.edu/rust-lang_v1.25/arch/amd64_ubuntu1404/share/doc/rust/html/book/first-edition/the-stack-and-the-heap.html)
- [YT](https://www.youtube.com/watch?v=N3o5yHYLviQ)

## Stack

What is the stack? (Execution Stack / Program Stack / Hardware Stack)

- LIFO -> last element put in the stack is the first one to be removed
- Very Fast
- But limited in size -> Stack Overflow

Compact data is crucial for:

- Efficient memory usage by avoiding external fragmentation
- Cache performance by increasing the probability of cache hits (CPU cache)

Predictable behavior (known size of data):

- Fast allocation time
- Easy to handle function calls and local data

But:

- Large data can cause stack overflow
- Fix size
- No dynamic size types
- Single Threaded (solved by the use of the heap)

The operating system (OS) acts an intermediary between the program and the hardware. It acts as a ressource manager, allocating memory to the program.

When a program runs, it can't by itself interact with the hardware and the memory. It needs to ask the OS to allocate memory for it.

The OS doesn't allocate memory for the program directly. Instead, it allocates memory for the program to use. The program can then use this memory to store data.

If there's enough free memory, but no contiguous block of memory large enough to satisfy the request, the OS will refuse the request. This is called **external fragmentation**.

In that case, the program needs to request more memory from the OS.

The OS will then look for a contiguous block of memory large enough to satisfy the request. If it finds one, it will allocate it to the program.

However, memory is finites, if no more memory available, it will use storage space as additional memory (swap space in Linux) -> Virtual Memory

But this memory is much slower than RAM.


Modern CPU have a special memory called Cache. A small dedicated memory, where a copy of memory region is stored, that is much faster than RAM.

When the CPU requires data, it can first check the cache. If the data is there, it can be retrieved much faster (Cache HIT) than if it had to be retrieved from RAM (Cache MISS).

The hardware decides what is stored in the cache and what is not. The hardware can also decide to evict data from the cache to make room for new data.

By having data stored in memory, in a compact form, increases the chances that the data will be in the cache when the CPU needs it. -> Increase probability of Cache HIT

The concept of keeping data as close to the CPU as possible is called **Locality of Reference**.

To keep data compact, a good way is to use the stack.

By pre-allocating data when the program starts, the OS can guarantee that the data will be stored in a contiguous block of memory.

But the size is limited, some MBs.


When a program starts, the main function is called. The main function is pushed onto the stack.

When a variable is called variable is pushed onto the stack.

When a function is called, the function and its arguments are pushed onto the stack.

When a function returns, the function and its arguments are popped off the stack and the stack pointer is moved back to where it was before the function was called.

To allocate memory on the stack, we need to get the stack pointer. Stack pointer is a register in the CPU that points to the top of the stack.

When working with stack, we need to be careful with the size of the data we are storing. Let's imagine we have an array of 3 elements, and we want to store it on the stack. We then declare other variables, but then push a new value into the array. This will overwrite the other variables, because the stack pointer will move to the new position. This is why the compiler will complain if the size of the array is not specified, or pre-allocated.


This process is different when allocating memory on the heap.


## Heap

Performance penalties:

- Allocations require searching available subregions within the heap
- Allocation may require System call

Runtime erros:

- Memory leaks
- Null pointers dereferencing
- Dangling pointers

But:

- Large memory Allocations
- Dynamic size types
- Fast accessing times if used correctly (what is slow is the allocation process, not the access to the data itself)


In the stack, we can't store large data or resize data. This is where the heap comes in.


When a process starts, the CPU knows its state, and store it in a register. The register carries the state of our processes.

When a process makes a system call, a request is made to the OS, it required the CPU to serve the request. 

To avoid modifying the register when serving a request, the register must be stored (as a copy) in the memory. This is called a **context switch**. This allow to restore the state of the process when the request is done or resume execution of a previously saved state.

But context switch is slow and takes time and memory. This is why we want to avoid it as much as possible.


Contrary to the stack, the heap as no size limit. It can grow as much as the memory allows it.

The way the memory of a process is organized is called "Memory Layout".

The memory layout of a process is divided into several sections:

- **Text**: The code of the program
- **Data**: The global and static variables
- **Heap**: The dynamic memory allocation
- **Stack**: The local variables and function calls

When the program requests memory to the OS, the OS will response with a chunk of memory. 

When storing data, the data itself is stored in the heap, but the pointer to the data is stored in the stack.

If data must be stored and enough memory is available, not system call is made. The memory is allocated and the pointer is stored in the stack.

The main difference between the stack and the heap is that for the stack, we know that the data will be stored in a contiguous block of memory, whereas for the heap, even if at first, the data is stored in a contiguous block of memory, when data is being removed, it can create holes in the memory. This is called **fragmentation**.

The data in the heap cannot be stored in a predictable way, similar to the stack.


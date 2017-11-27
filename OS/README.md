In C, statically-allocated variables without an explicit initializer are initialized to zero
or a null pointer. Implementations of C typically represent zero values and null pointer values
 using a bit pattern consisting solely of zero-valued bits.

 Hence, the bss (block started by symbol/block storage segment) section typically includes
 all uninitialized variables declared at the file level (outside of any function) as well as
 uninitialized local variables declared with the static keyword.

 Data region stores global/static variables.

When we start a C++ program, the compiler sets aside memory for our code (code storage or text storage), and the
compiled assembly resides in the Code segment.


- The heap manager selects an area of memory to use to satisfy the request, marks that area as in use in its private data
structures, and returns a pointer to the heap block. The new owner is responsible for setting the
memory to something meaningful. Sometimes there is variation on the memory allocation function
which sets the block to all zeros (calloc() in C).

- Each block should only be deallocated once.

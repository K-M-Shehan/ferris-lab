# Ownership

In rust memory is managed through a system of ownership.

Ownership has a set of rules and a program must comply to all the rules in order to compile.

Ownership features won't slow down the program while running.

## Stack and Heap

Stack: 
- stores values in the order it gets them, removes stuff in the opposite order. (LIFO)
- data stored must be of fixed size

Heap:
- uses pointers to store values, this pointer has a fixed size therefore it is stored in the stack

Ownership is needed to:
- keep track of what parts of code are using what data on the heap
- minimize the amount of duplicate data on the heap
- clean up unused data on the heap so that you don’t run out of space

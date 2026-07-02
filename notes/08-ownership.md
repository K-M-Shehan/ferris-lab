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

## Ownership rules
- each value has an owner
- there can only be one owner at a time
- when the owner goes out of scope the value will be dropped

## Strings
`String` can be mutated but literals cannot.

So to support a mutable with `String`, we must need:
- the memory to be requested from the memory allocator at runtime and,
- a way of returning this memory to the allocator when we're done iwht our `String`

We do the request with `String::from`.

Freeing the allocated memory is done automatically when the variable goes out of scope, but we can also do it manually with the function, `drop`.

Rust calls `drop` automatically at the closing curly brace.

## Complex situations

```rust
let s1 = String::from("hello");
let s2 = s1;
```

This may look simple at first but, its quite the opposite. `s1` here is not just a value, it has a pointer, length, and capacity.

Therefore when we say `s2 = s1`, we are copying the pointer, length and capacity to `s2`, not the stuff stored in the heap. 

Now this may not seem like a problem at first but, think about this, what happens when these 2 go out of scope, they will try to free the same allocated memory twice!

This is known as a double free error.

Freeing memory twice can lead to memory corruption.

To ensure memory safety, after `let s2 = s1`, rust considers `s1` as no longer valid.

So in such a situation, when a copy is made and the original is invalidated, in rust its called a move.

## Cloning

In the instance where we need to get a copy of the heap data as well as the stack, we can use the common method called `clone`.

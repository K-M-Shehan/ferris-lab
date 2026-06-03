# Functions

Just like they are in C.

```rust
fn main() {
    println!("Hello, world!");

    another_function();
}

fn another_function() {
    println!("Another function.");
}
```

Rust doesn't care where you define your functions like C, so you don't need to put a signature on top.

## Expressions
```rust
fn main() {
    let y = {
        let x = 3;
        x + 1
    };

    println!("The value of y is: {y}");
}
```

In rust the return value of a function is equivalent to the value of the final expression in the block. Still you can return early as well with the `return` keyword.

```rust
fn five() -> i32 {
    5
}

fn main() {
    let x = five();

    println!("The value of x is: {x}");
}
```

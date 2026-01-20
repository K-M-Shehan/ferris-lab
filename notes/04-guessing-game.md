# Programming a guessing game

We must first make a project, we can do that with cargo.

Then we edit the main file:
```rust
use std::io;

fn main() {
    println!("Guess the number!");

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {guess}");
}
```

```rust
use std::io;
```

This is like the header files that you would import in C. We are importing the io library.

By default, Rust has a set of items defined in the standard library that it brings into the scope of every program. This set is called the prelude. If a type you want to use isn’t in the prelude, you have to bring that type into scope explicitly with a use statement.

```rust
    let mut guess = String::new();
```
This is how we crate a variable to store stuff. We use the `let` statement to crate the variable.

```rust
let luffy = 56;
```

In rust variables are *immutable* by default, which means that once we give the variable a value, the value won't change.

To make a variable mutable we can add `mut` before the variable name as we did in the guessing game code.

> String is a string type provided by the standard library that is a growable, UTF-8 encoded bit of text.

The :: syntax in the ::new line indicates that new is an associated function of the String type. An associated function is a function that’s implemented on a type, in this case String.

## User input
```rust
    io::stdin()
        .read_line(&mut guess)
```

If we didn't import the io module with use at the start, we can still use the function by writing the function as `std::io::stdin`.

The full job of read_line is to take whatever the user types into standard input and append that into a string (without overwriting its contents).

The `&` is a reference, similar to how they are used in C for pointer references.

## Error handling
```rust
        .expect("Failed to read line");
```

Aside from storing the input, read_line() would also returns an enum, which is a type that can be in one of multiple possible states. We call each possible state a variant. The purpose of these Result types is to encode error-handling information.

The result variants will be `Ok` and `Err`, in the Err case we should use an expect (similar to try and catch in java) to do something in that case. If the result is `Ok` then it returns a value, in this case its the number of bytes in the user's input.

## Printing values

```rust
    println!("You guessed: {guess}");
```

When printing the result of evaluating an expression, place empty curly brackets in the format string, then follow the format string with a comma-separated list of expressions to print in each empty curly bracket placeholder in the same order. 

Very similar to C, in which we use `%`, but here we don't have letters.


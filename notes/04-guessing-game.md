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

## Random numbers

Now for the guessing game to be playable we must get a random number. For that we need an external library, in rust we call these things crates. We can import crates with cargo, by simply adding them to the toml file.

```toml
[dependencies]
rand = "0.8.5"
```

Then we build to get the packages.

---

Your project will remain at 0.8.5 until you explicitly upgrade, thanks to the Cargo.lock file.

---

To update crates you can use the command:

```bash
cargo update
```

### Using rand

```rust
use std::io;

use rand::Rng;

fn main() {
    println!("Guess the number!");

    let secret_number = rand::thread_rng().gen_range(1..=100);

    println!("The secret number is: {secret_number}");

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {guess}");
}
```

The `Rng` trait defines methods that random number generators implement, and this trait must be in scope for us to use those methods.

```rust
use std::cmp::Ordering;
use std::io;

use rand::Rng;

fn main() {
    // --snip--

    println!("You guessed: {guess}");

    match guess.cmp(&secret_number) {
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => println!("You win!"),
    }
}
```

The Ordering type is another enum and has the variants Less, Greater, and Equal. 

A match expression is made up of arms. An arm consists of a pattern to match against, and the code that should be run if the value given to match fits that arm’s pattern.

The above code doesn't compile due to mismatched types so we do this:
```rust
    // --snip--

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    let guess: u32 = guess.trim().parse().expect("Please type a number!");

    println!("You guessed: {guess}");

    match guess.cmp(&secret_number) {
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => println!("You win!"),
    }
```

Finally we must loop through so that the user can guess multiple times.

```rust
    // --snip--

    println!("The secret number is: {secret_number}");

    loop {
        println!("Please input your guess.");

        // --snip--

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => println!("You win!"),
        }
    }
}
```

We must also add a feature that would allow users to quit after a correct guess.

```rust
        // --snip--

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => {
                println!("You win!");
                break;
            }
        }
    }
}
```

We just added a break statement to break the loop just like we do in C.

Now finally we must handle invalid output.

```rust
        // --snip--

        io::stdin()
            .read_line(&mut guess)
            .expect("Failed to read line");

        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_) => continue,
        };

        println!("You guessed: {guess}");

        // --snip--
```

Here we just ignore an input which is not a number and go to the next guess, without crashing.

# Variables and Mutability

Variables are immutable by default in rust.

```rust
let x = 5
```

However you can make your variables mutable as well.

```rust
let mut x = 5
```

## Constants
Similar to immutable variables, cannot change after initialized once.

```rust
const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
```

Constants can be declared in any scope.

The compiler is able to evaluate a limited set of operations at compile time, which is how we did the small expression in the constant and didn't just write 10800. This is better for readability.

## Shadowing
A weird thing, is that you can declare a new variable with the same name as the previous variable. 

The first variable is shadowed by the second one.

```rust
fn main() {
    let x = 5;

    let x = x + 1;

    {
        let x = x * 2;
        println!("The value of x in the inner scope is: {x}");
    }

    println!("The value of x is: {x}");
}
```

A big difference between this and a mutable variable is that you can change the datatype of the variable when you overshadow it (crazy).

```rust
    let spaces = "   ";
    let spaces = spaces.len();
```

So if we try to do this with a mutable variable instead we will get a compile-time error.

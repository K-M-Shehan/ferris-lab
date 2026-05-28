# Data Types

There are 2 data subsets:
1. Scalar
2. Compound

## Scalar types
1. integers
2. floats
3. booleans
4. characters

### Integers
There are different types of integers as well.

Each signed variant can store numbers from −(2n − 1) to 2n − 1 − 1 inclusive, n here is the number of bits that variant uses.

### Floats

There are 2 types of floats `f32` and `f64`.

The default is `f64`.

All floats are signed.

### Boolean

```rust
fn main() {
    let t = true;

    let f: bool = false; // with explicit type annotation
}
```

They are 1 byte big.

### Character

In rust we write characters with single quotations.

A char is 4 bytes big.

## Compound types

So these are the types that can group mutitple values together.

There are 2 types.

### Tuples

Have fixed length.

```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```

#### Destructuring a tuple
This is when we want to extract the info inside a tuple.

```rust
fn main() {
    let tup = (500, 6.4, 1);

    let (x, y, z) = tup;

    println!("The value of y is: {y}");
}
```

Tuples are zero-indexed so you can also access them with a dot operator.

```rust
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);

    let five_hundred = x.0;

    let six_point_four = x.1;

    let one = x.2;
}
```

A tuple without values is called a unit.

### Arrays

Here every element must be of the same type.

Arrays have fixed length.

```rust
fn main() {
    let a = [1, 2, 3, 4, 5];
}
```

Stuff stored in an array lives in the stack, different from a `vector`, which is re-sizable, as it stores its elements in the heap.

```rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
```

Accessing elements in an array is the same as other programming languages.

```rust
fn main() {
    let a = [1, 2, 3, 4, 5];

    let first = a[0];
    let second = a[1];
}
```

If you try to access out of bounds you will get a run-time error, unlike in C where it just spits out garbage values.

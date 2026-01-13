# Hello world

Here we just learn to run our first program, which is to print hello world to the terminal.

We do this by writing this:

```rust
fn main() {
    println!("Hello world!");
}
```

Do note that rust also ends its lines with a semi colon.

We have a main function too similar to C (which is actually the first language I learnt).

The main function is always the first code that runs in every executable rust program.

The functions body is also wrapped by curly braces just like C.

`println!` calls a rust macro, but what is a rust macro? Coming in later notes...

If a function were to be called instead of a macro we would just write `println()` without the exclaimation mark.

Macros don't always follow the same rules as functions.

The stuff inside quotations is a string (same as many other langs).

Do note that we must compile a rust program to make an executable, so rust is not intepreted like python, its an ahead-of-time compiled language, this means that you can compile a program  and give the executable to someone else and they can run it even without having rust installed, so this is a little different from C as well, cause in C we must compile it again for someone else to use the exe.

Rustc is used for simple and small programs, as projects grow we must manage all the options to make it easy to share our code.

And as usual running the program prints the words "Hello world!" to your terminal.

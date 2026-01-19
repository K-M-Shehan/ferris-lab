# Cargo

Cargo is a build system and package manager.

You can create a project with cargo as such:
```bash
cargo new hello_cargo
```

This creates a new directory in which you would find a toml file which is cargo's config format.

All the source code will be placed inside the src sub directory, and the parent will house all the README.mds and other complimentary files like the LICENSE and etc.

We can also manually create a project, to do this we must run:
```bash
cargo init
```

Similar to `git init`, this will create the toml file and we can get started with out work.

## Building & running a cargo project

```bash
cargo build
```

With this we can build the project, this command creates an exe in the target/debug/hello_cargo rather than the current directory the command is being entered in. Because the default build is a debug build, Cargo puts the binary in a directory named debug.

To run:
```bash
./target/debug/hello_cargo
```

If it builds properly, we must get a "Hello, world!", printed in the terminal.

> Cargo will create a Cargo.lock file when running the build command for the first time.

The Cargo.lock file keeps track of the exact versions fo dependencies in the project.

The command I mentioned before is a more manual approach to running the project, as we can also `cargo run` to compile the code and run the resultant exe all in one command so its two commands in one.

There is also a command called `cargo check`, which can check whether the code can be compiled and doesn't produce an exe.

When your project is finally ready for release, you can use `cargo build --release` to compile it with optimizations. This command will create an executable in target/release instead of target/debug.

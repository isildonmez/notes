## 1. Getting Started

    $ rustc --version
    $ rustup update
    $ rustup self uninstall


    $ rustc main.rs // compiling
    $ ./main // running


    $ rustup component add rustfmt
    $ cargo fmt // cargo is Rust's build system and package manager.


    println!("Hello, world!")

notice `!` that means it's calling a macro instead of normal function. Macros don't always follow the same rules as functions. More in Chapter 19.

    $ cargo new hello_cargo

It creates a new directory and project called hello_cargo and creates its files in a directory of the same name.

    $ cargo build
creates an executable file in target/debug/hello_cargo. Cargo puts the binary in a directory named debug.

To run the executable:

    ./target/debug/hello_cargo
    Hello, world!

We can also use

    `$ cargo run` 
to build and run in one go.

    `$ cargo check`
to quickly check and make sure the code compiles, but doesn't produce an executable.

    $ cargo build --release
to compile it with optimizations. Creates an executable in *target/release* instead of *target/debug*
When benchmarking your code's running time, run `cargo build --release` and benchmark with the executable in target/release.

to work on any existing projects

    $ git clone example.org/someproject
    $ cd someproject
    $ cargo build


## 2. Programming a Guessing Game:

    let apples = 5; // immutable
    let mut bananas = 5; // mutable

    let x = 5;
    let y = 10;

    println!("x = {} and y = {}", x, y);
    // will print x = 5 and y = 10

`crate` is a collection of Rust source code files. This project is a *binary crate*, which is an executable. The e.g. `rand` crate is a *library crate*, which contains code intended to be used in other programs and can't be executed on its own.

    // Filename: Cargo.toml
    rand = "0.8.3"

Cargo understands Semantic Versioning (sometimes called *SemVer*), which is a standard for writing version numbers. The number `0.8.3` is actually shorthand for `^0.8.3`, which means any version that is at least `0.8.3` but below `0.9.0`

When we include an external dependency, Cargo fetches the latest versions of everything that dependency needs from the *registry*, which is a copy of data from `Crates.io`. Crates.io is where people in the Rust ecosystem post their open source Rust projects for others to use. After updating the registry, Cargo checks the `[dependencies]` section and downloads any crates listed that aren’t already downloaded.

    cargo update

It will ignore the *Cargo.lock* file and figure out all the latest versions that fit your specifications in *Cargo.toml*. Cargo will then write those versions to the *Cargo.lock* file. Otherwise, by default, Cargo will only look for versions greater than `0.8.3` and less than `0.9.0`.

    let secret_number = rand::thread_rng().gen_range(1..=100);

When we call the `rand::thread_rng` function that gives us the particular random number generator that we’re going to use: one that is local to the current thread of execution and seeded by the operating system.

    cargo doc --open

This command will build documentation provided by all of your dependencies locally and open it in your browser.

    match guess.cmp(&secret_number) {
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => println!("You win!"),
    }

A `match` expression is made up of *arms*. An arm consists of a pattern to match against, and the code that should be run if the value given to `match` fits that arm’s pattern. Rust takes the value given to `match` and looks through each arm’s pattern in turn.
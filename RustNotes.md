Date created: 01/01/2025
By: Gabriel Baje

## What is Rust?
- Rust is a systems programming language that focuses on **performance**, **memory safety**, and **safe concurrency**.

### Key Features of Rust
- Memory Safety without Garbage Collection
- Ownership, Borrowing, and Lifetimes
- Zero-Cost Abstractions
- Concurrency and Parrallelism
- Trait System and Pattern Matching
- Pattern Matching
- Functional and imperative paradigms
- Crates and Package Management
- No Null or Undefined Behaviour
- Cross-Platform Compatibility
- Ecosystem and Community
- Compiled Language

### Rust Development Environment
- `cargo`: the Rust package manager.
- `rustc`: the Rust compiler is sometimes invoked by cargo since your code is also treated as a package.
- `rustdoc`: the Rust documentation tool for documenting comments in Rust code.

## Building with Rust

### The structure of Rust Projects
- The important parts of a Rust project are seen when we use Cargo to initialize a new project.
	eg: 
```bash
	cargo new example
```
- `cargo.toml`: stores metadata for the package.
- `.gitignore`: stores files that Git should not track.
- `src/main.rs`: The `src/` subdirectory is where all Rust code is normally written. The `main.rs` file is the entry point for all binary crates.

### Understanding the basic syntax and structure

- Rust's `main` function can behave like every other function by accepting and returning values.
- Comments for the documentation are made with the double forward slash: `//`.
-  The `->` symbol is how you specify return values.
	eg(main function):

```rust
	fn main() -> () {
		let x = 5;
		println!("The value of x is {}", x);
	}
```

## Variable and data types in Rust
### Variables
- `mut` keyword stands for mutable when creating a variable. This allows a variable to be reassigned without initializing it.

### Data types

#### Numeric Types
- Integer types
- Floating-point types
- Machine-dependent integer types

#### Textual types

Under **Textual types**, you should find characters `char` and `str`. They are created like this:

```rust
	fn main() -> (){
		let single_alphabet = "a";
		println!('The single chracter is: {}', single_alphabet);

		let second_alphabet: char = 'b';
		println!("The single character with type inference is {}", second_alphabet);
	}
```

```rust
	fn main() -> (){
	

    let my_string = "hello world";

    println!("The string is : {}", my_string);



    let second_string: &str = "Hello, other world";

    println!("The string contnt with the type reference is: {}", second_string);
}
```
Notice the ampersand (&) we used during the _type inferred_ variable `second_string`.

Non-complicated way to create strings in Rust is to use automatic dynamically sized `String` keyword:

```rust
	fn main() -> (){
		let another_string = String::from("Hello, world");
		println!("The string is: {}", another_string);

		let new_string: String = String::from("Hey, world!");
		println!("The type inferred string content is: {}", new_string);
}

```

#### Sequence types
- In Rust, sequential typesrefer to data structures that store a sequence of values in a specific order.

- Arrays

```rust
	//Declaration and initialization of an array
	let numbers: [i32, 5] = [1, 2, 3, 4, 5];
```

- Slices
Slices are references to a contiguous sequence of elements within another sequential type (like an array or a vector).

```rust
	let numbers = [1, 2, 3, 4, 5];
	let slice: &[i32] = &numbers[1..4];
```

- Vectors

Vectors are dynamic arrays that can grow or shrink in size.

```rust
	// Creating and modifying a vector
	let mut vec = Vec::new();
	vec.push(1);
	vec.push(2);
	vec.push(3);
```

- Strings
Rust's `String` type is dynamically sized, UTF-8 encoded string.

```rust
	let mut text = String::from("Hello, ");
	text.push_str("world!");
```

- Ranges
Ranges are sequential types reoresenting a sequence of values from a start value to an end value.

```rust
	for number in 1..5 { // Inclusive range (1 to 5 inclusive )
	println!("Current number: {}", number);
				
}
```

- Tuples

Tuples are collections of values of different types, and they have a fixed size that's determined at compile time.

```rust
	// Creating tuples
	let person: (String, i32, bool) = ("Alice".to_string(), 30, true);
	// Accessing tuple elements
	let name = person.0; 	// Access the first element (name)
	let age = person.1; 	// Access the second element (age)
	let is_adult = person.2;// Access the third element (is_adult)	
```

## Functions and Modules in Rust

### Functions
#### Function with No Return Statement or Argument:
```rust
	fn greet(){
		println!("Hello, world!");
}
```

#### Function with Argument and No Return Statement:
```rust
	fn say_hello(name: &str){
		println!("Hello, {}!", name);
	}
```
- Here, the `say_hello` function takes a single argument of type `&str` (a string slice) and prints personalized greeting using that argument.	

#### Function with Argument and Return Statement:

```rust
	fn square(n: i32) -> i32 {
		n*n
}
```

- In the above example, the `square` function takes an `i32` argument and returns the square of that argument as an `i32`.

#### Function with Multiple Arguments and Return Statements:
```rust
	fn calculate_power(base: f64, exponent:i32) -> f64{
		if exponent == 0{
		1.0
		}else{
			let mut result = base;
			for _ in 1..exponent.abs(){
				result*= base;
						}
				if exponent < 0{
					1.0 / result
				}else{
					result
				}			
			}
							
}
```

The `calculate_power` function takes a `base` of type `f64` and an `exponent` of type `i32`. 

### Modules

Generally, breaking down function into different modules in a growning code base is best.

We can do this in Rust by leveragin the `mod.rs` file, a specially recognized and reserved file for Rust projects. Inside the `src/` directory, you can also have other subdirectories called modules. Using them in the project must be linked to the `main.rs` or `lib.rs` file.

Here's how you can work with modules in Rust. Inside the `src/` directory, create a new directory called database. In it, create a `mod.rs` file and a `model.rs` file. The `mod.rs` file gives visibility to other files in the subdirectory under the `src/` directory. To practically understand this, add the following code to the specfified files.

`mod.rs`:
```rust
	pub mod model;
```

`model.rs`:
```rust
	
pub fn create_user(name: &str, age: i32){
    
    println!("New user created: {} of age {}", name, age);

}
```

`main.rs`:
```rust
pub mod database; // make the database module availbale in this file.
pub use database::*; // give this file access to all public modules and their functions (*) inside of the database module.

fn main() {

	let name = "John";
	let age = 35;

	database::model::create_user(name, age);

}
```

Note that we are using a clean `main.rs` file. Run the code with cargo, and you should see:

```
    Finished dev [unoptimized + debuginfo] target(s) in 0.03s
     Running `target/debug/test_env src/main.rs`
New user created: John of age 35
```

- **Note**: In Rust, the double semicolon notation is used to call methods of a module/package. Since we already specified to use all public modules and their respective functions using this line `pub use database::*`, we can shorten the calling technique to this: `model::create_user(name, age)`.

We can also do this:

```rust
pub mod database;
pub use database::model::*;

fn main(){
	let name = "John";
	let age = 35;

	create_user(name, age);
}
```

Or this:

```rust
	pub mod database;
	pub use databse::model::create_user;
	// use on the create_user function from the model module in the database package.

fn main(){
	let name = "John";
	let age = 35;

	create_user(name, age);
}	
```







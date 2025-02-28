# Learning Resources :
- [ ] [A 10-minute lightning talk taking you from zero to Rust!](https://youtu.be/br3GIIQeefY?si=6V39a6fD_djz44cL)
- [ ] [A half-hour to learn Rust](https://fasterthanli.me/articles/a-half-hour-to-learn-rust)


# Basics :
Rust is a _statically typed_ language, which means that it must know the types of all variables at compile time.
Rust uses the term _panicking_ when a program exits with an error
Rust is an expression-based language.
In Rust, projects are typically classified into **binary** and **library** projects.

Binary Project 
- Produces an executable program, 
- output is a compiled binary file (e.g., .exe, ELF, or Mach-O)
Library Project 
- Produces reusable code (a library), 
- output is a .rlib (Rust library) or .so/.dll (dynamic library)

```
// to make a new binary project :
cargo init
```
---
```
// to run code :
cargo run
```
---
```rust
fn main() {
    // Statements here are executed when the compiled binary is called.
    // Print text to the console.
    println!("Hello World!");
}
```

## macro_rules!
macro system that allows meta programming. Instead of generating a function call, macros are expanded into source code that gets compiled with the rest of the program
```rust
// This is a simple macro named `say_hello`.
macro_rules! say_hello {
    // `()` indicates that the macro takes no argument.
    () => {
        // The macro will expand into the contents of this block.
        println!("Hello!")
    };
}

fn main() {
    // This call will expand into `println!("Hello!")`
    say_hello!()
}
```

## conditional :
```rust
fn main() {
	println!("{}", is_even(10));
}
  
fn is_even(num: i32) -> bool{
	if num%2 == 0 {
		return true;
	} else {
		return false;
	}
}
```

> Note: by default variables in rust are immutable therefore we are require to add `mut` to make them mutable i.e. variable

## loop : 
```rust
fn main() {
	println!("{}", fib(5));
}

fn fib(num: i32) -> i32 {
	let mut first= 0;
	let mut second= 1;
	
	if num == 1 {
		return 0;
	}
	if num == 2 {
		return 1;
	}
	
	for i in 0..(num-1) {
		let temp = second;
		second = second + first;
		first = temp;
	}
	return second;
}
```

## Strings :
```rust
fn main(){
	let str = String::from("hello");
	println!("{}", get_len_of_str(str));
}

fn get_len_of_str(s: String) -> usize {
	s.chars().count()
}
```
---
```rust
use std::io;
  
fn main() {
	println!("Guess the number!");
	
	println!("Please input your guess.");
	
	let mut guess: String = String::new();
	
	io::stdin()
		.read_line(&mut guess)
		.expect("Failed to read line");
	
	println!("You guessed: {}", guess);
}
```

## I/O :
```rust
use std::io;

fn main(){
	println!("Enter a number: ");
	let mut number:String = String::new();
	
	io::stdin()
		.read_line(& mut number)
		.expect("Failed to read line");
	
	println!("You entered: {}", number);
}
```
The `::` syntax in the `::new` line indicates that `new` is an associated function of the `String` type. An _associated function_ is a function that’s implemented on a type.

`read_line` puts whatever the user enters into the string we pass to it, but it also returns a `Result` value. `Result` is an _enumeration_, often called an _enum_ enums give you a way of saying a value is one of a possible set of values. enums give you a way of saying a value is one of a possible set of values.

> Example:
```rust
use std::io;
use std::cmp::Ordering;
use rand::Rng;

fn main(){
	println!("Enter a number: ");
	let mut guess:String = String::new();
	
	io::stdin()
	.read_line(&mut guess)
	.expect("Failed to read line");
	
	// Shadowing guess
	let guess:u32 = guess.trim().parse().expect("Please type a number!");
	
	println!("You entered: {}", guess);
	
	let mut rng = rand::rng();
	let secret_number = rng.random_range(1..=10);
	println!("Random number: {}", secret_number);
	
	match guess.cmp(&secret_number) {
		Ordering::Less => println!("Too small!"),
		Ordering::Greater => println!("Too big!"),
		Ordering::Equal => println!("You win!"),
	}
}
```
_Shadowing_ lets us reuse the `guess` variable name rather than forcing us to create two unique variables, such as `guess_str` and `guess`

## Data Types (fixed sized, stored in stack) :
_Shadowing_ example:
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

// OUTPUT
// The value of x in the inner scope is: 12 
// The value of x is: 6
```

**The types covered below are of a known size, can be stored on the stack and popped off the stack when their scope is over, and can be quickly and trivially copied to make a new, independent instance if another part of code needs to use the same value in a different scope.**
### Integer Types:
 the `isize` and `usize` types depend on the architecture of the computer your program is running on, which is denoted in the table as “arch”: 64 bits if you’re on a 64-bit architecture and 32 bits if you’re on a 32-bit architecture.
 
 > Integer Literal Notations:
```rust
let decimal = 42;        // Decimal (Base-10) 
let hex = 0x2A;          // Hexadecimal (0x prefix) 
let octal = 0o52;        // Octal (0o prefix) 
let binary = 0b101010;   // Binary (0b prefix) 
let byte = b'A';         // Byte literal (ASCII value of 'A' is 65)

println!("Decimal: {}", decimal); 
println!("Hex: {}", hex); 
println!("Octal: {}", octal); 
println!("Binary: {}", binary); 
println!("Byte: {}", byte);

// Decimal: 42
// Hex: 42
// Octal: 42
// Binary: 42
// Byte: 65
```

When you’re compiling in release mode with the `--release` flag, Rust does _not_ include checks for integer overflow that cause panics. Instead, if overflow occurs, Rust performs _two’s complement wrapping_. In short, values greater than the maximum value the type can hold “wrap around” to the minimum of the values the type can hold. In the case of a `u8`, the value 256 becomes 0, the value 257 becomes 1, and so on.

### Floating-Point Types:
All floating-point types are signed.
```rust
fn main() {
    let x = 2.0; // f64
    let y: f32 = 3.0; // f32
}
```

### Boolean Type:
Booleans are one byte in size.
```rust
fn main() {
    let t = true;
    let f: bool = false; // with explicit type annotation
}
```

### Character Type:
Rust’s `char` type is four bytes in size
```rust
fn main() {
    let c = 'z';
    let z: char = 'ℤ'; // with explicit type annotation
    let heart_eyed_cat = '😻';
}
```

### Compound Types:
Rust has two primitive compound types: tuples and arrays.

- **Tuple Type:** number of values with a variety of types into one compound type
	Tuples have a fixed length: once declared, they cannot grow or shrink in size.
	The tuple without any values has a special name, _unit_
	
	```rust
	fn main() { 
		let tup: (i32, f64, u8) = (500, 6.4, 1);
	}
	```
	
	destructuring tuple values:
	```rust
	fn main() {
	    let tup = (500, 6.4, 1);
		
	    let (x, y, z) = tup;
		
	    println!("The value of y is: {y}");
		
		let five_hundred = x.0; 
		let six_point_four = x.1; 
		let one = x.2;
	}
	```

- **Array Type:** multiple values of same data type
	```rust
	fn main() {
	    let a = [1, 2, 3, 4, 5];
	    let a: [i32; 5] = [1, 2, 3, 4, 5];
	    
	    let a = [3; 5]; 
	    // let a = [3, 3, 3, 3, 3];
	}
	```
	Accessing memory out of bound would result Rust to panic and would just exit the program instead of accessing random memory like C.

## Functions :
In function signatures, you _must_ declare the type of each parameter
- **Statements** are instructions that perform some action and do not return a value.
	Statements do not return values.
	Function definitions are also statements
	Creating a variable and assigning a value to it with the `let` keyword is a statement.
	
	```rust
	fn main() {
	    let x = (let y = 6);
	}
	// let y = 6 doesn't return anything
	// in C assignment return the value (like 6 here)
	
	// This is different from what happens in other languages, 
	// such as C and Ruby, where the assignment returns the value
	// of the assignment. In those languages, you can write 
	// `x = y = 6` and have both `x` and `y` have the value `6`; 
	// that is not the case in Rust.
	```
	
- **Expressions** evaluate to a resultant value. Let’s look at some examples.
	_calling_ a function is an expression as it return a value
	Calling a function is an expression. 
	Calling a macro is an expression. 
	A new scope block created with curly brackets is an expression.
	```rust
	fn main() {
	    let y = {
	        let x = 3;
	        x + 1
	    };
	
	    println!("The value of y is: {y}");
	}
	
	// The value of y is: 4
	```
	**Note** that the `x + 1` line doesn’t have a semicolon at the end, which is unlike most of the lines you’ve seen so far. Expressions do not include ending semicolons. If you add a semicolon to the end of an expression, you turn it into a statement, and it will then not return a value. 
	
	```rust
	fn main() {
	    let x = plus_one(5);
	    println!("The value of x is: {x}");
	}
	
	fn plus_one(x: i32) -> i32 {
	    x + 1;
	}
	
	// The definition of the function `plus_one` says that it will 
	// return an `i32`, but statements don’t evaluate to a value, 
	// which is expressed by `()`, the unit type. Therefore, nothing 
	// is returned, which contradicts the function definition and 
	// results in an error
	```

## Control Flow :
Blocks of code associated with the conditions in `if` expressions are sometimes called _arms_, just like the arms in `match` expressions
```rust
fn main() {
    let number = 3;
	
    if number {
        println!("number was three");
    }
}

// In C/C++ this would turn true but in Rust it
// results in an error as condition mustbe of a bool 
```

Because `if` is an expression, we can use it on the right side of a `let` statement to assign the outcome to a variable
```rust
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };
    
    println!("The value of number is: {number}");
}
```
---
```rust
fn main() {
    let condition = true;
    let number = if condition { 5 } else { "six" };
    println!("The value of number is: {number}");
}

// Would turn into an ERROR as number should have a fix data type
// as Rust can't have multiple hypothetical types
```

### loop:
```rust
fn main(){
	let counter = 0;
	let result = loop {
		counter +=1;
		
		if counter == 10 {
			break counter*2;	
		}
	}
	println!("The result is {result}");
}

// OUTPUT: The result is 20
// value after break statement is returned when break is encountered
```

### Loop Labels:
If you have loops within loops, `break` and `continue` apply to the innermost loop at that point. You can optionally specify a _loop label_ on a loop that you can then use with `break` or `continue`
Loop labels must begin with a single quote.
```rust
fn main() {
    let mut count = 0;
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;
		
        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }
		
        count += 1;
    }
    println!("End count = {count}");
}

// OUPTUT:
// count = 0
// remaining = 10
// remaining = 9
// count = 1
// remaining = 10
// remaining = 9
// count = 2
// remaining = 10
// End count = 2
```

### while:
```rust
fn main() {
    let mut number = 3;
	
    while number != 0 {
        println!("{number}!");
        number -= 1;
    }
	
    println!("LIFTOFF!!!");
}
```

### for:
```rust
fn main() {
    let a = [10, 20, 30, 40, 50];
	
    for element in a {
        println!("the value is: {element}");
    }
}
```
---
```rust
fn main() {
    for number in (1..4).rev() {
        println!("{number}!");
    }
    println!("LIFTOFF!!!");
}

// 3!  
// 2!  
// 1!  
// LIFTOFF!!!
```

# Ownership :
https://youtu.be/usJDUSrcwqI?si=Z6OBFP_ekKiwr7jq
Stack: All data stored on the stack must have a known, fixed size
Heap: When you put data on the heap, you request a certain amount of space. The memory allocator finds an empty spot in the heap that is big enough, marks it as being in use, and returns a _pointer_, which is the address of that location.

> A processor can do its job better if it works on data that’s close to other data (as it is on the stack) rather than farther away (as it can be on the heap).
### Ownership rules :
- Each value in Rust has an _owner_.
- There can only be one owner at a time.
- When the owner goes out of scope, the value will be dropped.

>So `string literals` are stored in stack, therefore even if a `string literal` is mutable it cannot be modified as it is stored in stack, but a mutable `String` type, which is used to store unknown size values like values entered during the runtime, is stored in heap and therefore can be modified. In the case of a string literal, we know the contents at compile time, so the text is hardcoded directly into the final executable. This is why string literals are fast and efficient. But these properties only come from the string literal’s immutability.

To allocate variable memory from heap for runtime values: 
- The memory must be requested from the memory allocator at runtime.
- We need a way of returning this memory to the allocator when we’re done with our `String` (most languages either use Garbage Collector that keep looking for disconnected node or ask us to manually free the memory).

> _**Rust takes a different path: the memory is automatically returned once the variable that owns it goes out of scope**_
```rust
{
	let s = String::from("hello"); // s is valid from this point forward
	// do stuff with s
}                                  // this scope is now over, and s is no
								   // longer valid
```
> _**When a variable goes out of scope, Rust calls**_ `drop` _**function, which works like free in C i.e. it frees the allocated space from memory.**_

### double free error :
```rust
    let s1 = String::from("hello");
    let s2 = s1;
```
![[Pasted image 20250225141155.png]]
Rust automatically calls the `drop` function and cleans up the heap memory for variable that goes out of scope. This is a problem: when `s2` and `s1` go out of scope, they will both try to free the same memory. This is known as a _double free_ error and is one of the memory safety bugs. Freeing memory twice can lead to memory corruption, which can potentially lead to security vulnerabilities.
Rust, to ensure memory safety, after the line `let s2 = s1;`, considers `s1` as no longer valid.
This is process is somewhat like a shallow copying but as original string is no longer valid it's called **`move`**.

> Rust will never automatically create “deep” copies of your data. Therefore, any _automatic_ copying can be assumed to be inexpensive in terms of runtime performance.

When you assign a completely new value to an existing variable, Rust will call `drop` and free the original value’s memory immediately. Consider this code, for example:
```rust
    let mut s = String::from("hello");
    s = String::from("ahoy");

    println!("{s}, world!");    // ahoy, world!
```
but what if we don't want to invalidate the original string/variable. We make a **`clone`** i.e. a deep copy of that variable. To make a **`clone`** is expensive
```rust
    let s1 = String::from("hello");
    let s2 = s1.clone();

    println!("s1 = {s1}, s2 = {s2}");
```

### Copy Trait :
Rust has a special annotation called the `Copy` trait that we can place on types that are stored on the stack (directly only and not indirectly)

Incase of variable size like a Vectors (`Vec<i32>`) their pointers are stored but that doesn't mean they have Copy trait as actual data is stored in heap 

A type with `Drop` trait can never have `Copy` trait

### Drop Trait :
Rust annotation that tells compiler that a type has custom drop function.

### Ownership in Functions :
Passing a variable to a function will move or copy, just as assignment does.
```rust
fn main() {
    let s1 = gives_ownership();         // gives_ownership moves its return
                                        // value into s1
                                        
    let s2 = String::from("hello");     // s2 comes into scope
    
    let s3 = takes_and_gives_back(s2);  // s2 is moved into
                                        // takes_and_gives_back, which also
                                        // moves its return value into s3
} // Here, s3 goes out of scope and is dropped. s2 was moved, so nothing
	// happens. s1 goes out of scope and is dropped.
	
fn gives_ownership() -> String {             // gives_ownership will move its
                                             // return value into the function
                                             // that calls it
	
    let some_string = String::from("yours"); // some_string comes into scope
	
    some_string                              // some_string is returned and
                                             // moves out to the calling
                                             // function
}
	
	// This function takes a String and returns one
fn takes_and_gives_back(a_string: String) -> String { // a_string comes into
                                                      // scope
    a_string  // a_string is returned and moves out to the calling function
}
```

But we can't taking ownership and then returning ownership with every function is a bit tedious. Rust has a feature for using a value without transferring ownership, called _references_.

# References and Borrowing :
A reference is like a pointer in that it’s an address we can follow to access the data stored at that address; that data is owned by some other variable. Unlike a pointer, a reference is guaranteed to point to a valid value of a particular type for the life of that reference.

```rust
fn calculate_length(s: &String) -> usize { // s is a reference to a String
    s.len()
} // Here, s goes out of scope. But because s does not have ownership of what
  // it refers to, the value is not dropped.
```
The scope in which the variable `s` is valid is the same as any function parameter’s scope, but the value pointed to by the reference is not dropped when `s` stops being used, because `s` doesn’t have ownership.
We call the action of creating a reference borrowing.
Just as variables are immutable by default, so are references.
### Borrowing rules : 
-  At any given time you can either have one mutable reference or any number of immutable reference
	The benefit of having this restriction is that Rust can prevent data races at compile time. A data race is similar to a race condition and happens when these three behaviors occur:
	1. Two or more pointers access the same data at the same time.
	2. At least one of the pointers is being used to write to the data.
	3. There’s no mechanism being used to synchronize access to the data.
	
	```rust
	let mut s = String::from("hello");

    let r1 = &mut s;
    let r2 = &mut s;

    println!("{}, {}", r1, r2);
	```
	
	```shell
	  |
	4 |     let r1 = &mut s;
	  |              ------ first mutable borrow occurs here
	5 |     let r2 = &mut s;
	  |              ^^^^^^ second mutable borrow occurs here
	6 |
	7 |     println!("{}, {}", r1, r2);
	  |                        -- first borrow later used here
	```
	We also cannot have a mutable reference while we have an immutable one to the same value.
	Users of an immutable reference don’t expect the value to suddenly change out from under them! However, multiple immutable references are allowed.
	```rust
	let mut s = String::from("hello");

    let r1 = &s; // no problem
    let r2 = &s; // no problem
    let r3 = &mut s; // BIG PROBLEM

    println!("{}, {}, and {}", r1, r2, r3);
	```
	
	>Note that a reference’s scope starts from where it is introduced and continues through the **last time that reference** is used.
	
	```rust
	let mut s = String::from("hello");
	
    let r1 = &s; // no problem
    let r2 = &s; // no problem
    println!("{r1} and {r2}");
    // variables r1 and r2 will not be used after this point
	
    let r3 = &mut s; // no problem
    println!("{r3}");
	```
	
- Reference must always be valid (i.e. referenced value must have long enough lifetime)
	In Rust, the compiler guarantees that references will never be dangling references: if you have a reference to some data, the compiler will ensure that the data will not go out of scope before the reference to the data does.
	```rust
	fn main() {
	    let reference_to_nothing = dangle();
	}
	
	fn dangle() -> &String { // dangle returns a reference to a String
	    let s = String::from("hello"); // s is a new String
	    &s // we return a reference to the String, s
	} // Here, s goes out of scope, and is dropped. Its memory goes away.
	  // Danger!
	```

### Slice Type :
_Slices_ let you reference a contiguous sequence of elements in a [collection](https://doc.rust-lang.org/book/ch08-00-common-collections.html) rather than the whole collection. A slice is a kind of reference, so it does not have ownership.
Unlike the built-in array and tuple types, the data these collections point to is stored on the heap, which means the amount of data does not need to be known at compile time and can grow or shrink as the program runs.
collection example vector, string, hash maps

```rust
// Example 1:
fn first_word(s: &String) -> usize {
    let bytes = s.as_bytes();
    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            return i;
        }
    }
    s.len()
}

fn main() {
    let mut s = String::from("hello world");
    let word = first_word(&s); // word will get the value 5
    s.clear(); // this empties the String, making it equal to ""
    // `word` still has the value `5` here, but `s` no longer has any content
    // that we could meaningfully use with the value `5`, so `word` is now
    // totally invalid!
}
```
This program compiles without any errors and would also do so if we used `word` after calling `s.clear()`. Because `word` isn’t connected to the state of `s` at all, `word` still contains the value `5`. We could use that value `5` with the variable `s` to try to extract the first word out, but this would be a bug because the contents of `s` have changed since we saved `5` in `word`.

Having to worry about the index in `word` getting out of sync with the data in `s` is tedious and error prone!
Rust has a solution to this problem: `string slices`.

### String Slices :
A string slice is a value that is made up of a reference to the starting point of the slice and the number of elements in the slice.
```rust
    let s = String::from("hello world");
    
    let hello = &s[0..5];
    let world = &s[6..11];
```

```rust
let s = String::from("hello");

let slice1 = &s[0..2];  
let slice2 = &s[..2];    // both slice1 and slice2 are same

let len = s.len();

let slice3 = &s[3..len];  
let slice4 = &s[3..];    // both slice3 and slice4 are same
```

```rust
// Rewrite Example 1 first_word function to return a slice
fn first_word(s: &String) -> &str {
    let bytes = s.as_bytes();

    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            return &s[0..i];
        }
    }

    &s[..]
}
```

So as string literals are can point to any String `&String` can be written as `&str` and this is better because, `&str` can hold both String and string literal i.e. string slices

# Structs :
A _struct_, or _structure_, is a custom data type that lets you package together and name multiple related values that make up a meaningful group.
```rust
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn main() {
    let mut user1 = User {
        active: true,
        username: String::from("someusername123"),
        email: String::from("someone@example.com"),
        sign_in_count: 1,
    };
    user1.email = String::from("anotheremail@example.com");
}

fn build_user(email: String, username: String) -> User {
    User {
        active: true,
        username,
        email,
        sign_in_count: 1,
    }
}
```

```rust
fn main() {
    // --snip--
    let user2 = User {
        active: user1.active,
        username: user1.username,
        email: String::from("another@example.com"),
        sign_in_count: user1.sign_in_count,
    };
}

// struct update syntax:
fn main() {
    // --snip--
    let user2 = User {
        email: String::from("another@example.com"),
        ..user1
    };
}
```

>Note that the entire instance must be mutable; **Rust doesn’t allow us to mark only certain fields as mutable**. As with any expression, we can construct a new instance of the struct as the last expression in the function body to implicitly return that new instance.

In this example, we can no longer use `user1` as a whole after creating `user2` as `active` and `sign_in_count` have `Copy` trait they won't be dropped, but the `String` in the `username` field of `user1` was moved into `user2`.

### Tuple Struct :
Tuple structs have the added meaning the struct name provides but don’t have names associated with their fields; rather, they just have the types of the fields.
```rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

fn main() {
    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);
}
```
Note that the `black` and `origin` values are different types because they’re instances of different tuple structs. Each struct you define is its own type, even though the fields within the struct might have the same types. For example, a function that takes a parameter of type `Color` cannot take a `Point` as an argument, even though both types are made up of three `i32` values.

### Unit-like Structs :
structs that don’t have any fields, they behave similarly to `()`. Unit-like structs can be useful when you need to implement a trait on some type but don’t have any data that you want to store in the type itself.
```rust
struct AlwaysEqual;

fn main() {
    let subject = AlwaysEqual;
}
```


# Crates :

## rand:
```rust
use rand::Rng;

fn main() {
	let mut rng = rand::rng();
	// generates a random integer number from [1, 2, 3, 4, 5, 6]
	// =6 means 6 is inclusive
	println!("Dice roll: {}", rng.random_range(1..=6));
	
	// generates a random integer number from [1, 2, 3, 4, .. 9] 
	// i.e. 10 is exclusive
	println!("Number from 0 to 9: {}", rng.random_range(0..10));
	
	// generates a random double number from 0 to 10, 10 is exclusive
	println!("Number from 0 to 9: {}", rng.random_range(0.0..10.0));
}
```


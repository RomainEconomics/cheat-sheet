

# Types

## Links

- [Rust Types](https://www.youtube.com/watch?v=MJrBLTHJPCo)

## Examples

### Unit

```rust
fn main() {
    let x: () = ();      // x is of type `()`, which is the unit type.
    println!("{:?}", x); // ()
}
```

### Integer

- Signed: `i8`, `i16`, `i32`, `i64`, `i128`, `isize`
- Unsigned: `u8`, `u16`, `u32`, `u64`, `u128`, `usize`

Unsigned integers are always positive or zero, while signed integers can be positive, negative, or zero.

Each signed variant can store numbers from `-(2^{n - 1})` to `2^{n - 1} - 1` inclusive, where `n` is the number of bits that variant uses.

So an `i8` can store numbers from `-(2^7)` to `2^{7 - 1}`, which equals `-128` to `127`. Unsigned variants can store numbers from `0` to `2^{n - 1}`, so a `u8` can store numbers from `0` to `2^8 - 1`, which equals 0 to 255.


### Floating Point

- `f32`: Single precision
- `f64`: Double precision

```rust

fn main() {
    let x = 2.0; // f64
    let y: f32 = 3.0; // f32
}
```

### Type Coercion

```rust
fn main() {
    let x = 42;
    let y = x as f64;
}
```


### Boolean

```rust
fn main() {
    let t = true;
    let f: bool = false; // with explicit type annotation
}
```

### Character

We specify `char literals` with `single quotes`, as opposed to `string literals`, which use `double quotes`.

Rust’s char type is four bytes in size and represents a Unicode Scalar Value, which means it can represent a lot more than just ASCII.

```rust
fn main() {
    let c = 'z';
    let z = 'ℤ';
    let heart_eyed_cat = '😻';
}
```

### String

Rust has only one string type in the core language, which is the string slice `str` that is usually seen in its borrowed form `&str`.

The `String` type, which is provided by Rust’s standard library rather than coded into the core language, is a growable, mutable, owned, UTF-8 encoded string type.

```rust
fn main() {
    let s = "hello"; // string slice
    let mut s = String::from("hello"); // String type
}
```


### Tuple

A tuple is a general way of grouping together a number of values with a variety of types into one compound type.

```rust

fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);

    let (x, y, z) = tup; // Destructuring
    println!("The value of y is: {}", y); // 6.4

    let five_hundred = tup.0; // Accessing elements
    let six_point_four = tup.1;
    let one = tup.2;
}
```

### Array

An array is a collection of elements of the same type, stored in contiguous memory.

Arrays in Rust have a fixed length, like tuples.

```rust
fn main() {
    let a = [1, 2, 3, 4, 5];

    let first = a[0];
    let second = a[1];
}
```

### Mutable Array

We can make an array mutable by using the `mut` keyword.
We reassigned the value of the first element of the array to 6.

```rust
fn main() {
    let mut a = [1, 2, 3, 4, 5];
    a[0] = 6;
}
```


### Slices

A slice is a reference to a contiguous sequence of elements in a collection.

It doesn't have ownership, but instead borrows from the original collection.

```rust
fn main() {
    let a = [1, 2, 3, 4, 5];

    let slice = &a[1..3]; // [2, 3]
}
```
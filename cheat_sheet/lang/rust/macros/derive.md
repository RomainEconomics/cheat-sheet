

# Derive

Derive is a feature in Rust that allows you to automatically implement traits for custom types.


## Examples


- `Debug`: Implements the `fmt::Debug` trait, enabling the struct or enum to be formatted using the `{:?}` formatter. This is particularly useful for debugging purposes.


- `PartialEq`: Implements the PartialEq trait to allow partial equality comparison (==, !=) between instances of the struct or enum.


- `Eq`: When derived alongside PartialEq, it implements the Eq trait, indicating that every comparison value is either equal or not equal (no partial comparisons). Eq requires PartialEq to be derived as well.


- `PartialOrd`: Implements the PartialOrd trait, allowing for partial ordering of instances. This enables comparison operators such as <, >, <=, and >=. It requires PartialEq to be derived too.


- `Ord`: Implements the Ord trait for total ordering of instances. This is useful for sorting operations. Ord requires both PartialOrd and Eq (and thus PartialEq) to be derived.


- `Clone`: Implements the Clone trait, enabling the struct or enum to be explicitly duplicated.


- `Copy`: Implements the Copy trait, indicating that instances of the type can be duplicated by bitwise copying. For a type to be Copy, it must also be Clone, and all of its components must be Copy as well.


- `Hash`: Implements the Hash trait, allowing instances to be hashed. This is necessary for types that will be used as keys in a HashMap or stored in a HashSet.


- `Default`: Implements the Default trait, providing a way to create an instance of the type with default values.


### Derive Debug

```rust
 #[derive(Debug, Clone, PartialEq)]
 struct Person {
     name: String,
     age: u32,
 }

 fn main() {
     let person1 = Person {
         name: String::from("Alice"),
         age: 30,
     };

     let person2 = person1.clone(); // Clone trait allows us to easily duplicate `person1`.

     // Debug trait allows us to print our struct, which is very handy for debugging.
     println!("{:?}", person1);

     // PartialEq trait allows for comparison.
     if person1 == person2 {
        println!("person1 and person2 are the same!");
    }
 }
```
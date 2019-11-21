# rustling_notes
Keeper for my notes

##  Arrays:

###  Declaring
use `let var : [` type `;` number declared (eg. 100) `]`

###  Slicing
```
fn main() {
    let a = [1, 2, 3, 4, 5];

    let nice_slice = &a[1 .. 4];

    assert_eq!([2, 3, 4], nice_slice)
}
[1]+  Done                    clear
```
### tuple destruct (aka py tuple unpacking)
```
fn main() {
    let cat = ("Furry McFurson", 3.5);
    let (name, age) = cat;

    println!("{} is {} years old.", name, age);
}
[1]+  Done                    clear
```
or you can grab them by var name & index ``` cat.1 ```

##  Functions

index a range through a function call :  needs the type for the range
```
fn main() {
    call_me(3);
}

fn call_me(num:u8) {
    for i in 0..num {
        println!("Ring! Call number {}", i + 1);
    }
}
[1]+  Done                    clear
```
### Function call and return type

#### Functions return only when the ```->``` is used

Return is either explicit or implicit.  Implicit return is:
 - returns last line
 - no semicolon at the end of line

 ```
 fn main() {
    let original_price = 51;
    println!("Your sale price is {}", sale_price(original_price));
}
```
for this function, we note the return type as i32
```
fn sale_price(price: i32) -> i32 {
    if is_even(price) {
        price - 10
    } else {
        price - 3
    }
}

fn is_even(num: i32) -> bool {
    num % 2 == 0
}
 ```
For an explicit return, using the ```return``` keyword, the line is semicoloned and any code below is ignored.



##  Strings:

### remember &str vs Strings 

I have a C++ background and I found it very useful to think about String and &str in C++ terms:
https://stackoverflow.com/questions/24158114/what-are-the-differences-between-rusts-string-and-str

A Rust String is like a std::string; it owns the memory and does the dirty job of managing memory.
A Rust &str is like a char* (but a little more sophisticated); it points us to the beginning of a chunk in the same way you can get a pointer to the contents of std::string.
Are either of them going to disappear? I do not think so. They serve two purposes:

String keeps the buffer and is very practical to use. &str is lightweight and should be used to "look" into strings. You can search, split, parse, and even replace chunks without needing to allocate new memory.

&str can look inside of a String as it can point to some string literal. The following code needs to copy the literal string into the String managed memory:

```let a: String = "hello rust".into();```
The following code lets you use the literal itself without copy (read only though)

```
let a: &str = "hello rust";
```

### Strings vs Chars

``` " ``` vs ``` ' ```

### ```to_string``` vs ```into_string```


Read this:

https://stackoverflow.com/questions/25316115/difference-between-tostring-and-intostring#comment71524171_25317888


to_string:
 - takes reference ```&str```
 - returns a new String  
 - allocates memory for that new String
 
into_string:
  - takes String
  - moves it to new location in stack

#### test2.rs
this all basically boils down to using teh ```string``` function if inside the paranthesis is a ```String```, versus using ```string_slice``` if the value is a reference.  Tricky.  Lots to memorize. 


```
fn string_slice(arg: &str) {
    println!("{}", arg);
}
fn string(arg: String) {
    println!("{}", arg);
}

fn main() {
    string_slice("blue");
    string("red".to_string());
    string(String::from("hi"));
    string("rust is fun!".to_owned());
    string("nice weather".into());
    string(format!("Interpolation {}", "Station"));
    string_slice(&String::from("abc")[0..1]);
    string_slice("  hello there ".trim());
    string("Happy Monday!".to_string().replace("Mon", "Tues"));
    string("mY sHiFt KeY iS sTiCkY".to_lowercase());
}
```



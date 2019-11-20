# rustling_notes
Keeper for my notes

##  Strings:
remember &str vs Strings 

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

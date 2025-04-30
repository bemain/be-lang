# be-lang
 > **Disclaimer:** The Be programming language is adapted to my own mind and developed according to my own preferences. If it ever happens to be useful to anyone else that is purely coincidental, and I do not take responsibility.

This repository contains the specification for the Be language, a coding language focused on prototyping and problem-solving. The core principles of the Be language are simplicity, compactness and elegance. 

```
isPrime := (Int p) => Bool {
  # Checks whether [p] is a prime number.
  => [2, 3...p~//2:2].map(p%).all(?=0);
}

expSum := (List<Float> vals, [Int exp = 2], {Int skip = 0, Float? max}) => (Float sum, {Float? overflow}) {
  # Raises the values in [vals] to an [exp]onent and sums them. 
  # Optionally skips the first [skip] values.
  # If [max] is non-null, the returned sum will not exceed that value. If the sum is clamped in this way, [overflow] will be the difference between the actual sum and the returned value.
  # Returns the [sum].
  s = vals[skip:].map(^exp).reduce(0, +);
  => ??max ? (s) : (max, overflow: s-max);
}

(sum, overflow: o) = expSum([3.2, 1.0, 17.8], 3, skip: 1);
```

This example showcases a number of the Be language's fundamental principles.
- **Common types**, such as `Int`, `Float` and `Bool`. The language is statically typed, but features type inference using `:=`. 
- A few **naming conventions**. Types should be named using UpperCamelCase and variables using lowerCamelCase.
- Creating a **range** of values using the `a...b:step` syntax.
- **Rounding arithmetic operators** (`~*`, `~^,` `~/`, `~//`) that round the returned value to an `Int` after performing their usual operation.
- A few common **list manipulation methods** such as `map`, `all` and `reduce`. Many more are available, like `any`, `where`, `sorted` and `reversed`. There are also methods that operate in-place, such as `sort`, `shuffle`, `remove` and `add`.
- **Semiloaded operators**, one of the core features that are (as far as I know) unique to the Be language. This is described in detail in another section of the specification, but in short it allows you to pass the parameters to an operator one at a time.
```
addThree = +3;
addThree(5); # 8
```
I'm trying to figure out if I can make this work for any function, but am struggling with what the syntax should be.
- **Object destructuring** for parameters. A few other objects such as lists and maps also support destructuring:
```
[a, b, ...m, l] = [1...6];
# a = 1, b = 2, m = [3, 4, 5], l = 6
```
- **Null-safety** using the `?` to indicate that a type is nullable (such as `Float?`) and the `??` operator to check whether a variable is `null`.

# Chapter 02. Predeclared Types and Declarations
* **Focus on Clarity:** Write Go code that expresses your intentions clearly.
* **Up Next:** 
    * Go's built-in types 
    * How to declare variables in Go 
    * How Go's approach may differ from what you're used to 

## Table of Contents
* [The Predeclared Types](#the-predeclared-types)
* [var Versus :=](#var-versus)
* [Using const](#using-const)
* [Typed and Untyped Constants](#typed-and-untyped-constants)
* [Unused Variables](#unused-variables)
* [Naming Variables and Constants](#naming-variables-and-constants)
* [Exercises](#exercises)
* [Wrapping Up](#wrapping-up)


### The Predeclared Types
**Go's Built-in Types**

* **Zero Values:** All types have a default zero value (e.g., 0 for numbers, false for booleans).
* **Literals:**  Represent values directly in code. Types include:
    * **Integer literals:** Base 10 by default, use prefixes for other bases (0b, 0o, 0x)
    * **Floating-point literals:** Include decimal point (can use scientific notation with 'e')
    * **Rune literals:**  Single Unicode characters in single quotes ('a')
    * **String literals:** Use double quotes for interpreted strings (most common), backticks for raw strings.

**Types in Detail**

* **Booleans (bool):**  true or false.
* **Integers:**
    * Signed and unsigned varieties (int8, int16, ..., uint8, uint16, ...)
    * Specials: `byte` (alias for `uint8`), `int` (size varies by system), `uint`
    * Choose `int` for most cases unless working with a specific format.
* **Floating-Point:** 
    * `float32`, `float64`
    * Default to `float64`  for accuracy. 
* **Complex (complex64, complex128):** Used for complex numbers if absolutely needed.

**Important Considerations**

* **Comparisons:** Use standard operators (==, !=, >, etc.). Be careful with floating-point equality.
* **No Automatic Conversions:** Explicitly convert between types (e.g., `float64(x)`). This enhances clarity.
* **Strings are Immutable:**   You can't modify a string's content in place.
* **Runes (rune):** Represent a single Unicode code point.
* **No "Truthy" Values:**  Unlike some languages, you can't use non-booleans as booleans. 

> **Key Takeaway:** Go prioritizes code clarity over implicit behaviors.  

### var Versus :=
**Variable Declarations in Go**

Go offers flexibility in how you declare variables. The style you choose communicates intent.

**Methods**

* **`var x type = value`:** Explicit type declaration and assignment.
* **`var x = value`:** Type inferred from the value.
* **`var x type`:** Declares variable with zero value of specified type.
* **`x := value`:**  Short declaration with type inference. Can be used for new or existing variables (within a function only).

**Best Practices**

* **Inside Functions:**  Generally, prefer the short declaration `:=` for its simplicity.
* **Package-Level Declarations:** You *must* use `var` for variables outside functions.  
* **Zero Value Importance:** If the zero value is meaningful, use `var x int`.
* **Explicit Types:** Use `var x type = value` to clarify intent when the type isn't the default for the value.
* **Shadowing Pitfalls:**  Be cautious with `:=`, as it can accidentally create new variables with the same name. Use `var` and explicit assignment to avoid this.

> **Key Point:** Limit package-level variable declarations. These can make understanding your program's data flow harder.

> **Immutability Note:**  Use `const` for values that should never change. 

### Using const
**Using `const` in Go**

* **Purpose:** `const` gives names to literal values known at compile time.
* **Key Points:**
    * **Limited Scope:**  `const` works only with literals or expressions comprised entirely of literals and operators.
    * **Immutability:** Values declared with `const` cannot be changed.
    * **Types:** Allowed types include numbers, booleans, strings, and runes.
    * **Runtime Immutability Missing:** Go doesn't support declaring variables as immutable once their value is set at runtime. 

**Types Supported by `const`**

* Numeric literals (e.g., 20, 3.14)
* `true` and `false`
* Strings (e.g., "hello")
* Runes (e.g., 'a')
* Values from built-in functions `complex`, `real`, `imag`, `len`, `cap`
* Expressions using the above with operators 

**Example:**

```go
const Pi = 3.14159 
const greeting = "Hello"
```

### Typed and Untyped Constants
**Typed vs. Untyped Constants in Go**

* **Untyped Constants:**
    * No explicit type.
    * Default type inferred from context.
    * Flexible - can be assigned to variables of compatible types.
    * Example: `const PI = 3.14159`

* **Typed Constants:**
    * Have an explicit type.
    * Enforcement - assignable only to variables of the same type.
    * Example: `const max int = 100`

**When to Choose** 

* **Untyped:**  Most cases, especially for constants usable with various numeric types.
* **Typed:**  When you need strict type enforcement. 

### Unused Variables
**Unused Variables in Go**

* **Key Rule:** Every *locally declared* variable **must be used** (read at least once). This is a compile-time error.
* **Purpose:** 
    * Ensures code clarity by preventing accidental unused variables.
    * Aids code maintainability for larger projects.
* **Compiler Behavior:**
    * Catches unused variables but might not detect unused assignments within the same variable.
    * Does not enforce this rule for package-level variables (another reason to minimize them!). 
* **Unused Constants:** Technically allowed, as they're removed during compilation if not used. 
* **Tools:** Third-party code quality tools can help catch more subtle cases of unused assignments. 

### Naming Variables and Constants
**Naming Variables and Constants in Go**

* **Technical Rules:**
    * Start with a letter or underscore.
    * Can contain letters, numbers, and underscores.
    * Unicode characters are broadly allowed.

* **Don't:** Use confusing names or Unicode look-alikes that hinder readability.

* **Idiomatic Go:**
    * **Camel Case:** For multi-word names (e.g., `indexCounter`)
    * **Short Names (within functions):**  Favored for small scopes (e.g., `i`, `j` for loop indices)
    * **Descriptive Names (package-level):** Clarify purpose within a wider context.

* **Avoid:**
    * **Snake Case:** (e.g., `index_counter`)
    * **Type Prefixes:** Go's strong typing makes this unnecessary.
    * **ALL CAPS:**  Reserved for exported package-level items. 

> **Key Takeaway:** Prioritize clear, readable names that communicate intent. 

### Exercises
> 1- Write a program that declares an integer variable called i with the value 20. Assign i to a floating-point variable named f. Print out i and f.

**Answer**:

```go
package main

import "fmt"

func main() {
	var i int = 20
	var f float64 = float64(i)

	fmt.Println(i)
	fmt.Println(f)
}
```

> 2- Write a program that declares a constant called value that can be assigned to both an integer and a floating-point variable. Assign it to an integer called i and a floating-point variable called f. Print out i and f.

**Answer**:

```go
package main

import "fmt"

func main() {
	const value = 52
	var i int = value
	var f float64 = value
	fmt.Println(i)
	fmt.Println(f)

}
```

> 3- Write a program with three variables, one named b of type byte, one named smallI of type int32, and one named bigI of type uint64. Assign each variable the maximum legal value for its type; then add 1 to each variable. Print out their values.

**Answer**:

```go
package main

import "fmt"

func main() {
	var b byte = 255
	var smallI int32 = 2147483647
	var bigI uint64 = 18446744073709551615

	b = b + 1
	smallI = smallI + 1
	bigI = bigI + 1

	fmt.Println(b)
	fmt.Println(smallI)
	fmt.Println(bigI)
}
```
### Wrapping Up
**Chapter 2 Recap**

* **Predeclared Types:** Go offers built-in types for numbers (integers, floats), booleans, strings, and runes.
* **Variables:**
    * `var` for explicit declaration.
    * `:=` for short declaration with type inference.
    * Use `const` for compile-time constants.
* **Clarity Matters:** Type conversions must be explicit. No "truthiness".
* **Unused Variables:**  Caught by the compiler -  keeps your code clean.
* **Naming:** Choose names that communicate intent.

**Up Next: Chapter 3**

* **Composite Types:**  Delve into arrays, slices, maps, and structs  – the building blocks of complex data structures.
* **Strings in Depth:**  Explore how strings and runes work with character encodings. 


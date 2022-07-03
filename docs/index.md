# Gopher Guide

This is meant to be a simple Go onramp and cheatsheet.

## Development Environment

### Installation

Approach #1: Install using homebrew (if on macOS or Linux) using the `brew install go` command.

Approach #2: Install directly from [go.dev/dl](https://go.dev/dl)

### Preferred Editors
- [Goland](https://www.jetbrains.com/go/) (free license available to students and faculty by using academic email)
- [VSCode](https://code.visualstudio.com/)

## Standard Setup

```go
package main

import "fmt"

func main() {
	fmt.Println("gophers are cool")
}
```

Everything in Go is a package. Programs start running in the `main` package. A standard setup starts with `package main` at the top of the file.

## Imports

We can group imports with parenthesis if more than one package is needed. Go has an extensive [standard library](https://pkg.go.dev/std) that you can use and import packages from without additional installation.

```go
package main

// we can group imports with parenthesis if more than one package is needed (factored imports)
import (
	"fmt"
	"math/rand"
) 

func main() {
	fmt.Println(rand.Intn(10)) // print a random number between 0-9
}
```

## Functions

```go
package main

import (
	"fmt"
	"strings"
)

// no parameters or return values
func sayHello() {
	fmt.Println("Howdy")
}

// one parameter and return value
func greeting(name string) string {
	return fmt.Sprintf("Howdy %v!\n", name)
}

// multiple input parameters and returns
func sum(x, y, z int) (int, int) {
	return x + y, y + z
}

// named return
func formatName(name string) (formattedName string) {
	formattedName := strings.ToUpper(name)
	return
}

func main() {
	sayHello()
	howdyGophers := greeting("gophers")
	a, b := sum(22, 33, 44)
	bigGopher := formatName("gopher")
	
}

```

!!! note
	In the last example we only included the `int` type after the last param. You can use this syntax when params are of the same type. For different types it would look something like `func hello(name string, age int)...`

## Variables

```go
package main

var isValid bool // package level variable

func main() {
	var i int // function level variable
	fmt.Println(i, isValid)
}
```

### Initializers

```go
pacakge main

import "fmt"

func main() {
	var i, j, k int = 101, 102, 103
	fmt.Println(i, j, k)
}
```

!!! tip
	If an initializer is present, we can omit the type (i.e. `var i = 101`)

### Shorthand Declaration

```go
package main

import "fmt"

func main() {
	name := "Kevin the Gopher"
	fmt.Println(name)
}
```

!!! note
	This shorthand syntax can be used at the function level. At the package level the `var` keyword is needed for variables (the `:=` is not available)

## Data types

Go has standard types like:
- bool
- string
- int, int8, int16, int32, int64
- uint, uint8, uint16, uint32, uint64, uintpr
- byte (int8)
- rune (int32, unicode code point)
- float32, float64
- coomplex64, complex128

!!! note
	`int`, `unit`, and `uintpr` are typically 32 bits wide on. 32-bit systems and 64 bits wide on 64-bit systems. You should use `int` when you need an integer value unless their is a specific reason to use a sized on unsigned integer

```go
package main

import "fmt"

func main() {
	var isMac bool
	fmt.Printf("value: %v, type %T\n", isMac, isMac)
}
```

### Type conversions

Type conversions are done similarly to other languages

```go
package main

import "fmt"

func main() {
	i := 77
	j := float64(77)
	fmt.Printf("value: %v, type: %T", i, i)
	fmt.Printf("value: %v, type: %T", j, j)
}
```

### Constants

Constants can be defined the same as variables, but with the `const` keyword

```go
package main

import "fmt"

func main() {
	const pi float64 = 3.14
	fmt.Println(pi)
}
```

!!! note
	You can't use the `:=` operator syntax for constants

## Looping

In Go, we only have a `for` loop.

```go
package main

import "fmt"

func main() {
	for i := 0; i < 10; i++ {
		fmt.Println(i)
	}
}
```

For loops are broken down into 3 parts:
1. The init statement which is executed before the first iteration (i.e. `i := 0`)
2. The condition statement which is evaluated before each iteration (i.e. `i < 10`)
3. The post statement which is executed at the end of each iteration (i.e. `i++`)

Init and post statements are optional in Go

```go
package main

import "fmt"

func main() {
	i := 0
	for i < 10; {
		fmt.Println(i)
		i++
	}
}
```

This is like a while loop in other languages. What happens if you don't write a condition? You write an infinite loop...

```go
package main

import "fmt"

func main() {
	i := 0
	for {
		i++
		fmt.Println(i)
	} // run until the end of time (or sooner perhaps)
}
```


## If

```go
package main

import "fmt"

func main() {
	x := 13
	if x > 11 {
		fmt.Println("x is greater than 11")
	} else {
		fmt.Println("x is not greater than 11")
	}
}
```

The short If

```go
package main

import (
	"fmt"
	"strings"
)

func main() {
	greeting := "Howdy gophers!"
	if greeting := "Howdy"; strings.Contains(greeting, "ow") {
		fmt.Println(greeting)
	}
}
```

## Switch

```go
package main

import (
	"fmt"
	"runtime"
)

func main() {
	switch os := runtime.GOOS; os {
	case "darwin":
		fmt.Println("Gophers running a reasonable OS")
	case "linux":
		fmt.Println("Gophers running the superior OS")
	default:
		fmt.Println("Gophers running the wrong OS")
	}
}
```


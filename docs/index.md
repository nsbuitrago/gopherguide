# Gopher Guide

This is meant to be a quick onramp / cheatsheet for busy people getting into Go.

## 1. Setup

**Installation (if necessary):**

Approach 1: Install directly from [go.dev/dl](https://go.dev/dl)

Approach 2 (Preferred, although only for macOS and Linux): Install using [Homebrew](https://brew.sh) using `brew install go` command.

- Install homebrew if necessary (copy and paste the following in your terminal to install or go to [brew.sh](https://brew.sh)for additional instruction)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

- Install Go with `brew install go` command.

**Preferred Editors:**

Now that you have Go, the next step is to setup your editor. I personally like to use [NeoVim](https://neovim.io), but it has a somewhat steep learning curve and can take considerable effort to setup if you are new to it.

[Goland](https://jetbrains.com/go) is a great IDE for Go that I have also used and enjoyed. Unfortunately, this one costs some money, but you can get a free license if you are a university student or faculty.

[VS Code](https://code.visualstudio.com) is another good alternative and is free. I would recommend installing the [official Go extension](https://marketplace.visualstudio.com/items?itemName=golang.go) for VS Code as well.

## 2. The standard main.go

Everything in Go is a package. Programs start running in the `main` package. The first line of any Go file should declare a package name.

```go
package main

import "fmt"

func main() {
	fmt.Println("Gophers are cool")
}
```

## 3. Imports

```go
package main

import (
	"fmt"
	"math/rand"
) // import multiple packages by enclosing with ()

func main() {
	fmt.Println(math.randIntn(10)) //print a random int betwee 0-9
}
```

## 4. Data types and variables

Go has standard types like:

* bool
* string
* int, int8, int16, int32, int64
* uint, uint8, uint16, uint32, uint64, uintpr
* byte (int8)
* rune (int32, unicode code point)
* float32, float64
* complex64, complex128

```go
package main

import "fmt"

var numGophers int = 0

func main() {
	// declare and init var with type bool
	var isGopher bool = false
	// we can also use a shorthand notation using :=
	isHuman := true // this will infer a type from the initializer

	fmt.Printf("Value: %v, Type: %T", numGophers, numGophers)
	fmt.Printf("Value: %v, Type: %T", isGopher, isGopher)
	fmt.Printf("Value: %v, Type: %T", isHuman, isHuman)
}
```

!!! note
	We cannot use the shorthand notation with `:=` when declaring variables at the package level. At the package level, everything needs to start with a keyword like `var`, `func`, etc.

### Constants and more

```go
package main

import (
	"fmt"
	"runtime"
)

func main() {
	// declare and init a constant variable
	const pi float64 = 3.14
	// declare a var without an initializer
	var operatingSystem string // we can now use this later

	fmt.Println(pi)
	// set operatingSystem variable
	operatingSystem = runtime.GOOS
	fmt.Println(operatingSystem)
}
```

### Type conversions

```go
package main

import "fmt"

func main() {
	i := 77
	j := float64(i) // convert i of type int to float64 
	
	fmt.Printf("value: %d, type: %T", i, i) // will be an int
	fmt.Printf("value: %d, type: %T", j, j) // will be float64
}
```

## 5. Functions

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
	In `sum(x, y, z int)` we only included the `int` type after the last param. You can use this syntax when params are of the same type. For different types it would look something like `func hello(name string, age int)...`

## 6. Looping and Conditional Logic

### For

```go
package main

import "fmt"

func main() {
	var z float64
	for i := 0; i < 10; i++ {
		z = i*i
		fmt.Println(z)
	}
}
```

In Go, we only have a `for` loop. For loops are broken down into 3 parts:

1. The init statement which is executed before the first iteration (i.e. `i := 0`)

2. The condition statement which is evaluated before each iteration (i.e. `i < 10`)

3. The post statement which is executed at the end of each iteration (i.e. `i++`)

Init and post statements on a loop are optional, i.e.

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

**The infinite loop**

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

### If

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

**The short if**

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

### Switch

```go
package main

import (
	"fmt"
	"runtime"
)

func main() {
	switch os := runtime.GOOS; os {
	case "darwin":
		fmt.Println("Reasonable")
	case "linux":
		fmt.Println("The superior OS")
	default:
		fmt.Println("I want better for you")
	}
}

```
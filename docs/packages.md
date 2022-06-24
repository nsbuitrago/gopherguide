# Packages

If you come from other programming languages, you are probably familiar with the idea of packages. In Go, everything is made up of packages and programs start running in the `main` package

Let's make a file called `main.go` and at the top we will specifiy it belongs to the `main` package by writing `package main`

We can also import existing packages to use in our programs. Go has a standard library of packages that are included (i.e. don't require an additional install and are ready to use)

To import packages, we use the `import` keyword. For importing a single package, you can write the name of the package in double quotes. For example

```go
package main

import "fmt"
```

Above, we are importint the `fmt` or format package from the standard library. In many cases, you will find yourself needing to import more than one package. In those cases,  you can simply list all the packages you need and enclose them with parenthesis like so:

```go
package main

import (
	"fmt"
	"math/rand"
	"net/http"
)
```

!!! note
	In the second and third packages imported above, the package name is `rand` and `http` respectively. The name always goes to the last element of the import path.


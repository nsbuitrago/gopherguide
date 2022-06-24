---
title: Datatypes and Variables
---

# Datatypes & Variables

Go gives you standard datatypes like:
- integers: int8, int16, int32, int64
- floats: float32, float64
- byte
- rune
- strings
- booleans

Let's say we want to decalre a variable called `myInt` and assign it an integer value of `8675309`

We can do that a couple of different ways.

Once approach is to use the `var` keyword for variable like this

```go
var myInt int = 8675309
```

Since we include the integer we want to assign, we can omit the type

```go
var myInt = 8675309
```

We also have a shor declaration syntax which uses `:=`

```go
myInt := 8675309
```

In the above two examples, the type is inferred from the value that is assigned. In cases where more fine control over the type is needed (i.e. specifically need an int8 over an int16), the first approach can be used.

You can also initialize variables using similar syntax as the first example (leaving off the value and assignment operator)

```go
var myInt int
```

`myInt` can then be used at a later time.


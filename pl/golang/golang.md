# Golang

## Table of Contents

## Naming Conventions

- if the object is accessible outside the package: `PascalCase`
- if the object is accessible only inside the package: `camelCase`

## Types

### Maximal and Minimal values for integers

It is possible to get them through the `math` package
```go
package main

import (
    "fmt"
    "math"
)

func main() {
    // integer max
    fmt.Printf("max int64   = %+v\n", math.MaxInt64)
    fmt.Printf("max int32   = %+v\n", math.MaxInt32)
    fmt.Printf("max int16   = %+v\n", math.MaxInt16)

    // integer min
    fmt.Printf("min int64   = %+v\n", math.MinInt64)
    fmt.Printf("min int32   = %+v\n", math.MinInt32)

    fmt.Printf("max float64 = %+v\n", math.MaxFloat64)
    fmt.Printf("max float32 = %+v\n", math.MaxFloat32)

    // etc you can see more int the `math`package
}
```

## Flow of control

### For in range

The following loop iterates the `entry` array:
```go
entry := []string{"Jack","John","Jones"}

for i, val := range entry {
  fmt.Printf("At position %d, the character %s is present\n", i, val)
}
```
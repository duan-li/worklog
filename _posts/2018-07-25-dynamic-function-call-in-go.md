---
layout: post
title: Dynamic function call in Go
date: 2018-07-25 06:35 +0000
---


Two ways to do it
* interface[^1]
* map[^2]

[^1]: https://mikespook.com/2012/07/function-call-by-name-in-golang/
[^2]: https://mikespook.com/2012/07/function-call-by-name-in-golang/

```golang
package main

import (
	"encoding/json"
	"io"
	"os"
	"reflect"
	"fmt"
)

type A struct {
	Name  string
	Value int
}

type B struct {
	Name1 string
	Name2 string
	Value float64
}

func doA() *A {
	return &A{"Cats", 10}
}

func doB() *B {
	return &B{"Cats", "Dogs", 10.0}
}

func doC() {
	fmt.Printf("c")
}

func Generic(w io.Writer, fn interface{}) {

	result := reflect.ValueOf(fn).Call([]reflect.Value{})[0].Interface()
	json.NewEncoder(w).Encode(result)
}

func main() {
	funcA := doA
	Generic(os.Stdout, funcA)
	Generic(os.Stdout, doB)
	fmt.Printf("other way")
	funcs := map[string]func() {"doC": doC}
	funcs["doC1"]()


}
```



---



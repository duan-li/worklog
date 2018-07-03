---
layout: post
title: go test case
date: 2018-06-16 12:29 +0000
---

# Command
* `go test ./...`: run all test cases in correct directory
* `go test -cover`: display test case coverage
* `go test -run Name`: run specific golang test case

## test all package
```
# https://github.com/opencontainers/runc/blob/master/Makefile
_allpackages = $(shell $(GO) list ./... | grep -v vendor)
allpackages = $(if $(__allpackages),,$(eval __allpackages := $$(_allpackages)))$(__allpackages)
go test -timeout 3m -v $(allpackages)
```

```
# https://github.com/dockercraft/libcontainer/blob/master/Makefile
GO_PACKAGES = $(shell find . -not \( -wholename ./vendor -prune -o -wholename ./.git -prune \) -name '*.go' -print0 | xargs -0n1 dirname | sort -u)

go test -cover -test.short -v $(GO_PACKAGES)
```


# Test Types
* `*testing.T`: Type T - Testing
* `*testing.B`: Type B - Benchmarks
* `*testing.M`: Type M - Main





## Example
**main.go**

```go
package main

func Sum(x int, y int) int {
	return x + y
}

func main() {
	Sum(5, 5)
}

```


**main_test.go**

```go
package main

import "testing"

func TestSum(t *testing.T) {
	total := Sum(5, 5)
	if total != 10 {
		t.Errorf("Sum was incorrect, got: %d, want: %d.", total, 10)
	}
}

```

```go
package main

import (
	"flag"
	"fmt"
	"os"
	"testing"
)

func setup() {
	println("setup")
}

func teardown() {
	println("teardown")
}

func TestMain(m *testing.M) {
	// call flag.Parse() here if TestMain uses flags
	switch os.Getenv("GO_TEST_MODE") {
	case "":
		setup()
		flag.Parse()
		exitCode := m.Run()
		fmt.Printf("exitCode is %d\n", exitCode)
		if exitCode == 0 {
			teardown()
		}

		// Exit
		os.Exit(exitCode)
	}

}

```

# Tools

## gotests
> Generate Go tests from your source code.

`go get github.com/cweill/gotests/...`

run 
`../../bin/gotests -exported ./`


## gover
> Gather all your *.coverprofile files to send to coveralls.io!

`go get github.com/modocache/gover`


- Ref
 - https://splice.com/blog/lesser-known-features-go-test/
 - https://golang.org/pkg/testing/
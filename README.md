# regexrand
[![GoDoc](https://godoc.org/github.com/multimikael/regexrand?status.png)](http://godoc.org/github.com/multimikael/regexrand)

regexrand is a library for generating matching string from a Go RE2 regular expression. 

## Installation
regexrand can be installed using `go get`:
```sh
go get github.com/multimikael/regexrand
```

## Usage
Generate a string by calling `GenerateMatch(&b, re, moreLimit)` 
* `b` is a `strings.Builder` where the result will be stored. The accumulated string of the builder can be returned by calling `b.String()`. 
* `re` is a given `syntax.Regexp` regular expression. This can be created using `syntax.Parse`.
* `moreLimit` is an `int` that determines the limit of "or more" operators. Using "or more" operator will generate a random integer between a minimum value and `moreLimit`.

### Example
Here is a simple example of regexrand. This will print a string with a lowercase character and 1 or more (up to 10) digits between 1 and 9.
```go
package main

import (
	"fmt"
	"regexp/syntax"
	"strings"

	"github.com/multimikael/regexrand"
)

func main() {
	re, err := syntax.Parse(`[a-z][1-9]+`, syntax.Perl)
	if err != nil {
		fmt.Println(err.Error())
	}
	var b strings.Builder
	regexrand.GenerateMatch(&b, re, 10)
	fmt.Println(b.String())
}
```
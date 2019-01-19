### Go CLI Commands

- ```go build``` - compiles a bunch of go source code
- ```go run``` - compiles and executes one or two files 
- ```go fmt``` - formats all the code in each file in the current directory
    - requires additional explanation
- ```go install``` - compiles and "installs" a package
    - requires additional explanation
- ```go get``` - downloads the raw source code of someone else's package
    - requires additional explanation
- ```go test``` - runs any tests associated with the current project 

### Go Syntax

Variable Declaration

```go 
var card string = "Ace of Spades"
// keyword :: variable name :: static typing :: value
card := "Ace of Spades"
// shorter version, but declaration depends on compiler 
```

Function Declaration
```go
func main() { // void/main function

}
func returnStuff() string { // return type function 
    return "stuff"
}
```

Variable Types

- Basic Data Types
    - bool, int, string, float64, byte
- Arrays
    - Two kinds of arrays
        - Array - fixed length list of things
        - Slice - an array that can grow or shrink
        ```go
        card := []string{"Ace of Diamonds", "etc"} // slice declaration
        cards = append(cards, "new element") // adding a new element 
        ```
    - every element in a slice/array must be of the same type 
- A byte slice is a string where a byte is an ASCII value that corresponds to a character

Type Casting

- much like many other languages
```go
[]byte("Hi There")
```

For Loops

```go
for i, card := range cards {
    fmt.Println(i, card)
}
```

While Loops

```go
for truthVariable {
    // do something
}
```

Type Declaration and Receiver Functions

```go
type deck []string // declaring a new custom type
func (d deck) print() { // a receiver, can be called through deck.print()
// instance goes first, then type 
// convention requires instance as one/two letter abbreviation of type
    fmt.Println(d)
}
``` 

Returning Multiple Values

- functions in go can return multiple values
- to capture these return values
```go
hand, remainingDeck := deal(cards,5) 
```
- to return these values by function
```go
func deal(d deck, handSize int) (deck, deck) {
    return d, d
}
```

### Basic Notes

- GoLang is not an object-oriented language

Packages

- package is a project or a workspace
- many files can be included in the same file, but the package they belong to must be declared at the top 
- two types of packages: executable, which produces an executable file, and helper, and reusable, code used as helpers and a good pace to put reusable logic, can be seen as code dependencies or libraries 
    - the name of package you use determines what type of package you make (**main** is the only name to make an executable file)
    - main package must have a "main" function 
- **files in the same package can freely call functions of each other** 

### Package Functions

bufio Package

```go
func NewReader(rd io.Reader) *Reader // makes a reader for in-line arguments, accepts 'os.Stdin' as io.Reader argument

func (b *Reader) ReadString(delim byte) (string, error) // reads up to the first occurrence of delim, returning the string up to and including delim

// If using ReadString up to next new line, must use strings.Replace function to remove new line character
```

ioutil Package

```go
func WriteFile(filename string, date []byte, perm os.FileMode) error // creates a file

func ReadFile(filename string) ([]byte, error ) // reads a file 
```

strings Package

```go
func  Join (a []string, sep string) string // reads a slice of strings into a single string 

func Replace(s, old, new string, n int) string // returns copy of s with the first n non-overlapping instances of old replaced by new, if n < 0, there is no limit on number of replacements 
```


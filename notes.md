## Go CLI Commands

- ```go build``` - compiles a bunch of go source code
- ```go run``` - compiles and executes one or two files 
- ```go fmt``` - formats all the code in each file in the current directory
    - requires additional explanation
- ```go install``` - compiles and "installs" a package
    - requires additional explanation
- ```go get``` - downloads the raw source code of someone else's package
    - requires additional explanation
- ```go test``` - runs any tests associated with the current project 

## Go Syntax

#### Variable Declaration

```go 
var card string = "Ace of Spades"
// keyword :: variable name :: static typing :: value
card := "Ace of Spades"
// shorter version, but declaration depends on compiler 
```

#### Function Declaration
```go
func main() { // void/main function

}
func returnStuff() string { // return type function 
    return "stuff"
}
```

#### Variable Types

- Basic Data Types
    - bool, int, string, float64, byte
- Arrays
    - Two kinds of arrays
        - Array - fixed length list of things
        - Slice - an array that can grow or shrink
        ```go
        card := []string{"Ace of Diamonds", "etc"} // slice declaration
        cards = append(cards, "new element") // adding a new element 
        len(cards) // length of slice
        ```
    - every element in a slice/array must be of the same type 
- A byte slice is a string where a byte is an ASCII value that corresponds to a character

#### Type Casting

- much like many other languages
```go
[]byte("Hi There")
```

#### For Loops

```go
for i, card := range cards {
    fmt.Println(i, card)
}
```

#### While Loops

```go
for truthVariable {
    // do something
}
```

#### Type Declaration and Receiver Functions

```go
type deck []string // declaring a new custom type
func (d deck) print() { // a receiver, can be called through deck.print()
// instance goes first, then type 
// convention requires instance as one/two letter abbreviation of type
    fmt.Println(d)
}
``` 

#### Returning Multiple Values

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

#### Structures 

```go
// Declaring a struct type
type person struct {
    firstName string
    lastName string
}

// structure initialization
alex := person{"Alex", "Anderson"}
// alternative
alex := person{firstName: "Alex", lastName: "Anderson"}
// alternative
var alex person // where fields are defaulted to empty strings

// assigning a field
alex.firstName = "Alex"
alex.lastName = "Anderson"
```

#### Maps

- keys and values must all be the same type
```go
colors := map[string]string {
    "red": "#ff0000",
    "green": "#feafda",
}
// alternative
colors := make(map[string]string)
// Map manipulation
colors[white] = "#fffff"
// Map deletion
delete(colours, "white")
// Map iteration
for color, hex := range mapName {
    fmt.Prinln(colour, hex)
}
```

#### Interfaces 

- used when different types of objects use similar functions (or functions that have the same name) 

```go
type bot interface {
    getGreeting() string
}
```

- interfaces are **not** generic types (go doesn't support generic types)
- interfaces are 'implicit'
- interfaces are a contract to help us manage types
- interfaces are tough, step #1 is understanding how to read them

#### Go Routines

- a single go routine is an engine that runs code 
- the benefit of go routine, we can run multiple go routines at the same time

```go
go functionName()
// the go keyword creates a new thread go routine, running the function 
```
- A Go Scheduler limits go routines to a particular core (by default, it only uses one core)
- if given multiple cores, we can run multiple go routines at the same time

#### Channels

- channels help communicate between go routines to make sure the main routine doesn't stop while child go routines are still running
- channels are typed and can only transfer data of that single type

```go
// Channel Creation
c := make(chan string)
// Sending a channel value
channel <- 5
// Receiving a channel value
myNumber <- channel
```

- Important Note: if you have a function that prints out 5 different messages from a channel, five <- channel messages are required, one is insufficient

#### Packages

- package is a project or a workspace
- many files can be included in the same file, but the package they belong to must be declared at the top 
- two types of packages: executable, which produces an executable file, and helper, and reusable, code used as helpers and a good pace to put reusable logic, can be seen as code dependencies or libraries 
    - the name of package you use determines what type of package you make (**main** is the only name to make an executable file)
    - main package must have a "main" function 
- **files in the same package can freely call functions of each other** 

### Testing with Go

- to make a test, create a new file ending with "_test.go"
- to run tests in a package, run the command, ``` go test ```
```go
// Test Example

func TestNewDeck(t *testing.T) {
    d := newDeck()
    if len(d) != 52 {
        t.Errorf("Expected deck length of 16, but got"< len(d))
    }
} 
```

## Package Functions

bufio Package

```go
func NewReader(rd io.Reader) *Reader // makes a reader for in-line arguments, accepts 'os.Stdin' as io.Reader argument

func (b *Reader) ReadString(delim byte) (string, error) // reads up to the first occurrence of delim, returning the string up to and including delim

// If using ReadString up to next new line, must use strings.Replace function to remove new line character
```

io/ioutil Package

```go
func ReadFile(filename string) ([]byte, error ) // reads a file 

func WriteFile(filename string, date []byte, perm os.FileMode) error // creates a file
// 0666 permission means anyone can read and write to file 
```

math/rand Package

```go
func Intn(n int) int // returns a random non-negative number from 0 to n

func NewSource(seed int64) Source // returns a new pseudo-random Source seeded 
// with the given value

func New(src Source) *Rand // returns a new Rand that uses random values from src to generate other random values
```

net/http Package

```go
func Get (url string) (resp *Response, err error)
```

os Package

```go
func Exit(code int) // causes current program to exit with given status code, 0 meaning success, non-zero meaning error
```

strings Package

```go
func  Join (a []string, sep string) string // reads a slice of strings into a single string 

func Replace(s, old, new string, n int) string // returns copy of s with the first n non-overlapping instances of old replaced by new, if n < 0, there is no limit on number of replacements 

funcSplit(s string, sep string) [] string // split slices s into all substrings seperated by sep and returns a slice of strings 
```

time Package

```go
func (t Time) UnixNano() int64 // returns time as a unix time 
```


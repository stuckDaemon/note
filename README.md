# INTRO

Imperative programming language. C++, Java and Python merged together.

# DATATYPE

Variable: a way to store and accessing information.

#### Numbers

```
int8	8-bit signed integer (-128 to -127)
int16	16-bit signed integer
int32	32-bit signed integer
int64	64-bit signed integer

uint8	8-bit unsigned integer
uint16	16-bit unsigned integer
uint32	32-bit unsigned integer
uint64	64-bit unsigned integer

int	    Both in and uint contain same size, either 32 or 64 bit.
uint	Both in and uint contain same size, either 32 or 64 bit.
rune	It is a synonym of int32 and also represent Unicode code points.
byte	It is a synonym of int8.
uintptr	It is an unsigned integer type. Its width is not defined, but its can hold all the bits of a pointer value.

float32	32-bit IEEE 754 floating-point number
float64	64-bit IEEE 754 floating-point number

complex64	Complex numbers which contain float32 as a real and imaginary component.
complex128	Complex numbers which contain float64 as a real and imaginary component.
```

#### String

```
"double quotation"
```

#### Booleans

```
true
false
```

To run memory optimised system, you should use the right datatype (eg. int8 rather than int64). With the syntax
`var number = 42` GoLang will automatically define the type of the variable.

When I declare a variable without giving it any value golang will populate it with the default value.

```
var number uint64   -> 0
var bl bool         -> false
```

# PRINT TO CONSOLE

Using `printf` as

```
fmt.Printf("Hello %T %v", 10, 10)
```

will generate the output `Hello int 10` where `%T` print out they Type and `%v` print out the value of the variable.

Using `sprintf` as

```
var x string = fmt.Sprintf(..., ...)
```

will allow us to save the output to a variable.

#### fmt cheat sheet

Default formats and type Value: []int64{0, 1}

```
Format	        Verb	Description
[0 1]	        %v	    Default format
[]int64{0, 1}	%#v	    Go-syntax format
[]int64	        %T	    The type of the value
```

Integer (indent, base, sign)
Value: 15

```
Format  Verb	Description
15	    %d	    Base 10
+15	    %+d	    Always show sign
␣␣15	%4d	    Pad with spaces (width 4, right justified)
15␣␣	%-4d	Pad with spaces (width 4, left justified)
0015	%04d	Pad with zeroes (width 4)
1111	%b	    Base 2
17	    %o	    Base 8
f	    %x	    Base 16, lowercase
F	    %X	    Base 16, uppercase
0xf	    %#x	Base 16, with leading 0x
```

Character (quoted, Unicode)
Value: 65   (Unicode letter A)

```
Format	Verb	Description
A	    %c	    Character
'A'	    %q	    Quoted character
U+0041	%U	    Unicode
U+0041 'A'	    %#U	Unicode with character
```

Boolean (true/false)

`Use %t to format a boolean as true or false.`

Pointer (hex)

`Use %p to format a pointer in base 16 notation with leading 0x.`

Float (indent, precision, scientific notation)
Value: 123.456

```
Format	        Verb	Description
1.234560e+02	%e	    Scientific notation
123.456000	    %f	    Decimal point, no exponent
123.46	        %.2f	Default width, precision 2
␣␣123.46	    %8.2f	Width 8, precision 2
123.456	        %g	    Exponent as needed, necessary digits only
```

String or byte slice (quote, indent, hex)
Value: "café"

```
Format	        Verb	Description
café	        %s	    Plain string
␣␣café	        %6s	    Width 6, right justify
café␣␣	        %-6s	Width 6, left justify
"café"	        %q	    Quoted string
636166c3a9	    %x	    Hex dump of byte values
63 61 66 c3 a9	% x	    Hex dump with spaces
```

Special values

```
Value	Description
\a	    U+0007 alert or bell
\b	    U+0008 backspace
\\	    U+005c backslash
\t	    U+0009 horizontal tab
\n	    U+000A line feed or newline
\f	    U+000C form feed
\r	    U+000D carriage return
\v	    U+000b vertical tab
```

# CONSOLE INPUT

Getting input from CLI. Perhaps a new scripting thing for me?

```go
package main

import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	bufio.NewScanner(os.Stdin)
	fmt.printf("Type something ")
	scanner.Scan() // Wait for input
	input := scanner.Text()
}
```

# LOOPs

Minimal for. (while loop)

```go
x := 3
for x<5{
x += 1
}
```

# SLICE

With standard array we need to define the size of that array when we created. Sometimes you might now know the size of
the array and it's really difficult to decide which size to pick. This is were `slice` is getting into.

```go
// This is an array
var x [5]int = [5]int{1, 2, 3, 4, 5}

// This is a slice cause we do not specify the size of it
var x []int = x[:]
```

` = x[:]` syntax means copy the whole content of the array x from the first till the latest element
` = x[1:]` syntax means copy th content of the array x from x[1] up to the latest element (2,3,4,5)
` = x[1:3]` syntax means copy th content of the array x from x[1] up to x[3] NOT INCLUDED (2,3)
` var a [int = []int{1,2,3,4,5,6,7}` valid syntax to define a slice of int

Once you define a slice, you are technically stuck with the dimension of the slice. In this case you can use the
function `append` to increase the capacity of the slice. It returns a slice with added an element at its very end.

```go
append(a, 10)
```

The `make` function represents an easier way to create a slice with a basic capacity of 5 elements

```go
a := make([int], 5)
```

# MUTABLE AND IMMUTABLE DATATYPES

Slices, Maps and Array are mutable data types but behave in different ways.

```go
var x []int = []int{3, 4, 5}
y := x
y[0] = 100
fmt.Println(x, y)

// OR
var x map[string]int = map[string]int{"A":1}
y := x
y["B"] = 2
fmt.Println(x, y)
```

this snippet will print `[100, 4, 5] [100, 4, 5]` and `map[A:1 B:2] map[A:1 B:2]`.

With the syntax `y:=x` I am saying is y is equal to the slice x is pointing to. This means x and y are pointing to the
same variable.

On the opposite hand the following snippet code
```go
var x [2]int = [2]int{3, 4}
y := x
y[0] = 100
fmt.Println(x, y)
```
prints `[3,4] [100,4]`. with the syntax `y := x` it produce a copy of in y.


```go
func changeFirst(slice []int){
    slice[0] = 1000
}

func main(){
    var x []int = int[]{3,4,5}
    fmt.Println(x)
    changeFirst(x)
    fmt.Println(x)
}
```
The output is `[3 4 5] [1000 4 5]`. I modify the value of the value in x


# FUNCTIONS

Function are themself a data type. This is a way to store functions.

```go
func test(){
    fmt.Println("hello")
}

func main(){
    test()      // -> call the function
    x := test   // -> reference x as function datatype
    x()         // -> valid thing to do
}
```

Create a function inside another function.
```go

func main(){
    test := func(){
        fmt.Println("hello")
    }
    test()
}
```

Make a function returning something
```go
func main(){ 
	
    test := func(x int) int{
        return x * -1
    }(8)                // Call the function directly and assign the value inside test
    fmt.Println(test)    // -8
}
```

Passing a function to another function
```go
func test2(myFunc func(int) int){
    fmt.Println(myFunc(7))
}

func main(){ 
	
    test := func(x int) int{
        return x * -1
    }(8)                // Call the function directly and assign the value inside test
    test2(test)         // -7
}
```


# POINTERS AND DEFERENCE OPERATORS (& and *)

```go
func main(){
    x := 7
    y := &x             // data type *int
    fmt.Println(x, y)   // 7 0xc000001001a0
	*y = 8
    fmt.Println(x, y)   // 8 0xc000001001a0
}
```

```go
func changeValue(str *string){
    *str = "changed!" 
}

func changeValue2(str string){
    str = "changed!"
}

func main(){
    toChange := "hello"     // toChange = hello
    changeValue(&toChange)  // toChange = changed!
    changeValue2(toChange)  // toChange = changed!
}
```



# STRUCTS AND CUSTOM TYPES

The following snippet shows how with structs we can avoid to de-reference the value of the variable to change its
value. That mean `(*p1).x = 8` produces the same output of `p1.x = 8`. (same thing if you pass `p1` to a function)
```go
type Point struct {
    x int32
    y int32
}

func main(){
    p1 := &Point{y:3}   // p1 = {0 3}
	p1.x = 8            // p1 = {8 3}
}
```


Getter/Setter and some weird magic to understand struct reference
```go
type Student struct{
    name string
    grades []int
    age int
}

// Function acts on Student object.
func (s Student) getAge() int {             // This `s` refers to whichever Student I call it against. (JAVA getter?)
    return s.age
}

func (s *Student) setAge(age int) int {     // You need a pointer to MODIFY the object
    s.age = age
}

func (s Student) getAverageGrade() float32 {
    sum := 0
	for _, v := range s.grades{
		sum += v
    }
    return float32(sum) / float32(len(s.grades))
}


func main() {
    s1 := Student{"Tim", []int{29,28,19,30,30}, 22}
    s1.getAge()          // 22
    s1.setAge()          // 30
    s1.getAge()          // 30
    
    s1.getAverageGrade() // 27.2
	
}
```


# INTERFACES

A way of looking at a set of related object or types

```go
type circle struct {
    radius float64
}

type rect struct {
    width float64
    height float64
}

func (r rect) area() float64 {
	return r.width * r.height
}

func (c circle) area() float64{
    return math.Pi * c.radius * c.radius
}

func main() {
    c1 := circle {4.5}
    r1 := rect{5,7}
    
    // 1. We need to define a type
    shapes := []type{c1,r1}
    // 2. I don't know the type but I want to call something like
    shapes[0].area()
    // 3. Let's solve with interface. Next snippet
}

```

```go
type shape interface {
    area() float64
}

type circle struct {
    radius float64
}

type rect struct {
    width float64
    height float64
}

func (r rect) area() float64 {
	return r.width * r.height
}

func (c circle) area() float64{
    return math.Pi * c.radius * c.radius
}

func main() {
    c1 := circle {4.5}
    r1 := rect{5,7}

    shapes := []shape{c1,r1}
    shapes[0].area()
	
}
```
In this example there is somehting worth to be mentioned. If I access the object from the shapes array (`shapes[0]`) I 
can only call methods defined in the `shape` interface.
`shapes[0].area()` this is valid
`shapes[0].radius` this is invalid cause `radius` is not defined in  `shape` interface. If I want to access the radius
of `c1` I need to write `c1.radius`

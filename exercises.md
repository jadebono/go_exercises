# `100 Golang Exercises`

Adapted from the [Python Exercises of Jeffrey Hu](https://github.com/zhiwehu/Python-programming-exercises).
[Github: Jeffrey Hu](https://github.com/zhiwehu)

Adapted by: [Joseph Anthony Debono](https://github.com/jadebono).
[Email Joseph](joe@jadebono.com)

These are the exercises with the standard solutions. Class-based (OOP) solutions are kept at a minimum and only as the exercise at that point.

1. The README file: [README.md](./README.md);
1. Object Oriented Programming solutions: [OOP exercises and solutions](./OOP.md)

---

## Question 1

Question:  
Write a program which will find all such numbers which are divisible by 7 but are not a multiple of 5, between 2000 and 3200 (both included). The numbers should be stored in a slice and the slice printed out at the end of the program.

Hints:

1. To create a slice, use make();
1. make() takes three args: type, length, capacity:
   i. Type, such as []int;
   ii. Length, if 0, then its empty, otherwise it will populate the slice with as many elements of zero value as defined;
   iii. Capacity, the max number of elements the slice can take;
   iv. Capacity is optional.

Solution:

```golang
package main

import "fmt"

// declare type of return between parentheses and bracer
func parseNumbers() []int {
	// make() creates a slice (or array), 2nd arg defines length
	// it can also take a 3rd arg for capacity.

	var mySlice = make([]int, 0)
	for i := 2000; i <= 3200; i++ {
		if i % 7 == 0 && i % 5 != 0 {
			// append() allows you to append i to mySlice thus:
			mySlice = append(mySlice, i)
			}
	}
	return mySlice
}

func main() {
	ans := parseNumbers()
	fmt.Println(ans)
}
```

---

## Question 2

Question:  
Write a program that returns two named returns (of whatever type you like) to the main func using naked return.

Hints:

1. To use a naked return, give a name to the return values in the func declaration and then just invoke return at the end of the func.

Solution:

```golang
package main

import (
	"fmt"
)

// naming return values makes it possible to return them by just invoking return
func addNums(a, b int) (sum int, ans string) {
	sum = a + b
	ans = fmt.Sprint("The answer to your sum is:")
	return
}


func main() {
	a := 5
	b := 10
	sum, ans := addNums(a, b)
	fmt.Println(ans, sum)
	}
```

---

## Question 3

Question:
Write a program with three functions:

1. WelcomeMessage() - takes the name of a customer as an arg and returns the following message: "Hello there, CUSTOMER!"
1. addBorder() - takes two args, a welcome message and an int expressing the number of stars to put above and below the welcome message like this:

```bash
***
hello!
***
```

1. cleanupMessage() takes the message below as an arg and returns it stripped away all the stars and spaces:

```bash
**************************
*    BUY NOW, SAVE 10%   *
**************************
```

Hints:

1. To create a string literal in go, use fmt.Sprintf using verbs:
   age := 30
   name := Joseph
   myStringLiteral := fmt.Sprintf("Hi, my name is %v and I am %v years old", name, age);
1. To create a string composed of multiple lines without using \n, use ticks ``.

Solution:

```golang

package main

import (
	"fmt"
	"strings"
)

// WelcomeMessage returns a welcome message for the customer.
func welcomeMessage(customer string) string {
	// returning the string literal
    return fmt.Sprintf("Welcome to the Tech Palace, %v", strings.ToUpper(customer))
}

func addBorder(welcomeMsg string, numStarsPerLine int) string {
	// strings.Repeat repeats char for int number of times
	border := strings.Repeat("*", numStarsPerLine)
	return fmt.Sprintf("%v\n%v\n%v", border, welcomeMsg, border)
}

func cleanupMessage(oldMsg string) string {
	// strings.ReplaceAll replaces all iterations in string of char with char
	noStarsMsg := strings.ReplaceAll(oldMsg, "*", " ")
	// trim leading and trailing whitespaces
	return strings.TrimSpace(noStarsMsg)
}

func main() {
	// create the welcome message with a customer's name
	customer := welcomeMessage("Joseph")
	// creating the welcome border with the message and int for the number of stars
	welcomeBorder := addBorder("Welcome!", 10)
	// creating the message with stars and spaces to be stripped away
	message := `
**************************
*    BUY NOW, SAVE 10%   *
************************** `
	//the stripped message
	cleanMessage := cleanupMessage(message)
	fmt.Println(customer)
	fmt.Println(welcomeBorder)
	fmt.Println(cleanMessage)

}
```

---

## Question 4

Question:  
Write a program that declares and initializes an integer variable in the local scope of the main func. Then it passes a pointer to a double() function that will double the value of the integer variable by updating the value at the pointer. This will then update the value of the variable in the local scope of the main func without returning anything from the double() func.

Hints:

1. create a pointer to a variable by prefixing the variable with &. This becomes a new variable containing the address of the original variable;
1. The type to a pointer is the variable prefixed by a *. Hence the type of a pointer to an int is *int;
1. Beware the confusion from dereferencing (obtaining) the value at the pointer, which is done by prefixing the pointer var (containing the address) with \*, and the type of the pointer which is the variable type prefixed by \*.

Solution:

```golang
package main

import (
	"fmt"
)

// the double func is defined with a parameter that is a pointer of type int
func double(n *int) {
	// the variable *n here is the value dereferenced from the pointer
	*n *= 2
}

func main() {
	num := 6
	double(&num)
	// since the arg passed to the double func is a pointer to a num variable in local
	// scope of main, the double func changes the value in the num variable all the same
	fmt.Println(num)
}
```

---

## Question 5

Question:  
Write a program which can compute the factorial of a given numbers.
Suppose the following input is supplied to the program: 8
Then, the output should be: 40320

Solution:

```golang
package main

import "fmt"

func fac(n int) int{
	if n == 0 {
		return 1
	} else {
		return n * fac(n-1)
	}
}

func main() {
	// create the var for the user input
	var inpt float64
	fmt.Println("Please enter an int to factorialize (floats will be truncated to ints):\t")
	// fmt.Scan() takes a single char or word from input and assigns it to the pointer
	// in the parentheses. The two underscores are blanks for the two returns.
	_, _ = fmt.Scan(&inpt)
	factorial := fac(int(inpt))
	fmt.Println(factorial)
}
```

---

## Question 6

Question:  
With a given integer number n, write a program to generate a map that contains (i, i\*i) such that is an integer number between 1 and n (both included). The key should be a string. Once the map is created, convert it to a JSON object and then print out the JSON object

Suppose the following input is supplied to the program: 8

Then, the output should be: {"0":0,"1":1,"2":4,"3":9,"4":16,"5":25,"6":36,"7":49,"8":64}

Hints:

1. While the fmt package will print the keys of the map in their original order, this order is lost when you JSONify the map.

Solution:

```go
package main

import (
	"encoding/json"
	"fmt"
	"math"
	"strconv"
)

// this func takes the user input and returns it to the main func
func getUserInput() int {
	var userInput string
	fmt.Println("Please input an integer\t")
	// use fmt.Scan to take a single input from the user and set it to the pointer to
	// to the userInput var
	_, _ = fmt.Scan(&userInput)
	// convert the string to a float64 - this will return an error if the userInput
	// var cannot be converted to a float )
	convInput, _ := strconv.ParseFloat(userInput, 64)
	// round convInput, convert it to an int and return
	return int(math.Round(convInput))
}

// takes an int arg and turns it into a map as a sequence of  i: i*i
func createMap(n int) map[int]int {
	// create a map (a data structure with keys and values)
	myMap := make(map[int]int)
	for i:= 0; i <= n; i++ {
		myMap[i] = i * i
	}
	return myMap
}


// take a map of key int: val int and turn it into a JSON obbject
func createJSON(myMap map[int]int) string {
	// json.Marshal returns a byte array and an error
	barr, _ := json.Marshal(myMap)
	// convert byte array to a string and return it
	return string(barr)
}

func main() {
	// get an int from user input
	num := getUserInput()
	// create a map from the user input
	myMap := createMap(num)
	// create the JSON object from the map
	myJSON := createJSON(myMap)
	// print the JSON object
	fmt.Println(myJSON)
}
```

---

## Question 7

Question:  
Write a program which declares and initialises a sequence of comma-separated numbers. Then use that sequence to generate an array and a JSON object which contains every number.

Example:  
Suppose the following input is supplied to the program:
34,67,55,33,12,98

Then, the output should be:
['34', '67', '55', '33', '12', '98']
{"12":12,"33":33,"34":34,"55":55,"67":67,"98":98}

Hints:  
Golang will automatically sort your map keys in numerical order:
{"12":12,"33":33,"34":34,"55":55,"67":67,"98":98}

Solution:

```golang
package main

import (
	"encoding/json"
	"fmt"
	"strconv"
	"strings"
)

// transform the sequence of numbers into an array and return it to the main func
func outputArray(seq string) []string {
	// strings.Split returns an array
return strings.Split(seq, ",")
}

// transform the sequence of numbers into a JSON object and return to the main func
func outputJSON(seq []string) string {
	// create map
	var seqMap = make(map[int]int)
	// populate map with the required key:value pairs
	for i := 0; i < len(seq); i++ {
		// converts str to int in a given base and bit size
		n, _ := strconv.Atoi(seq[i])
		seqMap[n] = n
	}
	// convert map into a JSON object
	barr, _ := json.Marshal(seqMap)
	// return JSON object
	return string(barr)
}

func main() {
	var mySequence = "34,67,55,33,12,98"
	var mySeqArr = outputArray(mySequence)
	var mySeqJSON = outputJSON(mySeqArr)
	fmt.Println(mySeqArr)
	fmt.Println(mySeqJSON)
}
```

---

## Question 8

Question:  
Write a program that calculates and prints the value according to the given formula:
Q = Square root of [(2 * c * d)/h]

- The fixed values of c and h: c is 50, h is 30.
- d is the variable whose values should be input to your program in a comma-separated sequence.

Example:  
Let us assume the following comma separated input sequence is given to the program: 100,150,180
The output of the program should be: 18,22,24

Hints:

1. If the output received is in decimal form, it should be rounded off to its nearest value for example, if the output received is 26.0, it should be printed as 26).

Solution:

```golang
package main

import (
	"fmt"
	"math"
	"strconv"
	"strings"
)

// convert string array to float64 slice and return it
func convertStrArrToFlt(arr []string) []float64 {
	//create slice of type float64 and dynamic size
	seqSlice := make([]float64, 0)
	for i := 0; i < len(arr); i++ {
		// convert each elem in arr to float64
		val, _ := strconv.ParseFloat(arr[i], 64)
		// append each new float64 to slice
		seqSlice = append(seqSlice,  val)
	}
	return seqSlice
}

// take float64 slice, run it through the formula, and return it as a new joined string
func formula(slc[] float64) string {
	// define values of formula
	var c float64 = 50
	var h float64 = 30
	//define q slice of type string
	q := make([]string, len(slc))
	// compute this formula for every one of the values in slc[]:
	// √[(2 * c * slc[i])/h]
	for i:= 0; i < len(slc); i++ {
		ansFloat := math.Sqrt((2 * c * slc[i])/h)
		// convert float64 to string with verb %.0f - float with 0 digits after point
		ansStr := fmt.Sprintf("%.0f", ansFloat)
		q[i] = ansStr
	}
	// use strings.Join() to join q string slice with , and return it
	return strings.Join(q, ",")
}

func main() {
		// define seq of comma-separated values and turn it into an array of ints
	var stringSeq string = "100,150,180"
	// transform csv string into a string array and turn it into a float64 slice
	Fl64Slc := convertStrArrToFlt(strings.Split(stringSeq, ","))
	// send the Float64[] to be run through the formula
	formSlc := formula(Fl64Slc)
	fmt.Println(formSlc)
}
```

---

## Question 9

Question:  
Write a program that takes 2 digits, X,Y as input and generates a 2-dimensional array. The element value in the i-th row and j-th column of the array should be i\*j. The two digits should be supplied by the user.

Example:  
Suppose the following inputs are given to the program:
3,5
Then, the output of the program should be:
[[0, 0, 0, 0, 0], [0, 1, 2, 3, 4], [0, 2, 4, 6, 8]]

Hints:

1. Arrays in goland are fixed-length sequences of items of the same type and they are values;
1. Slices are like arrays (or slices of the same array) but are of variable length. They can be resized using append() and they are reference types;
1. Use slices not arrays for this;
1. But tell user that the supplied inputs will be for arrays.

Solution:

```golang
package main

import (
	"fmt"
	"math"
)

// func to take user input
func userInput() int {
	// declare userInput as a float64
	var userInput float64
	_, _ = fmt.Scan(&userInput)
	// math.Round() rounds up a float
	userInput = math.Round(userInput)
	// convert userInput from float64 to int to return it
	return int(userInput)
}

// func to create the 2D slice
func createSlc(rows, cols int) [][]int {
	// make a 2d slice
	slc := make([][]int, 0)
	// start the outer loop
	for i := 0 ; i < rows ; i++ {
	// create the internal slice
	slcIn := make([]int, 0)
		for j := 0 ; j < cols ; j++ {
		// append i * j to slcIn  slice
		slcIn = append(slcIn, i*j)
	}
	// append the current slcIn slice to arr
	slc = append(slc, slcIn)

}
	// return arr
	return slc
}

// main func
func main() {
	// tell user to supply two inputs of type integer. Also tell user that supplied
	// floats will be rounded and converted to integers
	fmt.Println("This program will create a 2D array from two integers you supply.")
	fmt.Println("Please input an integer. A Float will be rounded to the nearest int:\t")
	rows := userInput()
	cols := userInput()
	twoDimSlice := createArray(rows, cols)
	fmt.Println(twoDimSlice)
}

```

---

## Question 10

Question:  
Write a program that accepts a comma separated sequence of words as input and prints the words in a comma-separated sequence after sorting them alphabetically. The input should be taken from the user.

Example:  
Suppose the following input is supplied to the program:
without,hello,bag,world
Then, the output should be:
bag,hello,without,world

Solution:

```golang
package main

import (
	"fmt"
	"sort"
	"strings"
)

// create the array of strings from the myStr arg and return string array
func splitStr(myStr string) []string {
	return strings.Split(myStr, ",")
}

// func to sort slice and then return it as comma separated string
func processSlice(strArr []string) string {
	// sort arr - strings.Sort() sorts array in place
	sort.Strings(strArr)
	// strings.Join() joins the elements of an array/slice with a supplied separator
	// and returns it as a string
	sortedStr := strings.Join(strArr, ",")
	return sortedStr
}

func main() {
	myStr := "without,hello,bag,world"
	// create string array
	strArr := splitStr(myStr)
	// sort array and return it as a comma-separated string
	sortedStr := processSlice(strArr)
	fmt.Println(sortedStr)
}

```

---

## Question 11

Question:  
Write a program that accepts sequence of lines as input and prints the lines after making all characters in the sentence capitalized.

Example:  
Suppose the following input is supplied to the program:
Hello world
Practice makes perfect
Then, the output should be:
HELLO WORLD
PRACTICE MAKES PERFECT

Hints:

1. Get the input from the user;
1. fmt.Scan() only takes a single char or word so it is not suitable for this task;
1. To take a string of more than one char/word use the bufio package.

Solution:

```golang

package main

import (
	"bufio"
	"fmt"
	"os"
	"strings"
)

func takeInput() string {
	// create the reader from bufio.NewReader(os.Stdin) to read a string from the user
	reader := bufio.NewReader(os.Stdin)
	fmt.Println("Please input a string to be capitalized:\t")
	// user reader to read a string from the user. The '\n' is the delimiter,
	// indicating how far the reader should read
	userInput, _ := reader.ReadString('\n')
	// return the userInput after using strings.TrimSpace to trim leading and trailing
	return strings.TrimSpace(userInput)
}

func capitalizeInput(input string) string {
	// return the capitalized input
	return strings.ToUpper(input)
}

func main() {
	input := takeInput()
	capitalized := capitalizeInput(input)
	fmt.Println(capitalized)
}
```

---

## Question 12

Question:  
Write a program that accepts a sequence of whitespace separated words as input and prints the words after removing all duplicate words and sorting them alphanumerically.

Example:  
Suppose the following input is supplied to the program:
hello world and practice makes perfect and hello world again
Then, the output should be:
again and hello makes perfect practice world

Hints:

1. You can either take the words as an input from the user or define them in the main func;
1. The strategy for this solution is:
   1. turn the input string into an array;
   1. sort the array;
   1. create an empty slice of size 1 to stop the compiler panicking;
   1. append the first element of the sorted array to the slice[1];
   1. then compare the subsequent elements of the sorted array to the len(slice)-1 and append that element to the slice IF the element is not the same.

Solution:

```golang
package main

import (
	"fmt"
	"sort"
	"strings"
)

// splits a string turning it into an array, sorts it and returns the sorted array
func sortString(input string) []string {
	inputArr := strings.Split(input, " ")
	sort.Strings(inputArr)
	return inputArr
}

// takes the sorted array as the param, creates a new slice, populates the slice with
// unique elements from the inputArr, and returns the new slice with unique elements
func filterArr(inputArr []string) []string {
	// create a new slice but give it a size of at least 1 because the compiler panics
	// when you try to append elements from inputArr
	inputSlice := make([]string, 1)
	// append the first element of inputArr to inputSlice
	inputSlice = append(inputSlice, inputArr[0])

	for i := 0; i < len(inputArr); i++ {
		// if elem inputArr[i] != to the current LAST elem of inputSlice, append it to
		// inputSlice
		 if inputArr[i] != inputSlice[len(inputSlice)-1] {
			  inputSlice = append(inputSlice, inputArr[i])
		 }
	}
	// return the slice without the first element which is an empty one
	return inputSlice[1:]
}

// joins the slice of unique sorted strings and returns it as a string
func sliceJoin(mySlice []string) string {
	return strings.Join(mySlice, " ")
}

func main() {
	// takes input, you can create a func to take input from user if you like
	input := "hello world and practice makes perfect and hello world again"
	// turn the input string into a sorted array
	output := sortString(input)
	// turn the sorted array into a slice of sorted unique elements
	filteredOutput := filterArr(output)
	// turn the sorted unique elements into a single string correlative to the input
	// string
	outputStr := sliceJoin(filteredOutput)
	fmt.Println(outputStr)
}
```

---

## Question 13

Question:  
Write a program which accepts a sequence of 4 comma-separated binary nibbles (a string of 4 bits) as its input and then check whether they are divisible by 5 or not. The nibbles that are divisible by 5 are to be printed in a comma separated sequence.

Example:  
0100,0011,1010,1001
Then the output should be:
1010

Hints:

1. The string of 4 nibbles should be inputted by the user;
1. As such add error handling to make sure that the input submitted by the user conforms to the format "nibble,nibble,nibble,nibble", ex: "0100,0011,1010,1001";
1. If the submitted input does not conform, return an error message to say so and stop the code;
1. You will have to convert the input from a string to bits;
1. strvconv.ParseInt() converts from a string to an int64 of whatever base you need;
1. strvconv.FormatInt() converts from an int64 of whatever base you have to a string.

Solution:

```golang
package main

import (
	"fmt"
)

// validate original input
func validInput(input string) bool {
	// check that the string contains:
	// (1) length of 19 chars; (2) 3 "," chars  (3) 16 incidences of either 1 or 0
	// convert input string into a string array with one element
	strIn := strings.Split(input, "")
	// check length of strIn
	lengthInput := len(strIn)
	var comma, bit int
	for i:= 0; i < lengthInput; i++ {
		// count the number of chars that are either 1 or 0
		if strIn[i] == "1" || strIn[i] == "0" {
			bit += 1
		}
		// count the number of chars that are ,
		if strIn[i] == "," {
			comma += 1
		}
	}
	// if vars are of the required size, return true
	if lengthInput == 19 && comma == 3 && bit == 16 {
		return true
	} else {
		// else return true
		return false
	}
}


// take input from user and return a string array and an error message
func userInput() ([]string, error) {
	var inputStr string
	fmt.Println("Please input a sequence of binaries separated by commas")
	_, _ = fmt.Scan(&inputStr)
	// test inputStr by submitting it to validInput that returns true/fale
	checkInput := validInput(inputStr)
	// if checkInput is false, return a string arr containing 0 and an error msg
	if !checkInput {
		return []string{"0"}, fmt.Errorf("%v is an invalid input as it does not consist of 4 nibbles separated by a comma", inputStr)
	} else {
		// else return the input str split into a string arr and an err msg of nil
		return strings.Split(inputStr, ","), nil
	}
}

func convArr(input []string) []int {
	intSlice := make([]int, 0)
	// convert every element in input to a decimal int
	for i:= 0; i < len(input); i++ {
		// convert every element into int64 from a base-2
		binInput, err := strconv.ParseInt(input[i], 2, 8)
		if err != nil {
			log.Fatal(err)
		}
		// convert the base-2 int64 into an int and append it to intSlice
		intSlice = append(intSlice, int(binInput))
	}
	return intSlice
}


func divSlice(intSlice []int) string{
	newSlice := make([]string, 0)
	// start looping through intSlice and check if the elements are divisible by 5
	for i := 0; i < len(intSlice); i++{
		if intSlice[i] % 5 == 0 && intSlice[i] != 0 {
			// if div by 5, use .FormatInt to convert elem from a base-2 int64 to str
			nib := strconv.FormatInt(int64(intSlice[i]), 2)
			// append element to newSlice
			newSlice = append(newSlice, nib)
		}
	}
	// if newSlice is empty, return a message saying so
	if len(newSlice) == 0 {
		return "No nibble in the submitted string is divisible by 5"
		} else {
			// else return the newSlice joined into one str by ","
			return strings.Join(newSlice, ",")
		}
}

func main() {
	// get user input. The second return value contains a validation check
	input, err := userInput()
	// if err is anything but nil, print the err and exit
	if err != nil {
		fmt.Println(err)
	// otherwise run through the rest of the code
	} else {
	// put the string arr received from userInput() into the convArr() func
	intSlice := convArr(input)
	// put the int arr received from conVarr() into the divSlice() func
	result :=divSlice(intSlice)
	// print the result
	fmt.Println(result)
	}
}
```

---

## Question 14

Question:  
Write a program, which will find all such numbers between 1000 and 3000 (both included) such that each digit of the number is an even number.
The numbers obtained should be printed in a comma-separated sequence on a single line.

Hints:

1. 0 digits are to be considered even.

Solution:

```golang
package main

import (
	"fmt"
	"strconv"
	"strings"
)

// takes the number, and returns true if each of its digits is divisble by 2, false
// otherwise
func checkEvens(n int) bool {
	// turn int into string
	intStr := strconv.Itoa(n)
	length := len(intStr)
	// split string into arr
	strArr := strings.Split(intStr, "")
	// start for loop to check each digit in the string
	for i := 0; i < length; i++ {
	// convert string element into int
		elemInt, _ := strconv.Atoi(strArr[i])
	// if int is NOT even, return false immediately
		if elemInt % 2 != 0 {
			return false
		}
	}
	// return true
	return true
}

// takes ints a and b, checks each number between them, and if each digit of that number
// is divisble by 2, then add it to a string slice, and return the slice joined into a
// comma-separated string
func findEvens(a, b int) string {
	// create string slice
	sliceStr := make([]string, 0)
	// start for loop
	for i := a; i <= b; i++ {
		// submit i to checkEvens func
		testElem := checkEvens(i)
		if testElem {
			sliceStr = append(sliceStr, strconv.Itoa(i))
		}
	}
	return strings.Join(sliceStr, ",")
}

func main() {
	evens := findEvens(1000,3000)
	fmt.Println(evens)
	}
```

---

## Question 15a

First of a set of four questions on using classes in Golang

Question (Creating a simple object):  
Create a simple struct with simple data types. Define the struct in global scope, and instantiate a instance of that struct in the main func.

Hints:

1. Go does not have classes but there are ways of implementing classes in Go. This question works you through the creating a class using different functionalities that Go makes available to you;
1. The first step to creating a class is using Go's struct functionality.

Solution:

```golang

package main

import (
	"fmt"
)

// creating the struct in global scope
type person struct {
	fname, sname string
}

func main() {
	john := person{fname: "John", sname: "Doe"}
	fmt.Println(john, john.fname, john.sname)
}

```

---

## Question 15b

Second of a set of four questions on using classes in Golang

Question (encapsulation):  
Create two structs. One should be externally available, the other available only internally. Define the structs in global scope, and instantiate a instance of each struct in the main func.

Hints:

1. Encapsulation means hiding or making available functions, methods, fields;
1. In Go, capitalizing the first letter of the func/method/field name makes it public and exported on the package level;
1. Otherwise, they remain private members of that package;
1. For the solution to this question extend the code of the solution to Question 14a.

Solution:

```golang
package main

import (
	"fmt"
)

// creating a public (externally accessible) struct in global scope
type Country struct {
	name, continent string
}

// creating a private (internal) struct in global scope
type person struct {
	fname, sname string
}

func main() {
	john := person{fname: "John", sname: "Doe"}
	eng := Country{name: "England", continent: "Europe"}
	fmt.Println(eng, eng.name, eng.continent)
	fmt.Println(john, john.fname, john.sname)
}

```

---

## Question 15c

Third of a set of four questions on using classes in Golang

Question (Inheritance):  
For each of the two structs you have already created, create a sub-struct. The encapsulation of each should be same as that of the parent struct. Define the structs in global scope, and instantiate a instance of each struct in the main func.

Hints:

1. Inheritance is when a class acquires the properties of its superclass. To achieve this in Go, you have to create a struct within a struct;
1. For the solution to this question extend the code of the solutions to Question 14a and 14b.

Solution:

```golang
package main

import (
	"fmt"
)

// creating a public (externally accessible) struct in global scope
type Country struct {
	Name, Continent string
	// nesting subclass
	Capital struct {
		Name string
		Population int
	}
}

// creating a private (internal) struct in global scope
type person struct {
	fname, sname string
	// nesting subclass
	details struct {
		phone, email string
	}
}

func main() {
	// instantiating person class
	john := person{fname: "John", sname: "Doe"}
	// instantiating details subclass inheriting from John
	john.details.phone = "346966556"
	john.details.email = "john@johndoe.com"
	// instantiating Country class
	eng := Country{Name: "England", Continent: "Europe"}
	// instantiating Capital subclass inheriting from Country
	eng.Capital.Name = "London"
	eng.Capital.Population = 9002488
	fmt.Println(john, john.fname, john.sname, john.details, john.details.phone, john.details.email)
	fmt.Println(eng, eng.Name, eng.Continent, eng.Capital, eng.Capital.Name, eng.Capital.Population)
}
```

---

## Question 15d

Fourth of a set of four questions on using classes in Golang

Question (Polymorphism):  
For each of the two structs you have already created, you need to provide methods. Remember that the method for the external struct has to be externally available itself, while the method for the internal struct must be likewise internal. You can provide the same functionality for both structs, or different functionality if you so please.

Hints:

1. Polymorphism is the provision of an interface to entities. Typical OOP languages allow you to define methods to a class within its structure;
1. In Go, you have to first define the interface and the method within it;
1. Then you have to create a func that takes the struct that the method is interfacing it with the struct as its parameter, and the method following it;
1. For the solution to this question extend the code of the solutions to Question 14a, 14b, and 14c.

Solution:

```golang

package main

import (
	"fmt"
)

// creating a public (externally accessible) struct in global scope
type Country struct {
	Name, Continent string
	// nesting subclass
	Capital struct {
		Name string
		Population int
	}
}

// creating an external interface to provide a method to an external struct
type GetSet interface {
	Get() string
}

// creating a private (internal) struct in global scope
type person struct {
	fname, sname string
	// nesting subclass
	details struct {
		phone, email string
	}
}

// creating an internal interface to provide a method to an internal struct
type getSet interface {
	get() string
}

//func to use get() from getSet internal interface on person struct
func (person person) get() string {
	return fmt.Sprintf("The user's full name is %v %v, his phone is: %v, and his email is: %v.", person.fname, person.sname, person.details.phone, person.details.email)
}

//func to use Get() from GetSet internal interface on person struct
func (Country Country) Get() string {
	return fmt.Sprintf("%v is a country in %v, its capital is: %v, and the population of %v is: %v.", Country.Name, Country.Continent, Country.Capital.Name, Country.Capital.Name, Country.Capital.Population)
}

func main() {
	// instantiating person class
	john := person{fname: "John", sname: "Doe"}
	// instantiating details subclass inheriting from John
	john.details.phone = "346966556"
	john.details.email = "john@johndoe.com"
	// instantiating Country class
	eng := Country{Name: "England", Continent: "Europe"}
	// instantiating Capital subclass inheriting from Country
	eng.Capital.Name = "London"
	eng.Capital.Population = 9002488
	fmt.Println(john, john.fname, john.sname, john.details, john.details.phone, john.details.email)
	fmt.Println(eng, eng.Name, eng.Continent, eng.Capital, eng.Capital.Name, eng.Capital.Population)
	// use get() from getSet interface to person struct
	johnFullName := john.get()
	// use Get() from GetSet interface to Country struct
	engFullDetails := eng.Get()
	fmt.Println(johnFullName)
	fmt.Println(engFullDetails)
}

```

---

## Question 16

Question:  
Write a program that accepts a sentence and calculate the number of letters and digits. Suppose the following input is supplied to the program: hello world! 123 Then, the output should be: LETTERS 10 DIGITS 3

Hints:

1. Take the sentence from user input;
1. There is no need to validate user input in this case. If there are no letters and digits, output a message to say so;
1. unicode.IsLetter and unicode.IsDigit checks if the rune of a character is a letter and digit;
1. A rune is an alias for an int32 type that represents a Unicode code point;
1. You can choose to output the result as both a struct and a map. This solution outputs in both forms.

Solution:

```golang
package main

import (
	"bufio"
	"fmt"
	"os"
	"unicode"
)

// declare results struct
type results struct {
	LETTERS, DIGITS int
}

// func for testing string to see if contains any letters and/or digits. If so,
// returns true else false
func testString(input string) bool {
	for _, a := range input {
		// use unicode.Isletter and unicode.IsDigit to see if char is letter/digit
		if unicode.IsLetter(a) || unicode.IsDigit(a) {
			return true
		}
	}
	return false
}

// return the string and a bool to indicate whether the input string contains letters
// and digits, or not.
func userInput() (string, bool) {
	fmt.Println("Please input a string. The program will report the number of letters and digits in the string.")
	reader := bufio.NewReader(os.Stdin)
	// no need to capture the error here
	input, _ := reader.ReadString('\n')
	//  return the input string and the result of the testString() func
	return input, testString(input)
}

// compute the results and output them in a map
func outputMaps(input string) map[string]int {
	mapResult := make(map[string]int)
	mapResult["LETTERS"] = 0
	mapResult["DIGITS"] = 0
	for _, char := range input {
		if unicode.IsLetter(char) {
			mapResult["LETTERS"] += 1
		} else if unicode.IsDigit(char) {
			mapResult["DIGITS"] += 1
		}
	}
	return mapResult
}

// compute the results and output them in a struct
func outputStruct(input string) results{
	stringResults := results{LETTERS: 0, DIGITS:0}
	for _, char := range input {
		if unicode.IsLetter(char) {
			stringResults.LETTERS += 1
		} else if unicode.IsDigit(char) {
			stringResults.DIGITS += 1
		}
	}
	return stringResults
}

func main() {
	// also return a bool indicating whether string contains letters/digits (true) or
	// not (false)
	getInput, test := userInput()
	// if !test, inform user and stop the code
	if !test {
		fmt.Printf("Your string is %v It is %v characters long but there are no letters and digits in your string. Stopping code here.", getInput, len(getInput))
		// otherwise analyse string and output results as map and struct
	} else {
		resultMaps := outputMaps(getInput)
		resultStruct := outputStruct(getInput)
		fmt.Printf("Your string is %v It is %v characters long.\n Your results in a map are: %v\n Your results in a struct are: Letters: %v, Digits: %v\n", getInput, len(getInput), resultMaps, resultStruct.LETTERS, resultStruct.DIGITS)
	}

}
```

---

## Question 17

Question:  
Write a program that accepts a sentence and calculate the number of upper case letters and lower case letters. Suppose the following input is supplied to the program: Hello world! Then, the output should be: UPPERCASE 1 LOWERCASE 9

Hints:

1. For this exercise the string should be provided by the user;
1. If there are no upper and/or lower case letters, just output 0 in the relevant field;
1. unicode.IsLower and unicode.IsUpper checks if a rune represents an upper or a lower case character;
1. You can choose to output the result as both a struct and a map. This solution outputs in both forms.

Solution:

```golang
package main

import (
	"bufio"
	"fmt"
	"os"
	"unicode"
)

// struct defined in global scope
type results struct {
	UPPERCASE, LOWERCASE int
}


func userInput() (input string) {
	reader := bufio.NewReader(os.Stdin)
	fmt.Println("Input a string for analysis:\t")
	input, _ = reader.ReadString('\n')
	return
}

// analyze the chars in the input string and naked return the number of upper and lower
// chars
func analyzeStr(input string) (upper, lower int) {
	for _, char := range input {
		if unicode.IsUpper(char) {
			upper += 1
		} else if unicode.IsLower(char) {
			lower += 1
		}
	}
	return
}

// create map to output the results in a map and naked return it
func mapResults(upper, lower int) (resultsMap map[string]int) {
	resultsMap = make(map[string]int)
	resultsMap["UPPERCASE"] = upper
	resultsMap["LOWERCASE"] = lower
	return
}

// create struct to output the results in a struct and naked return it
func structResults(upper, lower int) (resultStruct results ) {
	resultStruct.UPPERCASE = upper
	resultStruct.LOWERCASE = lower
	return
}

func main() {
	input := userInput()
	fmt.Print(input)
	upper, lower := analyzeStr(input)
	resultsMap := mapResults(upper, lower)
	resultStruct := structResults(upper, lower)
	fmt.Printf("Your string is: %vYour string is %v characters long.\nYour results in a map are: %v\nYour results in a struct are: Upper:%v Lower:%v\n" , input, len(input), resultsMap, resultStruct.UPPERCASE, resultStruct.LOWERCASE)
}

```

---

## Question 18

Question:  
Write a program that computes the value of a+aa+aaa+aaaa with the digit 9 substituted for the value of a . Suppose the following input is supplied to the program: 9 Then, the output should be: 11106

Hints:

1. For this question, that the string from the user;
1. However before you compute it, check every char to make sure that the every character in the string is either "a" or "+".
1. If the string fails this validation check, output message to that effect;
1. If the string is valid, submit to other functions to carry out the computation with the "a"s substituted by the digit 9.

Solution:

```golang
package main

import (
	"bufio"
	"fmt"
	"os"
	"strconv"
	"strings"
)

/* declaring and initiating the digit with which to substitute the characters in the
input string. The digit is declared as a string because the input string will be
split into a string array. The makeNines() func will then take as an argument each
individual element, substitute the digit with each char of the element, append it to
a string array, and then join it together as a single string that will then be
converted to an int in the makeNines() func
*/
var digit string = "9"

func userInput() (input string, valid bool) {
	reader := bufio.NewReader(os.Stdin)
	fmt.Print("Please input a string consisting of sequences of the character \"a\" concatenated with \"+\". The characters will be subsituted with the integer 9 and the expression computed. Inputs containing any other character will be rejected:\n")
	input, _ = reader.ReadString('\n')
	// trim whitespace because it will cause problems further on
	input = strings.TrimSpace(input)
	valid = validateStr(input)
	return
}

// func to validate that every char is either an "a" or an "+". This will be achieved
// by counting the number of "a"s and "+"s and comparing that num with len(strArr).
// "+" at the beginning or end of the string will reduce the count by 1 to ensure.
func validateStr(input string) bool {
	strArr := strings.Split(input, "")
	count := 0
	for i := 0; i < len(strArr); i++ {
		if strArr[i] == "a" || strArr[i] == "+" {
			count += 1
			} else {
			count += 0
			}
	}
	if strArr[0] == "+" || strArr[len(strArr)-1] == "+"{
		return false
		}
	if count == len(strArr) {
		return true
		}
	return false
	}

// func to convert each element of the argument supplied to computeResult() into a
// number substituted by 9 for each character
func makeNines(elem string) (num int) {
	numStr := make([]string, 0)
	for i := 0; i < len(elem); i++ {
		// the selected digit to substitute for the "a"s in each element is
		// inputted here.
		numStr = append(numStr, digit)
	}
	num, _ = strconv.Atoi(strings.Join(numStr, ""))
	return
}


// func to take the validated string and compute it
func computeResult(input string) (result int){
	// split string by +
	exprArr := strings.Split(input, "+")
	// declare a counter
	result = 0
	// start a loop
	for i := 0; i < len(exprArr); i++ {
		// submit each element to the makeNines func to get a num of 9s substited
		// for the "a"s in the elem
		num := makeNines(exprArr[i])
		// add the num to result
		result += num
	}
return
}


func main() {
	input, result := userInput()
	if (!result) {
		fmt.Printf("Your string is: %v but it is not valid since it contains characters other than \"a\" concatenated with \"+\".\n", input)
	} else {
		finalResult := computeResult((input))
		fmt.Println(finalResult)
	}
}

```

---

## Question 19

Question:

Write a program to take in a sequence of comma-separated numbers, and validate them. Then output them in:  
(a) An array or a slice containing ONLY the odd numbers squared;  
(b) A map[int][int] with keys consisting of only of the odd numbers out of the original ones, and the values of their squares;  
(c) As a string of comma-separated squares of the odd numbers of the original input.

Example:  
Suppose the following input is supplied to the program: 1,2,3,4,5,6,7,8,9 Then, the output should be:  
(a) As an array: [1 9 25 49 81];  
(b) As a map: map[1:1 3:9 5:25 7:49 9:81]  
(c) 1,9,25,49,81

Hints:

1. Take the input from the user and validate it.

Solution:

```golang
package main

import (
	"bufio"
	"fmt"
	"os"
	"strconv"
	"strings"
	"unicode"
)

func checkInput(input string) bool {
	inArr := strings.Split(input, "")
	counter := 0
	for i := 0; i < len(inArr); i++ {
		if inArr[i] == "," {
		counter += 1
		}
	}
	for _, r := range input {
		if unicode.IsDigit(r) {
			counter += 1
		}
	}
	if inArr[0] == "," || inArr[len(inArr)-1] == "," {
		counter -= 1
	}
	return counter == len(input)
}

func userInput() (input string, validatedInput bool) {
	reader := bufio.NewReader(os.Stdin)
	fmt.Println("Please input a string of comma-separated numbers. If your string contains anything else, it will be rejected:\t")
	input, _ = reader.ReadString('\n')
	input = strings.TrimSpace(input)
	validatedInput = checkInput(input)
	return
}

func makeArray(input string) []int {
	strArr := strings.Split(input, ",")
	odd2Arr := make([]int, 0)
	num := 0
	for i := 0; i < len(strArr); i++ {
		num, _ = strconv.Atoi(strArr[i])
		if num % 2 != 0 {
			odd2Arr = append(odd2Arr, num * num)
		}
	}
	return odd2Arr
}

func makeMap(input string) map[int]int {
	odd2Map := make(map[int]int)
	strArr := strings.Split(input, ",")
	num := 0
	for i := 0; i < len(strArr); i++ {
		num, _ = strconv.Atoi(strArr[i])
		if num % 2 != 0 {
			odd2Map[num] = num * num
		}
	}
	return odd2Map
}

func convIntArrToStr(input []int) string {
	convStr := make([]string, 0)
	for i := 0; i < len(input); i++ {
		convStr = append(convStr, strconv.Itoa(input[i]))
	}
	return strings.Join(convStr, ",")
}

func main() {
	input, result := userInput()
	if !result {
		fmt.Printf("Your string, which is %v, is invalid because it contains characters other than the required digits and commas.", input)
	} else {
		arrInput := makeArray(input)
		mapInput := makeMap(input)
		csvInput := makeArray(input)
		csvResult := convIntArrToStr(csvInput)
		fmt.Printf("The array of your input is: %v\n", arrInput)
		fmt.Printf("The map of your input is: %v\n", mapInput)
		fmt.Printf("The string of your input is: %v\n", csvResult)
	}
}
```

---

## Question 20

Question:  
Write an appointment scheduler for a beauty salon that opened on September 15th in 2021. The scheduler has five functions:

1. schedule(date string) - parse a textual representation of an appointment date into the corresponding time.Time format. Returns time.Time such as: 2019-07-25 13:45:00 +0000 UTC;
1. hasPassed(date string) - takes an appointment date and checks if the appointment was somewhere in the past. Returns bool;
1. isAfternoonAppointment(date string) - takes an appointment date and checks if the appointment in the afternoon (>= 12:00 && < 18:00). Returns bool;
1. description(date string) - takes an appointment date and returns a description of that date and time. Returns formatted string: "You have an appointment on Thursday, July 25, 2019, at 13:45.";
1. anniversaryDate() - returns the anniversary date of the salon's opening for the current year in UTC. Returns formatted spring: "2022-09-15 00:00:00 +0000 UTC"

Hints:

1. The reference date and time is: Monday, January 2, 2006 15:04:05;
1. Use time.Parse with a string formatted with a reference format such "1/02/2006 15:04:05". Ex: time.Parse("1/02/2006 15:04:05", date);
1. The date passed as an argument must match the layout:
   1. layout: "1/02/2006 15:04:05" - supplied date: "7/25/2019 13:45:00";
   1. layout: "Monday, January 2, 2006 15:04:05" - supplied date: "Monday, January 2, 2006 15:04:05";
1. time.Parse creates a time.Time type by parsing a layout and a supplied date;
1. time.Time.Format() takes a layout and returns a string.

Source: [History for go/exercises/concept/booking-up-for-beauty
](https://github.com/exercism/go/commits/main/exercises/concept/booking-up-for-beauty)

```golang
package main

import (
	"fmt"
	"time"
)

// Schedule returns a time.Time from a string containing a date
func schedule(date string) time.Time {
	// create the layout to parse the string into.
	// supplied date argument MUST match the defined layout
	layout := "1/02/2006 15:04:05"
	t, _ := time.Parse(layout, date)
	return t
}

// HasPassed returns whether a date has passed
func hasPassed(date string)  bool {
	// create the layout to parse.
	// supplied date argument MUST match the defined layout
	layout := "1/02/2006 15:04:05"
	// create the time.Time type
	d, _ := time.Parse(layout, date)
	// supply time.Now() to d.Before() for a boolean result
	return d.Before(time.Now())
 }

 // checks supplied date to see if it's in the afternoon
func isAfternoonAppointment(date string) bool {
	// create the layout to parse.
	// supplied date argument MUST match the defined layout
	layout := "Monday, January 2, 2006 15:04:05"
	// create the time.Time type
	d, _ := time.Parse(layout, date)
	// compared time.Time type with the hours between noon and 18:00
	if d.Hour() >= 12 && d.Hour() < 18 {
		return true
	}
	return false
}

// Description returns a formatted string of the appointment time
func description(date string) string {
	// create the layout to parse.
	// supplied date argument MUST match the defined layout
	layout := "1/2/2006 15:04:05"
	// create the time.Time type
	d, _ := time.Parse(layout, date)
	// create the string literal supplying a new layout to d.Format()
	return fmt.Sprintf("You have an appointment on %s", d.Format("Monday, January 2, 2006, at 15:04."))
}

// AnniversaryDate returns a Time with this year's anniversary
func anniversaryDate() time.Time {
	// create the layout to parse.
		layout := "2006-01-2"
	// create time.Time type by parsing defined layout with the string literal)
	t, _ := time.Parse(layout, fmt.Sprintf("%d-09-15", time.Now().Year()))
	return t
}

func main() {
	// create an appointment from a string and return it as a time.Time type
	appointment := schedule("7/25/2019 13:45:00")
	// check whether the scheduled appointment has passed
	appointmentHasPassed := hasPassed("July 25, 2019 13:45:00")
	// check whether the scheduled appointment is in the afternoon
	appointmentInAfternoon := isAfternoonAppointment("Thursday, July 25, 2019 13:45:00")
	// output a description of the appointment
	appointmentDescription := description("7/25/2019 13:45:00")
	// generate the date of the salon's decription this year
	anniversaryThisYear := anniversaryDate()
	// print the generated data:
	fmt.Println(appointment)
	fmt.Println(appointmentHasPassed)
	fmt.Println(appointmentInAfternoon)
	fmt.Println(appointmentDescription)
	fmt.Println(anniversaryThisYear)
}

```

---

## Question 21

Question:  
Write a program that computes the net amount of a bank account based on a transaction log. The transaction log is an array in the following format: [D 100 W 200]. D means deposit while W means withdrawal. Suppose the following input is supplied to the program: D 300 D 300 W 200 D 100 Then, the output should be: 500

Hints:

1. Declare the initiate the input in a variable in global scope;
1. Since Go's arrays only take one type, the numbers will be strings and will have to be converted to ints at some point.

Solution:

```golang
package main

import (
	"fmt"
	"strconv"
)

// log declared and initiated in global scope. Note that the array is of fixed
// length with the elements supplied (although you can have zero value elements)
var log = [8]string{"D","300","D","300","W","200","D","100"}

func splitArr(log [8]string) ([]int, []string) {
	// create an int slice to take the quantities converted to ints
	intSlice := make([]int, 0)
	// create a slice to take only the type of transaction
	txSlice := make([]string, 0)
	for i := 0; i < len(log); i++ {
		// if i is even take log[i] and put it into txSlice
		if i % 2 == 0 {
		txSlice = append(txSlice, log[i])
		// if take log[i] and convert it into an int and put it into intSlice
		} else if i % 2 != 0 {
			intStr, _ := strconv.Atoi(log[i])
			intSlice = append(intSlice, intStr)
		}
	}
	return intSlice, txSlice
}

// returns the amount int as a naked return
func calcTotal(quants []int, txs []string) (amount int) {
		for i := 0; i < len(txs); i++ {
			// if the item at the index of txs is "D" add the corresponding index of
			// quants to amount. Else deduct that amount
			if txs[i] == "D" {
				amount += quants[i]
			} else {
				amount -= quants[i]
			}
		}
		return
}

func main() {
	quants, txs := splitArr(log)
	netAmount := calcTotal(quants, txs)
	fmt.Println(netAmount)
}
```

---

## Question 22

Question:  
A website requires the users to input username and password to register. Write a program to check the validity of password input by users. Following are the criteria for checking the password:

At least 1 letter between [a-z]
At least 1 number between [0-9]
At least 1 letter between [A-Z]
At least 1 character from [$#@]
Minimum length of transaction password: 6
Maximum length of transaction password: 12
Your program should accept a sequence of comma separated passwords and will check them according to the above criteria. Passwords that match the criteria are to be printed, each separated by a comma.

Example:  
If the following passwords are given as input to the program: ABd1234@1,a F1#,2w3E\*,2We3345,4Jr4#175 Then, the output of the program should be: ABd1234@1,4Jr4#175

Hints:

1. Use regex for this;
1. A good resource is [Regexr](https://regexr.com/);
1. Go has a regexp package that is perfect for this task.

Solution:

```golang
package main

import (
	"fmt"
	"regexp"
	"strings"
)

// func to turn pwd str into a slice
func slicePwds(myPwds string) []string {
	return strings.Split(myPwds, ",")
}

// func to check each  6 >= pwd <= 12
func howLong(pwd string) (valid bool) {
	valid = len(pwd) >= 6 && len(pwd) <= 12
	return
}

// func to check pwd has 1 char each from [a-z] [0-9] [A-Z] [$#@]
func regTest(pwd string) bool {
	// create regex string. In this case, the regex means: "Match at least one char
	// from this range [start-stop] contained in this group ()"
	 a, _ := regexp.MatchString("([A-Z])\\w+", pwd)
	 b, _ := regexp.MatchString("([a-z])\\w+", pwd)
	 c, _ := regexp.MatchString("([0-9])\\w+", pwd)
	 d, _ := regexp.MatchString("([$#@])\\w+", pwd)
	 return a && b && c && d
}

func main() {
	// create empty slice to take the validated pwds
	validPwds := make([]string, 0)
	myPwds := "ABd1234@1,a F1#,2w3E*,2We3345,4Jr4#175"
	slicedPwds := slicePwds(myPwds)
	// start loop. Add to validPwds any slice that meets the required length AND char
	// combination
	for i:= 0; i < len(slicedPwds); i++ {
		if howLong(slicedPwds[i]) && regTest(slicedPwds[i]) {
			validPwds = append(validPwds, slicedPwds[i])
		}
	}
	// transform slice into a comma-separated slice:
	csOutput := strings.Join(validPwds, ",")
	fmt.Println(csOutput)
}
```

---

## Question 23

Question:  
You are required to write a program to sort in ascending order a slice of structs containing the (name, age, height) fields. In these fields, name is string, age and height are numbers.
The sort criteria is: 1: Sort based on name; 2: Then sort based on age; 3: Then sort by score. The priority is that name > age > score.
To create your structs, take an input as a comma-separated string, split it, create a struct for each set of data, and add it to a slice. Then sort the slice according to the criteria defined above.

Example:  
If the following structs are given as input to the program: "Tom,19,80 Jony,17,23 John,20,90 Jony,17,91 Jony,17,93 Jason,21,85 Jony,17,24";
Then, the output of the program should be: [{Jason 21 85} {John 20 90} {Jony 17 24} {Jony 17 23} {Jony 17 91} {Jony 17 93} {Tom 19 80}]

Solution:

```golang
package main

import (
	"fmt"
	"sort"
	"strconv"
	"strings"
)

// create the struct type
type child struct {
	name string
	age, height int
}

func createSlice(input string) []child {
	// create main slice
	mainSlice := make([]child, 0)
	// split input
	splitInput := strings.Split(input, " ")
	// start loop to split each element in splitInput and add new arr to mainSlice
	for i := 0; i < len(splitInput); i++ {
		// split each element
		childArr := strings.Split(splitInput[i], ",")
		// create 3 vars using each element in the parent element
		childName := childArr[0]
		// remember to convert the num str into ints
		childAge, _ :=  strconv.Atoi(childArr[1])
		childHeight, _ := strconv.Atoi(childArr[2])
		// create the struct using the above vars
		newChild := child{name: childName, age : childAge, height: childHeight}
		// append the new struct to the slice
		mainSlice = append(mainSlice, newChild)
	}
	return mainSlice
}


func main() {
	// supply the input
	input := "Tom,19,80 Jony,17,23 John,20,90 Jony,17,91 Jony,17,93 Jason,21,85 Jony,17,24"
	// split the input into a slice of structs
	getSlice := createSlice(input)
	// sort the slice in place - note that this takes a "callback function" with 2
	// params to access the individual fields in each struct.
	sort.Slice(getSlice, func(i, j int) bool {
		return getSlice[i].name < getSlice[j].name
	})
	fmt.Println(getSlice)
}

```

---

## Question 24

Question:  
Define a generator which can iterate the numbers, which are divisible by 7, between a given range 0 and n.

Hints: at this stage it is premature to tackle it since the best solution probably requires channels that haven't been covered yet. Solve this later.

```golang

```

---

## Question 25

Question:  
A robot moves in a plane starting from the original point (0,0). The robot can move toward UP, DOWN, LEFT and RIGHT with a given steps. The trace of robot movement is shown as the following: UP 5 DOWN 3 LEFT 3 RIGHT 2.­ The numbers after the direction are steps. Write a program to compute the distance from current position after a sequence of movement and original point. If the distance is a float, then just print the nearest integer.

Example:  
If the following directions are given as input to the program: UP 5 DOWN 3 LEFT 3 RIGHT 2 Then, the output of the program should be: 2

Hints:

1. Input data is to be assumed to be supplied in this format: UP 5,DOWN 3,LEFT 3,RIGHT;
1. To find the distance between (x1, y1) and (x2, y2) Use this formula: d= √((x2−x1)**2+(y2−y1)**2);
1. Assume that the starting co-ordinates are 0,0;
1. Don't forget to round it to the nearest integer.

Solution:

```golang
package main

import (
	"fmt"
	"math"
	"strconv"
	"strings"
)

// func to transform the input into an array of arrays
func makeMyData(input string) [][]string {
	// create outer slice
	outer := make([][]string, 0)
	splInput := strings.Split(input, ",")
	for i := 0; i < len(splInput); i++ {
		splitElem := strings.Split(splInput[i], " ")
		outer = append(outer, splitElem)
	}
	return outer
}

// func to get the stopping point of the robot as a slice of cartesian co-ordinates
func getStop(data [][]string) []int {
	// create slice of length 2 to contain the co-ordinates at stopping point
	posTwo := make([]int, 2)
	for i:= 0; i < len(data); i++ {
		n, _ := strconv.Atoi(data[i][1])
		if data[i][0] == "UP" {
			posTwo[0] += n
		} else if data[i][0] == "DOWN" {
			posTwo[0] -= n
		}  else if data[i][0] == "LEFT" {
			posTwo[1] -= n
		} else if data[i][0] == "RIGHT" {
			posTwo[1] += n
		}
	}
	return posTwo
}

// func to calcualte the distance from posTwo to posOne
func computeDistance(posTwo []int) (distance int) {
// √((x2−x1)**2+(y2−y1)**2)
// x1,y1 are the starting coordinates, assume that they are 0,0
	x1, y1 := float64(0), float64(0)
	x2, y2 := float64(posTwo[0]), float64(posTwo[1])
	aEq, bEq  := (x2-x1)*(x2-x1), (y2-y1)*(y2-y1)
	distance = int(math.Round(math.Sqrt(aEq + bEq)))
	return
}

func main() {
	input := "UP 5,DOWN 3,LEFT 3,RIGHT 2"
	// split input into an array of arrays containing directions
	createData := makeMyData(input)
	// get the co-ordinates of the stopping point
	posTwo := getStop(createData)
	// submit both sets of co-ordinates to calculate distance
	distance := computeDistance(posTwo)
	fmt.Println(distance)
}

```

---

## Question 25

Question:  
Write a program to compute the frequency of the words from the input. The output should be sorted by the key alphanumerically in ascending order.

Example:  
If the input is:
"New to programming or trying to choose between OOP and functional programming? 1 new language to try programming first is Golang right now. Golang does both."
The output should be:
{"1":1,"and":1,"between":1,"both.":1,"choose":1,"does":1,"first":1,"functional":1,"golang":2,"is":1,"language":1,"new":2,"now.":1,"oop":1,"or":1,"programming":2,"programming?":1,"right":1,"to":3,"try":1,"trying":1}

Hints:

1. If you wish, you may take the user's input for this exercise;
1. Sort in ascending order;
1. Output as an JSON object.

Solution:

```golang
package main

import (
	"encoding/json"
	"fmt"
	"sort"
	"strings"
)

// func to take supplied arr and return a map containing each individual word as the
// key and the number of iterations of that word as the value
func genMap(input []string) map[string]int {
	myMap := make(map[string]int)
	// convert each word into lowercase
	loweredSlice := make([]string, 0)
	for i:= 0; i < len(input); i++ {
		loweredSlice = append(loweredSlice, strings.ToLower(input[i]))
	}
	// create a new slice from loweredSlice to sort and to reduce to just every
	//individual word
	sortedSlice := loweredSlice
	sort.Strings(sortedSlice)
	// sort and reduce to each individual word
	sort.Slice(sortedSlice, func(i, j int) bool {
		return sortedSlice[i] < sortedSlice[j]
	})
	fmt.Println(loweredSlice)
	fmt.Println(len(loweredSlice))
	// start looping through input and loweredSlice and count each iteration and assign
	// them to the map
	for i := 0; i < len(sortedSlice); i++ {
		num := 0
		char := sortedSlice[i]
		for j := 0; j < len(input); j++ {
			if char == loweredSlice[j] {
				num += 1
			}
		}
		myMap[char] = num
	}
	return myMap
}

// func to convert map to JSON
func getJSON(myMap map[string]int) string {
	myJSON, _ := json.Marshal(myMap)
	return string(myJSON)
}

func main() {
	input := "New to programming or trying to choose between OOP and functional programming? 1 new language to try programming first is Golang right now. Golang does both."
	inArr := strings.Split(input, " ")
	myMap := genMap(inArr)
	jsonStr := getJSON(myMap)
	fmt.Println(jsonStr)
}

```

---

## Question 26

Question:  
Write a function that can calculate the square value of a number. The program should take the input from the user and there should be error correction to ensure that only number inputs are processed.

Hints:

1. Allow for the user to input multiple words;
1. But only retain and test the first one;
1. If that first word is an int, square it, otherwise tell the user that his input is invalid;
1. use 64 bit max ints for this exercise. No need to use the math/big package.

Solution:

```golang
package main

import (
	"bufio"
	"fmt"
	"os"
	"strconv"
	"strings"
)

// takes the user's input.
// Returns the int and true if the input is valid.
// Returns 0 and false if the input is invalid.
func takeInput()  (int, bool){
	fmt.Println("Input an integer to square. The code will only accept integers:\t")
	// create reader and take user input
	reader := bufio.NewReader(os.Stdin)
	input, _ := reader.ReadString('\n')
	input = strings.TrimSpace(input)
	// start error checking.
	// first split string by spaces in case there is more than one word or number.
	inputArr := strings.Split(input, " ")
	// Retain only the first element in the new array.
	elem := inputArr[0]
	// test elem to check whether it is an int or not
	_, err := strconv.ParseInt(elem, 10, 64)
	// if err is nil, return the elem and true
	if err == nil {
		elem, _ := strconv.Atoi(elem);
		return elem, true
		// else return 0 and false
	} else {
		return 0, false
	}
}

func squareMyNum(num int) int {
	return num * num
}

func main() {
	input, valid := takeInput()
	if valid {
		num := squareMyNum(input)
		fmt.Printf("The square of your input %v\n", num)
	} else {
		fmt.Println("Your input is invalid")
	}
}
```

---

## Question 27

Question:  
Define a function that can compute and return the sum of two integers. But adding the two numbers is only your secondary objective. Your primary objective is to add an error return to a function testing that the user's input is in fact an integer.

Hints:

1. For a successful test, return nil without creating a new error message;
1. Otherwise create a custome error message;
1. To create a new error message use: error := errors.New("new custom error message").

Solution:

```golang
package main

import (
	"bufio"
	"errors"
	"fmt"
	"log"
	"os"
	"strconv"
	"strings"
)

// takes the user's input. Returns the int if the input is valid else stops the code.
func takeInput()  int {
	fmt.Println("Input an integer to square. The code will only accept integers:\t")
	// create reader and take user input
	reader := bufio.NewReader(os.Stdin)
	input, _ := reader.ReadString('\n')
	input = strings.TrimSpace(input)
	// test the input
	checkedInput, err := validateInput(input)
	// check if the err == nil
	if err != nil {
		// if err != nil, use log.Fatal to print err and stop the program
		log.Fatal(err)
	}
	return checkedInput
}

// func to validate input. Returns int and nil if input is valid, returns 0 and a
// custom error message otherwise.
func validateInput(input string) (int, error) {
	// start error checking.
	// first split string by spaces in case there is more than one word or number.
	inputArr := strings.Split(input, " ")
	// Retain only the first element in the new array.
	elem := inputArr[0]
	// test elem to check whether it is an int or not
	_, err := strconv.ParseInt(elem, 10, 64)
	// if err is nil, return the elem and an error message of "nil"
	if err == nil {
		elem, _ := strconv.Atoi(elem);
		// return both the int and nil for the error
		return elem, nil
		// else return 0 and a custom error message
	} else {
		// create a non-nil error message and return it
		error := errors.New("invalid input! Exiting code now.")
		return 0, error
	}
}

func addMyNum(a, b int) int {
	return a + b
}

func main() {
	numOne := takeInput()
	numTwo := takeInput()
	sum := addMyNum(numOne, numTwo)
	fmt.Println(sum)
}
```

---

## Question 28

Question:
Define a function that can receive two integers (type int) in string form and compute their sum and then print it out.

Hints:

1. Add error checking to allow for the possibility that the inputs are not integers in the type of a string
1. Add functionality to check if the number is a float and if so convert it to an integer
1. In case of input data being supplied to the question, it should be requested and taken from the user.

Solution:

```golang
package main

import (
	"bufio"
	"errors"
	"fmt"
	"log"
	"math"
	"os"
	"strconv"
	"strings"
)

// func to get user input
func userInput() (a, b int)  {
	fmt.Println("Please input an int to add with another. Anything beside a number will be rejected. Floats will be rounded up and converted to ints:\t")
	// create reader
	reader := bufio.NewReader(os.Stdin)
	aStr, _ := reader.ReadString('\n')
	// trim whitespace
	aStr = strings.TrimSpace(aStr)
	// validate aStr
	validatedAStr, err := validate(aStr)
	// if no error, set aStr to a otherwise close the prog with the error msg
	if (err == nil) {
		a = validatedAStr
	} else {
		log.Fatal(err)
	}
	fmt.Println("Please input a second int:\t")
	bStr, _ := reader.ReadString('\n')
	// trim whitespace
	bStr = strings.TrimSpace(bStr)
	// validate bStr
	validatedBStr, err := validate(bStr)
	// if no error, set bStr to b otherwise close the prog with the error msg
	if (err == nil) {
		b = validatedBStr
	} else {
		log.Fatal(err)
	}
	return
}

// func for error checking and check whether string is an int/float. Return
// the number turned into an int and nil if valid, or 0 and error if invalid
func validate(aStr string) (int, error) {
	// start error checking.
	// first split string by spaces in case there is more than one word or number.
	strArr := strings.Split(aStr, " ")
	// get first element and discrad rest of arr
	elem := strArr[0]
	// check if elem is float:
	elemFl, err := strconv.ParseFloat(elem, 64)
	if err == nil {
		// if no error message, elem IS a float, round it, and return it as an int
		elemFl := math.Round(elemFl)
		return int(elemFl), nil
	} else {
		// if elem is not a float, check to see if it is an int, if so return it
		elemInt, err := strconv.Atoi(elem)
		if err == nil {
			return elemInt, nil
		}
	}
	// if we get here, assume that the input is neither an int nor a float but is
	// invalid. Return 0 and an new error message
	return 0, errors.New("Invalid input!")
}

// func to add user input - redundant but, hey, it's a func
func addMe(a, b int) int {
	return a + b
}

func main() {
	a, b := userInput()
	sum := addMe(a, b)
	fmt.Println(sum)
}
```

---

## Question 29

Question:  
Define a function that can accept two strings as input and concatenate them and then print it in console.

Hints:

1. Take the strings from the user.

Solution:

```golang
package main

import (
	"bufio"
	"fmt"
	"os"
	"strings"
)

// func to take user input as a string. Return string. No error checking necessary.
func userInput() (userStr string) {
	// create reader
	reader := bufio.NewReader(os.Stdin)
	fmt.Println("Please input a string:\t")
	// take user input
	userStr, _ = reader.ReadString('\n')
	// trim whitespace
	userStr = strings.TrimSpace(userStr)
	return
}

// func to concatenate two strings. Returns the concatenated string
func conc(strA, strB string) (concedStr string) {
	concedStr = strA + " " + strB
	return
}

func main() {
	strA := userInput()
	strB := userInput()
	joinedStr := conc(strA, strB)
	fmt.Println(joinedStr)
}

```

---

## Question 30

Question:  
Define a function that can accept two strings as input and print out the longest string. If two strings have the same length, then the function should print both strings line by line.

Example:

1. "hey" "world" returns "world";
1. "hello" "world" returns "hello" "world".

Hints:

1. Take input from user;
1. The input should be taken at one go;
1. But test the input to make sure that it contains more than one word;
1. If it only contains one word, prompt the user for another;
1. If more than two words are submitted, discard everything after the second word;

Solution:

```golang
package main

import (
	"bufio"
	"fmt"
	"os"
	"strings"
)

// func to take user input. Check that two strings have been inputted.
//If only 1 string is inputted, prompt for another one. If more than 2 are submitted
// discard the extra ones. Returns two strings.
func userInput() (strA, strB string) {
	// create reader
	reader := bufio.NewReader(os.Stdin)
	fmt.Println("Please input a string consisting of two words. Fewer than that will require you to input another one. More than that will be discarded:\t")
	strInput, _ := reader.ReadString('\n')
	// trim whitespace
	strInput = strings.TrimSpace(strInput)

	strArr := strings.Split(strInput, " ")
	// if arr contains 2 or more words, set strA and StrB to first 2 elems of the arr
	if len(strArr) < 2 {
		strA = strArr[0]
		strB = getMissingWord()
	} else if (len(strArr) >= 2) {
		strA = strArr[0]
		strB = strArr[1]
	}
	return
}

// get the missing word if original input contains only one word
func getMissingWord() (strB string) {
	// create reader
	reader := bufio.NewReader(os.Stdin)
	fmt.Println("Your original input is missing a word. Please input another one. If you input more than one word, the extra ones will be discraded:\t")
	strInput, _ := reader.ReadString('\n')
	// trim whitespace
	strInput = strings.TrimSpace(strInput)
	strArr := strings.Split(strInput, " ")
	strB = strArr[0]
	return
}

// func that takes both strings and prints out the longest string, or both strings line
// by line if both strings are of equal length.
func printLongestStr(strA, strB string) {
	if (len(strA) > len(strB)) {
		fmt.Println(strA)
	} else if (len(strA) < len(strB)) {
		fmt.Println(strB)
	} else if (len(strA) == len(strB)) {
		fmt.Printf("%v\n%v\n", strA, strB)
	}
}

func main() {
	stringA, stringB := userInput()
	printLongestStr(stringA, stringB)
}

```

---

## Question 31

Question:

You have been tasked with creating a log library to assist with managing your organization's logs. This library will allow users to identify which application emitted a given log, to fix corrupted logs, and to determine if a given log line is within a certain character limit.

1. Identify which application emitted a log
   Logs come from multiple applications that each use their own proprietary log format. The application emitting a log must be identified before it can be stored in a log aggregation system.

Implement the Application function that takes a log line and returns the application that emitted the log line.

To identify which application emitted a given log line, search the log line for a specific character as specified by the following table:

Application: recommendation Character: ❗ Unicode Code Point: U+2757
Application: search Character: 🔍 Unicode Code Point: U+1F50D
Application: weather Character: ☀ Unicode Code Point: U+2600

If a log line does not contain one of the characters from the above table, return default to the caller. If a log line contains more than one character in the above table, return the application corresponding to the first character found in the log line starting from left to right.

2. Fix corrupted logs
   Due to a rare but persistent bug in the logging infrastructure, certain characters in logs can become corrupted. After spending time identifying the corrupted characters and their original value, you decide to update the log library to assist in fixing corrupted logs.

Implement the Replace function that takes a log line, a corrupted character, and the original value and returns a modified log line that has all occurrences of the corrupted character replaced with the original value.

log := "please replace '👎' with '👍'"
Replace(log, '👎', '👍') // => please replace '👍' with '👍'"

3. Determine if a log can be displayed
   Systems responsible for displaying logs have a limit on the number of characters that can be displayed per log line. As such, users are asking for this library to include a helper function to determine whether or not a log line is within a specific character limit.

Implement the WithinLimit function that takes a log line and character limit and returns whether or not the log line is within the character limit.

Hints:

1. For part 1, if there is more than rune in the string, return only the output corresponding to the FIRST rune;
1. Runes may consist of more than one char so to get an accurate reading of the length of the string supplied as an argument in part 3, turn the string into a rune array.

Source: [History for go/exercises/concept/logs-logs-logs
](https://exercism.org/tracks/go/exercises/logs-logs-logs)

Solution:

```golang
package main

import (
	"fmt"
	"strings"
)

func Application(log string) string {
	logSlice := make([]string, 0)
	for _, char := range log {
		// compare char with each possible rune, and append the desired output if it
		// matches
		if (char == '❗') {
			logSlice = append(logSlice, "recommendation")
			} else if (char == '🔍') {
				logSlice = append(logSlice, "search")
				} else if (char == '☀') {
					logSlice = append(logSlice, "weather")
					}
	}
	// if there is more than one output (if more than one rune is found, return only
	// the first one)
	if len(logSlice) > 0 {
		return logSlice[0]
	}
	// otherwise return "default"
	return "default"
}

// Replace replaces all occurrences of old with new, returning the modified log
// to the caller.
func Replace(log string, oldRune, newRune rune) string {
	// split the string into an array
	stringSlice := strings.Split(log, " ")
	// set up a slice to contain indices
	idxSlice := make([]int, 0)
	// stringify both the runes
	oldRuneStr := fmt.Sprintf("%c", oldRune)
	newRuneStr := fmt.Sprintf("%c", newRune)
	// iterate through array comparing each char with the stringified oldRune
	for index, char := range stringSlice {
		if (char == oldRuneStr) {
			// if there is a match, append the index of the char to the idxSlice
			idxSlice = append(idxSlice, index)
		}
	}
	// using the idxSlice iterate through stringSlice and set elem in stringSlice
	// corresponding to the index stored in idxSlice to the stringified newRune
	for i:= 0; i < len(idxSlice); i++ {
		stringSlice[idxSlice[i]] = newRuneStr
	}
	return strings.Join(stringSlice, " ")
}

// WithinLimit determines whether or not the number of characters in log is
// within the limit.
func WithinLimit(log string, limit int) bool {
	// set log to a rune arr
	r := []rune(log)
	// return length of rune array <= limit
	return len(r) <= limit
}

func main() {
	a := Application("❗ recommended search product 🔍") 	// => recommendation
	fmt.Println(a)
	log := "please replace '👎' with '👍'"
	newLog := Replace(log, '👎', '👍') // => please replace '👍' with '👍'"
	fmt.Println(newLog)
	secondLog := "❗ recommended product ❗"
	newSecondLog := Replace(secondLog, '❗','?')
	fmt.Println(newSecondLog)
	limit := WithinLimit("hello❗", 6) // => true
	fmt.Println(limit)

}

```

---

## Question 32

Question:  
Define a function that can accept an integer number as input and print the "It is an even number" if the number is even, otherwise print "It is an odd number".

Hints:

1. Use % operator to check if a number is even or odd;
1. Take the input from the user;
1. Reject all input that does not resolve to an integer, but if the input is the string of an integer or float, turn it into an integer and process it accordingly;
1. If the input cannot be resolved to an integer, keep prompting the user to supply a valid input.

Solution:

```golang
package main

import (
	"bufio"
	"fmt"
	"math"
	"os"
	"strconv"
	"strings"
)

//func to take user input and check if it is int/float/string
// if it is an int, return the int and true
// if it is a float, round it up and return true
// if it is a string, return 0 and false
func userInput() (myInt int, myResult bool) {
	// create reader
	reader := bufio.NewReader(os.Stdin)
	fmt.Println("Please enter an integer. Only integers will be accepted for this operation:\t")
	userInput, _ := reader.ReadString('\n')
	userInput = strings.TrimSpace(userInput)
	// split string into array and take the first elem
	firstElem := strings.Split(userInput, " ")[0]
	// check to see if that elem is a float
	testFltElem, err := strconv.ParseFloat(firstElem, 64)
	if (err == nil) {
		// if it is a float, rount it up, convert to int and set it to myInt
		myInt = int(math.Round(testFltElem))
		// set result to true
		myResult = true
	}
	// if not a float, test to see if an int
	testIntElem, err := strconv.Atoi(firstElem)
	if (err == nil) {
		if (err == nil) {
			// if an int, set it to myInt
			myInt = testIntElem
			// set result to true
			myResult = true
			} else {
				// otherwise set myInt to 0 and myResult to false
				myInt = 0
				myResult = false
			}
		}
		return
	}

func testEven(a int) (result string) {
	if (a % 2 == 0) {
		result = "It is an even number"
	} else {
		result = "It is an an odd number"
	}
	return
}

func main() {
	a, result := userInput()
	// if the result is true
	if (result) {
		// test whether the returned int is even or odd
		ans := testEven(a)
		fmt.Println(ans)
		// otherwise inform the user that his input is invalid
	} else {
		fmt.Println("Your input is invalid!")
	}

}
```

---

## Question 33

Question:  
Define a function which can print a JSON object where the keys are 1... n (supplied) and the values are squares of n. For example, if createObj(3), then the created object would be: { 1: 1, 2: 4, 3: 9, 4: 16 }. The supplied n should be an integer due to the need to ensure that the keys are in a predictably ascending range.

Hints:

1. First create the object as a map then encode it as a JSON object;
1. Assume that the input can be of any type. Add functionality to check for this and reject all invalid types, but if the input is the string of an integer or float, turn it into an integer and process it accordingly;
1. In case of input data being supplied to the question, it should be assumed to be a prompt input from a webpage.

Solution:

```golang
package main

import (
	"bufio"
	"encoding/json"
	"fmt"
	"math"
	"os"
	"strconv"
	"strings"
)

// take userInput. Return an integer
func userInput() (num int) {
	reader := bufio.NewReader(os.Stdin)
	flag := false
	var result bool
	// this is how to do a while loop in Go - use For and a bool value
	for !flag {
		fmt.Println("Please input an integer. Only the first integer will be accepted. Floats will be rounded up. Text will be rejected:\t")
		takeInput, _ := reader.ReadString('\n')
		takeInput = strings.TrimSpace(takeInput)
		// submit the input to the validator func. Returns the num and a bool to set to
		// the flag
		num, result = testInput(takeInput)
		flag = result
	}
	return
}

// the validator func. Tests input string. If the string is a float, it rounds it
// up and returns it as an int, with true as the result. Likewise if it is an int.
// If it is a string, it returns 0 and false.
func testInput(input string) (num int, result bool)  {
	// Take the first element of the input when split into an array
	inElem := strings.Split(input, " ")[0]
	// test to find out if it we have a float
	inElemFlt, err := strconv.ParseFloat(inElem, 64)
	if (err == nil) {
		num = int(math.Round(inElemFlt))
		fmt.Println(num)
		result = true
		// if not check if it is an int
	} else if (err != nil) {
		inElemInt, error := strconv.Atoi(inElem)
		if (error == nil) {
			num = inElemInt
			result = true
		}
		// if not, return 0 and false
	} else  {
		num = 0
		result = false
	}
	return
}

// func that takes an int and returns an JSON object as a string
func createObject(num int) (obJSON string) {
	// create a map of [int]int
	nuMap := make(map[int]int, 0)
	// start a loop to run through the sequence of 0... num
	for i:= 1; i <= num; i++ {
		// for every num, the key:value pair is num:num*num
		nuMap[i] = i * i
	}
	// convert map to JSON byte array
	bArr, _ := json.Marshal(nuMap)
	// convert byte array to string. Remember that the stringified
	// JSON object will not be printed with the keys sorted
	// by the fmt package.
	obJSON = string(bArr)
	return
}

func main() {
	num := userInput()
	myJSONObject := createObject(num)
	fmt.Println(myJSONObject)

}
```

---

## Question 34

Question:  
Define a function which can print out a map where the keys are numbers between 1 and 20 (both included) and the values are square of keys.

Hints:

1. No input or error checking;
1. any functions called outside main should take no arguments. Use global scope parameters.

Solution:

```golang
package main

import "fmt"

var num int = 20

// this func creates and prints out the map
func genMap() {
	myMap := make(map[int]int,20)
	for i:= 1; i <= num; i++ {
		myMap[i] = i * i
	}
	fmt.Println(myMap)
}

func main() {
	genMap()
}
```

---

## Question 35

Question:  
Define a function which can generate an object where the keys are numbers between 1 and 20 (both included) and the values are the square of the keys. Then print out the values and print them out in ascending order.

Hints:

1. No input or error checking;
1. any functions called outside main should take no arguments. Use global scope parameters;
1. You can export the printing of the values to another function;
1. To print out the values in ascending order, you have to sort them in a different data structure.

Solution:

```golang
package main

import (
	"fmt"
	"sort"
)

var num int = 20

func genMap() {
	// create map
	myMap := make(map[int]int, 20)
	// create slice to take the values of myMap and sort them
	mySlice := make([]int, len(myMap))
	// create the map and also add each value to mySlice
	for i := 1; i <= num; i++ {
		myMap[i] = i * i
		mySlice = append(mySlice, i*i)
	}
	// sort mySlice
	sortedSlice := sort.IntSlice(mySlice)
	// iterate through sortedSlice and print out the values
	for _, values := range sortedSlice {
		fmt.Println(values)
	}
}

func main() {
	genMap()
}

```

---

## Question 36

Question:  
Define a function which can generate an object where the keys are numbers between 1 and 20 (both included) and the values are the square of the keys. Then print out the keys and print them out in ascending order.

Hints:

1. No input or error checking;
1. any functions called outside main should take no arguments. Use global scope parameters;
1. You can export the printing of the values to another function;
1. To print out the keys in ascending order, you have to sort them in a different data structure.

Solution:

```golang
package main

import (
	"fmt"
	"sort"
)

var num int = 20

func genMap() {
	// create map
	myMap := make(map[int]int, 20)
	// create slice to take the values of myMap and sort them
	mySlice := make([]int, len(myMap))
	// create the map and also add each key to mySlice
	for i := 1; i <= num; i++ {
		myMap[i] = i * i
		mySlice = append(mySlice, i)
	}
	// sort mySlice
	sortedSlice := sort.IntSlice(mySlice)
	// iterate through sortedSlice and print out the keys of the map
	// keep in mind that the keys of the map are the values of sortedSlice
	for _, value := range sortedSlice {
		fmt.Println(value)
	}
}

func main() {
	genMap()
}
```

---

## Question 37

Question:  
Define a function which can generate a slice where the values are square of numbers between 1 and 20 (both included). Then the function needs to print an slice with the first 5 elements in the slice. You can export the slice to another function and print it there.

Hints:

1. No input or error checking;
1. Any functions called outside main should take no arguments. Use global scope parameters;
1. You can export the printing of the values to another function.

Solution:

```golang
import "fmt"

var num int = 20

// the slice generation and output func
func genSlc() {
	mySlc := make([]int, 0)
	for i:= 1; i <= num; i++ {
		mySlc = append(mySlc, i*i)
	}
	fmt.Println(mySlc[0:5])
}

func main() {
	genSlc()
}
```

---

## Question 37

Question:
Define a function which can generate an slice where the values are square of numbers between 1 and 20 (both included). Then the function needs to print an slice with the last 5 elements in the slice. You can export the slice to another function and print it there.

Hints:

1. No input or error checking;
1. Any functions called outside main should take no arguments. Use global scope parameters;
1. You can export the printing of the values to another function;

Solution:

```golang
package main

import "fmt"

var num int = 20

// the slice generation and output func
func genSlc() {
	mySlc := make([]int, 0)
	for i:= 1; i <= num; i++ {
		mySlc = append(mySlc, i*i)
	}
	// printing the last 5 elements of the array
	fmt.Println(mySlc[num-5:])
}


func main() {
	genSlc()
}
```

---

## Question 38

Question:
Define a function which can generate an slice where the values are square of numbers between 1 and 20 (both included). Then the function needs to print an slice with all values except the first 5 elements in the list. You can export the slice to another function and print it there.

Hints:

1. No input or error checking;
1. Any functions called outside main should take no arguments. Use global scope parameters;
1. You can export the printing of the values to another function.

Solution:

```golang
package main

import "fmt"

var num int = 20

func genSlc() {
	mySlc := make([]int, 0)
	for i := 1; i <= num; i++ {
		mySlc = append(mySlc, i * i)
	}
	fmt.Println(mySlc[num-5:])
}

func main() {
	genSlc()
}

```

---

## Question 39

Question:  
Write a program to create a slice dynamically [1,2,3,4,5,6,7,8,9,10] and then print the first half values in one line and the last half values in one line.

Hints:

1. Any functions called outside main should take no arguments. Use global scope parameters;
1. You can export the printing of the values to another function.

Solution:

```golang
package main

import "fmt"

func genSlc() (mySlc []int){
	for i:= 1; i <= 10; i++ {
		mySlc = append(mySlc, i)
	}
	return

}

func printSlc(slc []int) {
	n := len(slc) / 2
	fmt.Println(slc[:n])
	fmt.Println(slc[n:])
}

func main() {
	getSlc := genSlc()
	printSlc(getSlc)
}
```

---

## Question 40

Question:
Write a program to generate and print another array whose values are even numbers in the given array [1,2,3,4,5,6,7,8,9,10] => [2,3,6,8,10]. If you like add functionality to do the same if the numbers are supplied as a comma separated string "1,2,3,4,5,6,7,8,9,10". In this case,the output should be a comma separated string.

Hints:

1. Use a slice for the output array as it is easier to append the even n to an empty slice than to replace values in an array.

Solution:

```golang
package main

import (
	"fmt"
	"strconv"
	"strings"
)

var strNum string = "1,2,3,4,5,6,7,8,9,10"

// func to do all the work
func processStr() {
	// splits the string into an array
	strArr := strings.Split(strNum, ",")
	// create an n half the len of strArr
	n := len(strArr) / 2
	// create new slice of size half len(strArr)
	evenArr := make([]string, 0, n)
	// start loop to populate evenArr
	for i := 0; i < len(strArr); i++ {
		strToInt, _ := strconv.Atoi(strArr[i])
		if strToInt % 2 == 0 {
			evenArr = append(evenArr, strArr[i])
		}
	}
	csv := strings.Join(evenArr, ",")
	fmt.Println(csv)
}

func main() {
	processStr()
}

```

---

## Question 41

Question:  
Write a program to swap two variables.

Hints:

1. In many languages, you will need to create a temporary variable. Not so in Go;

Solution:

```golang
package main

import "fmt"

func main() {
	x := 10
	y := 20
	x, y = y, x
	fmt.Println(x, y)
}
```

---

## Question 42

Question:  
Write a program which accepts a string as input and prints "Yes" if the string is any permutation of "yes" (YES, YeS, yEs, yes, yES, YEs etc.), otherwise print "No".

Hints:

1. For this exercise get the input from the user.

Solution:

```golang
package main

import (
	"bufio"
	"fmt"
	"os"
	"strings"
)

// takes user input
func userInput() (inp string) {
	// create reader
	reader := bufio.NewReader(os.Stdin)
	fmt.Printf("Please enter a string. If it contains any permutation of \"yes\", the code will let you know, otherwise it will print \"no\":\t")
	// reader takes input
	inp, _ = reader.ReadString('\n')
	// trims whitespace
	inp = strings.TrimSpace(inp)
	return
}

// test input for any permutation of "yes", returns bool
func testInput(inp string) (test bool) {
	// reduces entire string to lowercase
	inp = strings.ToLower(inp)
	if inp == "yes" {
		test = true
	} else {
		test = false
	}
	return
}

func main() {
	// get user input
	inp := userInput()
	// test user input
	result := testInput(inp)
	// use switch to print out resul
	switch result {
	case true:
		fmt.Println("yes")
	case false:
		fmt.Println("no")
	}
}
```

---

## Question 43

Question:  
Write a program which can filter even numbers in an array by using filter function. The array is: [1,2,3,4,5,6,7,8,9,10]. For this exercise, the numbers should be type of integer number

Hints:

1. Unlike Javascript, Go does not have a filter function, but there's nothing stopping you from writing your own;
1. Since Go is strongly typed, the same function cannot filter arrays or slices of different types. For now assume that the array to be filtered consists of int elements.

Solution:

```golang
package main

import "fmt"

// the filter func. It filters int arrays of size 10 and returns a slice of type int
func filterInt(intArr [10]int) (filteredArr []int) {
	for _, v := range intArr {
		if v % 2 == 0 {
			filteredArr = append(filteredArr, v)
		}
	}
	return
}

func main() {
	myArr := [10]int{1,2,3,4,5,6,7,8,9,10}
	filteredArr := filterInt(myArr)
	fmt.Println(filteredArr)
}
```

---

## Question 44

Question:  
Write a program which can map through an array to return a slice whose elements are squares of elements in that array. For this exercise, the array should be [1,2,3,4,5,6,7,8,9,10] of type int.

Hints:

1. Unlike Javascript, Go does not have a map function, but there's nothing stopping you from writing your own;
1. Since Go is strongly typed, the same function cannot map arrays or slices of different types. For now assume that the array to be mapped consists of int elements.

Solution:

```golang
package main

import "fmt"

// the map func. It maps int arrays of size 10 and returns a slice of type int
func mapArr(myArr [10]int) (mappedSlc []int) {
	for i := 0; i < len(myArr); i++ {
		mappedSlc = append(mappedSlc, myArr[i] * myArr[i])
	}
	return
}


func main() {
	myArr := [10]int{1,2,3,4,5,6,7,8,9,10}
	mappedArr := mapArr(myArr)
	fmt.Println(mappedArr)
}

```

---

## Question 45

Question:  
Write a program which can filter and map to return a slice whose elements are squares of even numbers in [1,2,3,4,5,6,7,8,9,10]. For this exercise, the array should consist of types of integer numbers. For this exercise, the array should be [10]int{1,2,3,4,5,6,7,8,9,10}.

Example:
Given an array of: [1,2,3,4,5,6,7,8,9,10]
Return a slice of: [4 16 36 64 100]

Hints:

1. Unlike Javascript, Go has neither a map nor a filter function, but there's nothing stopping you from writing your own;
1. Since Go is strongly typed, the same function cannot map/filter arrays or slices of different types. For now assume that the array to be mapped consists of int elements;
1. There are two approaches to this problem - you can either write two separate functions to do the work of filtering or mapping, or you can combine both functions into one;
1. This solution combines both functions into one.

Solution:

```golang
package main

import "fmt"

// func to first filter and then map an arr of type int and then returns a slice of
// ints that have been filtered by even numbers and then mapped as squares
func filterAndMap(myArr [10]int) (mySlc []int) {
	for i := 0; i < len(myArr); i++ {
		if myArr[i] % 2 == 0 {
			mySlc = append(mySlc, myArr[i] * myArr[i])
		}
	}
	return
}


func main() {
	myArr := [10]int{1,2,3,4,5,6,7,8,9,10}
	processArr := filterAndMap(myArr)
	fmt.Println(processArr)
}
```

---

## Question 46

Question:
Write a program that can generate a slice containing integers between 1... and n and then write a filter function to filter that slice to return a slice whose elements are the even numbers in the original slice.

Example:
Given an n of 20, return a slice of: [2,4,6,8,10,12,14,16,18,20]

Hints:

1. Take the n from the user and add error checking to ensure that the input is an int;
1. If it is a float, round it up and convert it to an int;
1. If it neither an int, nor a float, keep prodding the user to submit a valid int.

Solution:

```golang
package main

import (
	"bufio"
	"fmt"
	"math"
	"os"
	"strconv"
	"strings"
)

// func to take user input
func userInput() (n int) {
	reader := bufio.NewReader(os.Stdin)
	// create a bool to use as a flag for a while loop
	flag := false
	for !flag {
		fmt.Print("Please input an integer n to populate a slice from 1... n. Floats will be rounded and converted to an int. Any other input will be discarded and this prompt will loop until you submit a valid input:\t")
		inp, _ := reader.ReadString('\n')
		inp = strings.TrimSpace(inp)
		n, flag = testInput(inp)
	}
	return
}

// func to validate user input. Accepts the user input as an arg, returns bool
func testInput(userStr string) (n int, flag bool) {
	firstElem := strings.Split(userStr, " ")[0]
	nFlt, err := strconv.ParseFloat(firstElem, 64)
	if (err == nil) {
		n = int(math.Round(nFlt))
		flag = true
		return
	}
	nInt, err := strconv.Atoi(firstElem)
	if (err == nil) {
		n = nInt
		flag = true
		return
	}
	n = 0
	flag = false
	return
}

// func to create slice. Accepts int n as an arg, returns a slice of ints from 1... n
func genSlc(n int) (mySlc []int) {
	for i := 1; i <= n; i++ {
		mySlc = append(mySlc, i)
	}
	return
}

// func to filter slice. Accepts []int as an arg, returns slice filtered by evens
func filterSlc(mySlc []int) (filtSlc []int) {
	for i := 0; i < len(mySlc); i++ {
		if mySlc[i] % 2 == 0 {
			filtSlc = append(filtSlc, mySlc[i])
		}
	}
	return
}

func main() {
	n := userInput()
	nSlc := genSlc(n)
	filSlc := filterSlc(nSlc)
	fmt.Println(filSlc)
}

```

---

## Question 47

Question:  
Write a program that has a map function to create an array whose elements are the squares of the numbers between 1 and 20 (both included).

Hints:

1. For this exercise, create an array not a slice;
1. Replace each individual zero value element with the required values.

Solution:

```golang
package main

import "fmt"

// func to generate array. Takes no arguments, returns nothing.
func genArr()  {
	// create array
	var myArr [20]int
	// start the loop to replace each zero value with the required square of n
	for i := 0; i < len(myArr); i ++ {
		// square i + 1 to ensure that first elem is 1^2 and last elem is 20^2
		myArr[i] = (i + 1) * (i + 1)
	}
	// print array
	fmt.Println(myArr)
}

func main() {
	genArr()
}

```

---

## Question 48

Question:  
Create a new type called vehicle the underlying type of which is a struct. Vehicle should have two fields, one called doors int and color string. Then create two more types of the same underlying type of struct. These types should be truck struct & sedan struct. Embed the “vehicle” type in both truck & sedan. Give truck the field “fourWheel” which will be set to bool. Give sedan the field “luxury” which will be set to bool. Using the vehicle, truck, and sedan structs:

1. using a composite literal, create a value of type truck and assign values to the fields;
1. using a composite literal, create a value of type sedan and assign values to the fields;
1. Print out each of these values;
1. Print out a single field from each of these values.

Hints:

1. To embed a struct within another, just type out the struct's name at the bottom of the other fields without the type struct accompanying it.

Solution:

```golang
package main

import "fmt"

type vehicle struct {
	doors int
	color string
}

type truck struct {
	fourWheel bool
	vehicle
}

type sedan struct {
	luxury bool
	vehicle
}

func main() {
	bigTruck := truck{
		fourWheel: true,
		vehicle: vehicle {
			doors: 5,
			color: "red",
		},
	}
	mySedan := sedan {
		luxury: true,
		vehicle: vehicle{
			doors: 2,
			color: "yellow",
		},
	}

	fmt.Println(bigTruck)
	fmt.Println(bigTruck.doors)
	fmt.Println(mySedan)
	fmt.Println(mySedan.color)
}
```

---

## Question 49

Question:  
Assuming that we have some email addresses in the "username@companyname.com" format, write program to print the user name of a given email address. Both user names and company names are composed of letters only.

Example:  
If the following email address is given as input to the program: john@gmail.com
Then, the output of the program should be: john

Hints:

1. use strings.Index for this. Syntax is strings.Index(str, char).

Solution:

```golang
package main

import (
	"fmt"
	"strings"
)

// func to extract name from address. Takes string, returns string.
func returnName(address string) (name string) {
	// use strings.Index(str, char) to return the index of specific character
	idx := strings.Index(address, "@")
	// return a string up to but not including the @
	name = address[:idx]
	return
}

func main() {
	email := "john@gmail.com"
	name := returnName(email)
	fmt.Println(name)
}
```

---

## Question 50

Question:
Assuming that we have some email addresses in the "username@companyname.com" format, write program to print the company name of a given email address. Both user names and company names are composed of letters only.

Example:
If the following email address is given as input to the program: john@google.com
Then, the output of the program should be: google

Hints:

1. Use strings.Index for this. Syntax is strings.Index(str, char).
1. Remember to exclude the dot "." as well.

Solution:

```golang
package main

import (
	"fmt"
	"strings"
)

// func to extract company from email address. Takes string, returns string
func returnCompany(address string) (company string) {
	// index has to be (index of @ + 1) to exclude @ from the return
	idx := strings.Index(address, "@") + 1
	// get the index of the dot to exclude it from the return
	dot := strings.Index(address, ".")
	company = address[idx:dot]
	return
}

func main() {
	email := "john@google.com"
	company := returnCompany(email)
	fmt.Println(company)
}

```

---

## Question 51

Question:  
Write a program which accepts a sequence of words. The program then should check to see if any of the strings are ints and floats. If any floats exists, round them up and convert them to ints. Finally add any ints thus found to a slice and output it.

Example:  
If the following words is given as input to the program: 2 cats and 3 dogs.
Then, the output of the program should be: [2 3]

If the following words is given as input to the program: 2.3 apples and 14 oranges
Then, the output of the program should be: [2 14]

Hints:

1. You can add a user input facility;
1. Add facility to convert floats to ints and add them to the output slice if they are in the string.

```golang

package main

import (
	"bufio"
	"fmt"
	"math"
	"os"
	"strconv"
	"strings"
)

// func to take user input
func userInput() (input string) {
	reader := bufio.NewReader(os.Stdin)
	fmt.Println("Please input a string. The program will output any integers it finds:\t")
	input, _ = reader.ReadString('\n')
	input = strings.TrimSpace(input)
	return
}

// func to assess string for ints. Takes string, returns slice of ints and bool
func checkStr(myString string) (mySlc []int, valid bool) {
	strArr := strings.Split(myString, " ")
	for i := 0; i < len(strArr); i++ {
		// checking for floats
		elemFlt, err := strconv.ParseFloat(strArr[i], 64)
		if err == nil {
			elemFlt = math.Round(elemFlt)
			mySlc = append(mySlc, int(elemFlt))
			valid = true
			// checking for ints
		} else {
		elem, err := strconv.Atoi(strArr[i])
		if err == nil {
			mySlc = append(mySlc, elem)
			valid = true
			}
		}
	// if no floats and ints are found, nothing will be appended and valid remains false
	}
	return
}

func main() {
	inp := userInput()
	mySlc, valid := checkStr(inp)
	if valid {
		fmt.Println(mySlc)
	} else {
		fmt.Println("No integers in your string")
	}
}
```

---

## Question 52

Question:
Define a type human with struct as the underlying type. Extend it with a type called nationality which is equally a struct. Add a method that prints the nationality.

Hints:

1. Embed sub-types into top-level types;
1. Methods in Go have to be defined outside the structs;
1. The syntax of methods is: func (r receiver) identifier(parameters) (return/s) {}

Solution:

```golang
package main

import "fmt"

// the top-level type with the sub-type at the bottom of the list
type human struct {
	fname, lname, gender string
	age int
	nationality
}

// the sub-type
type nationality struct {
	continent, country string
}

// the method. Very similar to a function in syntax except for the (r receiver)
// following the func keyword.
func (h human) speak() (speech string) {
	speech = fmt.Sprintf("Hi, my name is %v %v. I am %v and I am a citizen of %v, which is a country belonging to the continent of %v", h.fname, h.lname, h.age, h.continent, h.country)
	return
}

func main() {
	// initialising an instance of type human
	joe := human{
		fname: "Joseph" ,
		lname: "Debono",
		age: 47,
		nationality: nationality{
			continent: "Europe",
			country: "Malta",
		},
	}
	// invoking the method
	joePerson := joe.speak()
	fmt.Println(joePerson)
}
```

---

## Question 53

Question:  
Create an type called colour of underlying type struct. The colour fields should include red, green, blue. Add a method to struct. The method should output the red green blue value in CSS style. Initialize two instances of this type.

Example:
If you submit the following values: 12, 54, 87
The output should be: rgb(12,54,87)

Hints:

1. If you like you can add a facility to take the values from the user. If so add error checking to validate the input. Remember that the RGB values are of type uint8;
1. RGB CSS syntax looks like this: rgb(34, 56, 123)

Solution:

```golang
package main

import (
	"bufio"
	"fmt"
	"os"
	"strconv"
	"strings"
)

// defining the colour struct
type colour struct {
	red, green, blue uint8
}

// the method to generate the rgb field
func (col colour) formRGB() (rgb string) {
	rgb = fmt.Sprintf("rgb(%v,%v,%v)", col.red,col.green,col.blue)
	return
}

// func to take user input which must consist of 3 uint8 types. Returns r, g, b uint8
func userInput() (r,g,b uint8) {
	reader := bufio.NewReader(os.Stdin)
	// slice to take the values as they are submitted
	mySlc := make([]uint8, 0)
	for len(mySlc) < 3 {
		fmt.Println("Please input an integer from 0-255 to generate an RGB values. Any input other than such an integer will be discarded. This will keep looping until all required uint8s have been inputted:\t")
	input, _ := reader.ReadString('\n')
	input = strings.TrimSpace(input)
	// returns val uint8, error bool
	val, error := testInput(input)
	// if error is false, append val to mySlc
	if !error {
		mySlc = append(mySlc, val)
		}
	}
	// spread vales of mySlc into r, g, b
	r, g, b = mySlc[0], mySlc[1], mySlc[2]
	return
}

// func to validate user input. Takes input string, returns val uint8 and error bool
func testInput(input string) (val uint8, error bool) {
	strElem := strings.Split(input, " ")[0]
	elemInt, err := strconv.Atoi(strElem)
	// if no err, and the elemInt is between 0 and 255, turn it into a uint8
	if err == nil && elemInt >= 0 && elemInt <= 255 {
		val = uint8(elemInt)
		error = false
	} else {
		val = 0
		error = true
	}
	return
}

func main() {
	r, g, b := userInput()
	myNewCol := colour{red: r, green: g, blue: b}
	myNewColString := myNewCol.formRGB()
	fmt.Println(myNewColString)
}
```

---

## Question 54

Question:  
Define a type circle of underlying type struct. Circle has a radius field of type float64. The circle type has a method that returns the area.

Example:  
If my circle has a radius of 5.0 units, it has an area of 78.539.

Solution:

```golang
package main

import (
	"fmt"
	"math"
)

type circle struct {
	radius float64
}

// the method to return the area
func (c circle) makeArea() (area float64) {
	area =   math.Pi * math.Pow(c.radius, 2)
	return
}

func main() {
	myCircle := circle{radius: 5.0}
	areaOfMyCircle := myCircle.makeArea()
	fmt.Println(areaOfMyCircle)
}
```

---

## Question 55

Question:  
Define a type named rectangle of underlying type struct. It has two fields of type float64, length and width. The rectangle type has a method that can compute the area.

Example:  
If my rectangle has a length of 10 and width of 3.45, it has an area of 34.5.

Solution:

```golang
package main

import "fmt"

type rectangle struct {
	length, width float64
}

// method to compute area
func (r rectangle) computeArea() (area float64) {
	area = r.length * r.width
	return
}

func main() {
	myRec := rectangle{length: 10.0, width: 3.45}
	areaOfMyRec := myRec.computeArea()
	fmt.Println(areaOfMyRec)
}
```

---

## Question 56

Question:  
Define a type circle of underlying type struct. Circle has a radius field of type float64. Define another type named rectangle of underlying type struct. It has two fields of type float64, length and width. Each tpye has a method called computeArea() to calculate the area. Then create an interface called shape that includes the method computeArea() making both circle and rectangle a value of the type shape as well. Create a type of each circle and rectangle, and use the computeArea() method to return the area of each shape.

Example:  
If my rectangle has a length of 10 and width of 3.45, it has an area of 34.5;
and
If my circle has a radius of 5.0 units, it has an area of 78.539.

Hints:

1. The interface gives all types whose methods are listed in the interface the type of the interface;
1. The methods can be generic (i.e. a simple print function);
1. Or they can be methods specific to their type, and the interface will run the relevant one;
1. In either case you will have to create one for each type because you need to include the type in the receiver;
1. Finally write a func that takes the interface type so that it may call both types and their methods with the same func.

Solution:

```golang
package main

import (
	"fmt"
	"math"
)

type circle struct {
	radius float64
}

type rectangle struct {
	length, width float64
}

// the computeArea() for the circle
func (c circle) computeArea() (area float64) {
	area = math.Pi * math.Pow(c.radius, 2)
	return
}

// the computeArea() for the rectangle
func (r rectangle) computeArea() (area float64) {
	area = r.length * r.width
	return
}
```

---

## Question 57

Question:  
Create a program that consists of an anonymous function, a function expression, and generates a returned function.

Hints:

1. Anonymous functions are funcs without a name and executed with parentheses at the end;
1. A function expression is very similar but is returned to a variable;
1. A returned function is very similar to any other function except that it has a function in its return space.

Solution:

```golang
package main

import "fmt"

// the function to return a func. Note the syntax. Also arguments are passed
// to the myReturnedStr() func not the anonymous func within it.
// This returned function itself returns a string literal.
func myReturnedStr(str string) func() string {
	// the returned func is an anonymous func prefaced with return
	return func() string {
		myStr := fmt.Sprintf("Hi, the submitted string is %v", str)
		return myStr
	}
}

func main() {
	// an anonymous function. Note the parentheses executing the function
	func(x, y int) {
		fmt.Println(x + y)
	}(5, 6)
	// a function expression
	mySumFunc := func(x, y int) {
		fmt.Println( x + y)
	}
	mySumFunc(4, 10)
	// the returned function. returnedMe() is the returned function
	returnedMe := myReturnedStr("Hello!")
	// testStr is the string returned by returnedMe(), which is a returned function
	testStr := returnedMe()
	// printing out the returned string from the returned function.
	fmt.Println(testStr)
}
```

---

## Question 58

Question:  
● create a func with the identifier foo that
○ takes in a variadic parameter of type int
○ pass in a value of type []int into your func (destructure the []int)
○ returns the sum of all values of type int passed in
● For comparisons, create a func with the identifier bar that
○ takes in a parameter of type []int
○ returns the sum of all values of type int passed in

Hints:

1. Variadic parameters are a varying number of parameters passed to a function;
1. When a number of arguments are passed as variadic parameters to the function, they are passed in as a slice, which you can then process as such;
1. You can also pass an array/slice and then destructure it to pass its elements as variadic arguments

Solution:

```golang
package main

import "fmt"

// the foo func takes variadic parameters and returns an int.
// the ellipsis preceding the type tells the func that myInt is a variable sequence of
// parameters
func foo(myInt ...int) (sum int) {
	for _, val := range myInt {
		sum += val
	}
	return
}

// func that takes just an []int
func bar(intArr []int) (sum int) {
	for _, val := range intArr {
		sum += val
	}
	return
}

func main() {
	// a slice
	a := []int{1,2,3,4,5}
	// slice submitted to the variadic function and destructured with the
	// subsequent ellipsis
	returnedArrFoo := foo(a...)
	// variadic arguments passed independently. They do not need to be destructured
	// hence no subsequent ellipsis
	fooedArgs := foo(10,20,30,40,50)
	// a slice to be passed to bar(), a non-variadic function
	arrToSum := []int{50, 60, 70}
	summedArr := bar(arrToSum)
	// printing the returns
	fmt.Println(returnedArrFoo)
	fmt.Println(fooedArgs)
	fmt.Println(summedArr)
}
```

---

## Question 59

Question:  
Create a program that makes use of a callback function to create a function that can return even numbers. Your function to return evens takes a func and variadic parameters to check ints and return them if they are even numbers.

Hints:

1. The syntax of the callback function is conventional, i.e. func identifier(parameters) returns {code};
1. But to define the callback function in its receiver function, you have to nest the syntax of the callback function in the parameter parentheses of the receiver functions,

Solution:

```golang
package main

import "fmt"

// this is the callback function. It will take an integer and return a bool to indicate
// whether the argument is an even number or not.
func callMeToSiftEvens(a int) (flag bool) {
	if a % 2 == 0 {
		flag = true
	} else {
		flag = false
	}
	return
}

// findEvens is the receiver function for the callback. Observe how the callback func
// is defined in the parameter parentheses of the receiver function. It also takes
// variadic parameters of ints to be checked by the callback to determine if they are
// even numbers or not.
func findEvens(f func(a int) (flag bool) , nArgs ...int) (evenSlc []int) {
	// the variadic params are in a slice and will be processed by iterating over it
	for i := 0; i < len(nArgs); i++ {
		// check whether the arg is even by running it through the callback func
		flag := f(nArgs[i])
		// if the return from the callback func is true, append it to slice defined
		// by the naked return
		if flag {
			evenSlc = append(evenSlc, nArgs[i])
		}
	}
	return
}

func main() {
	// x takes the returns from the findEvens func the arguments of which are
	// the callback func and a set of variadic arguments
	x := findEvens(callMeToSiftEvens, 1,2,3,4,5,6,7,8,9,10)
	fmt.Println(x)
}
```

---

## Question 60

Question:  
Create a type called shape of underlying type struct with no fields. Within it embed another struct of type square. The square type has the fields length and breadth of type float64. Both types have access to a method that can print the area of type float64

Hints:

1. To declare and initialise an instance of shape of underlying type square the syntax is. Note the comma: a: = shape{
   square{length: 10, breadth: 20},
   }

Solution:

```golang
package main

import "fmt"

// the type shape of underlying type struct
type shape struct {
	// the sub-type square embedded in shape
	square
}

// type square of underlying type struct
type square struct {
	length, breadth float64
}

// func area receives type shape and returns the area
func (s shape) area() float64 {
	return s.length * s.breadth
}

func main() {
	// creating a square. Note how first shape is created, and then nested
	// square embedded type
	mySq := shape{
		square{length: 10, breadth: 23.43},
	}
	// returning the area from the area method.
	mySquareArea := mySq.area()
	fmt.Println(mySquareArea)
}
```

---

## Question 61

Question:

1. create a person struct
1. create a func called “changeMe” with a \*person as a parameter
1. change the value stored at the \*person address
1. create a value of type person
   i. print out the value
1. in func main
   i. call “changeMe”
1. in func main
   i. print out the value

Hints:

1. to dereference a struct, use (*value).field. Note the difference: # p1.first # (*p1).first (pointer type to p1.first)
1. “As an exception, if the type of x is a named pointer type and (\*x).f is a valid selector expression denoting a field (but not a method), x.f is shorthand for (\*x).f.”

```golang
package main

import "fmt"

type person struct {
	fname, lname string
}

// func that takes a type of pointer to person and then changes the field by
// deferencing the value at the pointer
func changeMe(p *person) {
	// the syntax to dereference the field of a struct is (*person).field
	(*p).fname = "Jack"
	(*p).lname = "Burke"
}

func main(){
	// create a instance of person type
	newPer := person{fname: "John", lname: "Doe"}
	fmt.Println(newPer)
	// call change me with pointer to newPer and change it
	changeMe(&newPer)
	fmt.Println(newPer)
}
```

---

## Question 62

Question:  
Print a unicode string "hello world".

Hints:

1. All that is necessary to convert a string to unicode in go is to cast it into an rune array: []rune("Hi, There!")

Solution:

```golang
package main

import "fmt"

func main() {
	a := "Hello World"
	b := []rune(a)
	fmt.Println(b)
}
```

---

## Question 63

Question:  
Write a program to read an ASCII string and to convert it to a unicode string encoded by utf-8.

Hints:

1. The strategy here is:
   i. Convert the ascii string to a unicode rune array
   ii. then transform that unicode rune array back into a string which, this time will be unicode utf-8 encoded

Solution:

```golang
package main

import (
	"fmt"
	"strings"
)

// func to take the ascii-encoded string and return a string encoded in unicode with
// utf-8
func asciiToUnicodeString(asciiStr string) string {
	// creating a string slice
	a := make([]string, 0)
	// splitting arg into a string array
	strArr := strings.Split(asciiStr, "")
	for i := 0; i < len(strArr); i++ {
		// converting the ascii char to a unicode rune
		unicodeI := []rune(strArr[i])
		// converting unicode rune to unicode utf-8 encoded string
		uniStr := string(unicodeI)
		a = append(a, uniStr)
	}
	// joining the string slice and returning it
	return strings.Join(a, "")
}

// func to validate that the original string contained only ascii characters. Takes a
//
func validateAscii(myStr string) (result bool) {
	// start result with value of true
	result = true
	// create a rune array from myStr
	strArr := []rune(myStr)
	// create string slice
	mySlc := make([]int, 0)
	for i := 0; i < len(strArr); i++ {
		// convert each rune to its int value
		intChar := int(strArr[i])
		// append int value of each rune to mySlc
		mySlc = append(mySlc, intChar)
	}
	// check each int to see whether they fall into ASCII range (> 0 && < 128)
	for _, value := range strArr {
		if value < 0 || value > 127 {
			// if value is outside ASCII range, switch result to false
			result = false
		}
	}
	return
}

func main() {
	// ascii string
	myStr := "Hello World!"
	// verifying valid ascii string
	result := validateAscii(myStr)
	// if the result is true
	if result {
	// convert ascii string to unicode string
	unicodedStr := asciiToUnicodeString(myStr)
	fmt.Println(unicodedStr)
	// if result if false, i.e. non-ascii chars were discovered in the string
	} else {
		// print an error message
		fmt.Println("Your string contains non-ASCII characters!")
	}
}
```

---

## Question 64

Question:  
Write a program to compute 1/2 + 2/3 + 3/4 ...+n/n+1 with a given n int or float input where n>0. If the input is a float, round it off to an int. Compute the sum and output the answer as float to 2 decimal places. The input n is to be provided by the user.

Example:  
If the following n is given as input to the program: 5  
Then, the program should compute 1/2 + 2/3 + 3/4 + 4/5 + 5/6  
And the output of the program should be: 3.55.

Hints:

1. Go won't compute the fractions unless yours types are floats.

Solution:

```golang
package main

import (
	"bufio"
	"fmt"
	"math"
	"os"
	"strconv"
	"strings"
)

// func to get user's input. Func will return the user's input as a int
func getInput() (n int) {
	// the flag to keep the while loop going until valid input is provided
	flag := false
	//creating a new reader
	reader := bufio.NewReader(os.Stdin)
	for !flag {
		fmt.Println("Please input a number of type int or float to use as n to compute 1/2 + 2/3 + 3/4 ...+n/n+1. Any other input will be rejected and the program will loop until valid input is provided:\t")
		userInpt, _ := reader.ReadString('\n')
		userInpt = strings.TrimSpace(userInpt)
		n, flag = validateInput(userInpt)
	}
	return
}

// func to test user's input. Will return n type int and flag bool, true if input
// is valid, n = 0 and false otherwise. The flag bool will stop the while loop in
// getInput() if it's valid.
func validateInput(userStr string) (n int, flag bool) {
	flag = false
	// getting the first element from the userStr split into an array
	elem := strings.Split(userStr, " ")[0]
	// check if elem is a float64
	testElem, error := strconv.ParseFloat(elem, 64)
	if error == nil {
		// if so, set the elem to n and flag to true
		n = int(math.Round(testElem))
		flag = true
	}
	// if elem is not a float64, test if elem is an int
	intElem, error := strconv.Atoi(elem)
	if error == nil {
		// if so, convert intElem to float64 and set it to n, also set flag to true
		n = intElem
		flag = true
	}
	// else set n to 0.00 and return n and flag == false
	if !flag {
		n = 0
	}
	return
}

// func to compute the required sum. Takes n float64, returns sum float64
func computeSum(n int) (sum float64) {
	for i := 1; i <= n; i++ {
		// compute the sum by making sure that both numerator and denominator are
		// float64s
		i := float64(i) / (float64(i) + 1.00)
		sum += i
	}
	return
}

func main() {
	n := getInput()
	omnia := computeSum(n)
	fmt.Printf("%.2f\n", omnia)
}
```

---

## Question 65

Question:  
Write a program to compute: f(n)=f(n-1)+100 when n>0 and f(0)=0 with a given n input by console (n>0).

Example:  
If the following n is given as input to the program: 5
Then the output of the program should be: 500

Hints:

1. This is a recursive function with a base case of 0 returning 0;
1. Base case 1: f(n)=0 if n=0.

Solution:

```golang
package main

import (
	"bufio"
	"fmt"
	"math"
	"os"
	"strconv"
	"strings"
)

// func to get userInput and validate it. Can take int and float. Returns int
func getInput() (n int) {
	// bool to keep the while loop going
	flag := false
	reader := bufio.NewReader(os.Stdin)
	for !flag {
		fmt.Println("Please input an int for the recursive function. Ints and floats are accepted. Anything else will be rejected:\t")
		inp, _ := reader.ReadString('\n')
		inp = strings.TrimSpace(inp)
		n, flag = validateInp(inp)
	}
	return
}

// func to validate user input. Takes string, returns int and result bool.
// if arg is a valid int, returns int and true. Else returns 0 and false.
func validateInp(inp string) (n int, result bool) {
	result = false
	// get the first elem from the string array of inp
	elem := strings.Split(inp, " ")[0]
	// check if elem is a float
	testFloat, err := strconv.ParseFloat(elem, 64)
	if err == nil {
		// if so round it, and convert it to an int
		n = int(math.Round(testFloat))
		// set result to true
		result = true
	}
	// else check if it's an int
	testInt, err := strconv.Atoi(elem)
		if err == nil {
			// if so set elem to n and result to true
			n = testInt
			result = true
	}
	// if not, return 0 and false
	if !result {
		n = 0
	}
	return
}

// the recursive function. Takes an int, returns an int
func computeFunc(n int) int {
	// the base case is 0 returning 0
	if n == 0 {
		return 0
	} else {
		return computeFunc(n-1) + 100
	}
}

func main() {
	n := getInput()
	getSum := computeFunc(n)
	fmt.Println(getSum)
}
```

---

## Question 66

Question:  
The Fibonacci Sequence is computed based on the following formula:

Base case 1: f(n)=0 if n=0
Base case 2: f(n)=1 if n=1
Otherwise: f(n)=f(n-1)+f(n-2) if n>1

Write a program to generate the value f(n) when f() computes the Fibonacci sequence as laid out above. Assume that n is supplied by the user and add input validation.

Example:  
If 7 is given as input to the program
Then the output should be 13

Hints:

1. Another recursive function but with two base cases;
1. Base case 1: f(n)=0 if n=0;
1. Base case 2: f(n)=1 if n=1;
1. For some variety, use switch/case instead of if/else in the Fibonacci func;
1. Remember to add input validation.

```golang
package main

import (
	"bufio"
	"fmt"
	"math"
	"os"
	"strconv"
	"strings"
)

// func to get the user's input and returns it as an int, or a float that has been
// rounded and converted to an int. Func will loop until valid input provided
func getUser() (n int) {
	// flag to loop the func until valid input provided
	flag := false
	// reader
	reader := bufio.NewReader(os.Stdin)
	// input loop
	for !flag {
		fmt.Println("Please input a number n, either an int or a float to calculate f(n) where f() computes the Fibonacci sequence. Strings will be discarded. Floats will be rounded and converted to ints:\t")
		nString, _ := reader.ReadString('\n')
		nString = strings.TrimSpace(nString)
		// submit input for validation
		n, flag = validateN(nString)
	}
	return
}

// func to validate input. Takes a string as an argument, returns an int and a bool
// if valid, returns num and result == true. Else returns 0 and false.
func validateN(n string) (num int, result bool) {
	// default value of result is false
	result = false
	// get the first elem of the string split into an array
	elem := strings.Split(n, " ")[0]
	// test to see if elem is a float
	eleFlt, err := strconv.ParseFloat(elem, 64)
	if err == nil {
		// if so, round it and convert to an int
		num = int(math.Round(eleFlt))
		// and set result to true
		result = true
	}
	// otherwise test to see if elem is an int
	eleInt, err := strconv.Atoi(elem)
	if err == nil {
		// if so, set the int to num and result to true
		num = eleInt
		result = true
	}
	// if elem is neither a float nor an int, set num to 0
	if !result {
		num = 0
	}
	return
}

func computeFib(n int) int {
	// the recursive func using a switch/case
	switch n {
	case 0:
		return 0
	case 1:
		return 1
	default:
		return computeFib(n-1) + computeFib(n-2)
	}
}

func main() {
	n := getUser()
	myFib := computeFib(n)
	fmt.Println(myFib)
}
```

---

## Question 67

Question:  
The Fibonacci Sequence is computed based on the following formula:

Base case 1: f(n)=0 if n=0
Base case 2: f(n)=1 if n=1
Otherwise: f(n)=f(n-1)+f(n-2) if n>1

Write a program to generate a slice containing the values of the Fibonacci Sequence to a given n. Assume that n is supplied by the user and add input validation.

Example:  
If 7 is given as input to the program
Then the output should be [0, 1, 1, 2, 3, 5, 8, 13]

Hints:

1. Another recursive function but with two base cases;
1. Base case 1: f(n)=0 if n=0;
1. Base case 2: f(n)=1 if n=1;
1. Remember to add input validation.

Solution:

```golang
package main

import (
	"bufio"
	"fmt"
	"math"
	"os"
	"strconv"
	"strings"
)

// func to get the user's input and returns it as an int, or a float that has been
// rounded and converted to an int. Func will loop until valid input provided
func getUser() (n int) {
	// flag to loop the func until valid input provided
	flag := false
	// reader
	reader := bufio.NewReader(os.Stdin)
	// input loop
	for !flag {
		fmt.Println("Please input a number n, either an int or a float to calculate f(n) where f() computes the Fibonacci sequence. Strings will be discarded. Floats will be rounded and converted to ints:\t")
		nString, _ := reader.ReadString('\n')
		nString = strings.TrimSpace(nString)
		// submit input for validation
		n, flag = validateN(nString)
	}
	return
}

// func to validate input. Takes a string as an argument, returns an int and a bool
// if valid, returns num and result == true. Else returns 0 and false.
func validateN(n string) (num int, result bool) {
	// default value of result is false
	result = false
	// get the first elem of the string split into an array
	elem := strings.Split(n, " ")[0]
	// test to see if elem is a float
	eleFlt, err := strconv.ParseFloat(elem, 64)
	if err == nil {
		// if so, round it and convert to an int
		num = int(math.Round(eleFlt))
		// and set result to true
		result = true
	}
	// otherwise test to see if elem is an int
	eleInt, err := strconv.Atoi(elem)
	if err == nil {
		// if so, set the int to num and result to true
		num = eleInt
		result = true
	}
	// if elem is neither a float nor an int, set num to 0
	if !result {
		num = 0
	}
	return
}

// func to compute the nth term of the fibonacci sequence using a recursive function.
// returns the nth terms as an int.
func computeFib(n int) int {
	if n == 0 {
		return 0
	} else if n == 1{
		return 1
	} else {
		return computeFib(n-1)+computeFib(n-2)
	}
}

//func to create an array containing the Fibonacci sequence up to the nth term supplied
// by the user and computed by computeFib(). Returns array of a Fib sequence.
func genArr(n int) (fib []int) {
	for i := 0; i <= n; i++ {
		myFib := computeFib(i)
		fib = append(fib, myFib)
	}
	return
}

func main() {
	n := getUser()
	fibArr := genArr(n)
	fmt.Println(fibArr)
}
```

---

## Question 68

Question:  
Write assert statements to verify that every number in the list [2,4,6,8] is even.

```golang

```

---

## Question 69

Question:  
Create and compile a Go program importing funcs/vars from an external package you have created yourself. The program should take a simple slice of ints and run a function on it from another go package that you have created.

Hints:

1. Run "go mod init folder/target_folder"
1. Create a file called pkg_exercise.go and in it create an int[] slice of ints;
1. In an external package in the same folder, create another package called evens.go;
1. In evens.go create a function to test individual ints submitted by pkg_exercise.go to test if they are ints or not;
1. Finally compile the program and run it;
1. To compile on different platforms: [How to Build Go Executables for Multiple Platforms](https://www.digitalocean.com/community/tutorials/how-to-build-go-executables-for-multiple-platforms-on-ubuntu-16-04)

```bash
# the path should be within the usual Go folder setup in src/github.com/user/target
go mod init jadebono/pkg_exercise
go mod tidy
# At this point, create pkg_exercise.go and evens.go and write the code in these files.
# When you are ready to compile:
go build
# To run the compiled file.
./pkg_exercise
```

```golang
// the pkg_exercise.go file
package main

import "fmt"

func main() {
	nums := []int{0,2,3,5,6,23,56, 65, 88}
	evenNums := make([]int, 0)
	for _, v := range nums {
		// func TestEvens() from evens.go is accessible because the first letter is in
		// caps, and it does not need to be imported.
		n, result := TestEvens(v)
		if result {
			evenNums = append(evenNums, n)
		}
	}
	fmt.Println(evenNums)
}
```

```golang
package main

// func TestEvens()  takes int and returns int and result. even int is the submitted n
// and result bool is true if the n int is an even, otherwise even is 0 and result is
// false. TestEvens() is made available to pkg_exercise.go because the first letter
// is a capital.
func TestEvens(n int) (even int, result bool) {
	even = 0
	result = false
	if n % 2 == 0 {
		even = n
		result = true
	}
	return
}
```

---

## Question 70

Question:  
Write a binary search function which searches an item in a sorted array. The function should return the index of element to be searched in the list.

Hints:

1. First check the midpoint;
1. If the midpoint is smaller than the elem, search the midpoint of the segment to the right;
1. If smaller, check the midpoint of the segment to the left

Solution:

```golang
package main

import (
	"fmt"
	"math"
	"sort"
)


func findBine(arr []int, elem int) (n int) {
	// set the initial bottom index to the index of the 1st elem of arr
	bottom := float64(0)
	// set the initial top index to the index of the last elem of arr
	top := float64(len(arr) - 1)
	// set the current index to the index of the last elem of arr
	idx := float64(len(arr) - 1)
	for top >= bottom && idx == float64(len(arr) - 1) {
		mid := int(math.Round((top+bottom) / 2.0))
		if arr[mid] == elem {
			idx = float64(sort.SearchInts(arr, arr[mid]))
		} else if arr[mid] > elem {
			top = float64(mid-1)
	} else {
		bottom = float64(mid + 1)
		}

	}
n = int(idx)
return
}

func main() {
	arrToSearch := []int{1,2,3,4,5,6,7,8,9,10}
	// carry out a binary search on array element 3 at index arrToSearch[2]
	idx := findBine(arrToSearch, 3)
	fmt.Printf("The index in the array of your input %v is %v\n", arrToSearch[idx], idx)
}
```

---

## Question 71

Question:  
Generate a random float64 whose value is between 10 and 100 using the math/rand package. The output should be formatted to 2 places after the decimal point.

Hints:

1. The math/rand package is Go's pseudorandom number;
1. This package is deterministic so it will produce the same number each time;
1. To produce a different number, give it a seed that changes;
1. To provide such a seed, create a new rand.Source using a unix time, and then using that seed to generate a new Rand.

Solution:

```golang
package main

import (
	"fmt"
	"math/rand"
	"time"
)

// func to create a rnd number. Returns the rnd number as a float.
func getRnd() (rnd float64) {
	// create a seed using the current time in unix time
	s1 := rand.NewSource(time.Now().UnixNano())
	// using the seed to create a new random number
	r1 := rand.New(s1)
	// returning the rand as a number between 0.0 and 0.1, hence multiply it by hundred
	//to put it in a range between 0 and 100
	rnd = r1.Float64() * 100
	return
}

func main() {
	// creating a flag to use for the while loop
	flag := false
	// create the myRand float64 int
	var myRand float64
	// start the while loop
	for !flag {
		// get a random number from the getRnd() func
		rnd := getRnd()
		// if the rnd number: rnd >= 10 && rnd <= 100
		if rnd >= 10 && rnd <= 100 {
			// switch flag to true to stop the while loop
			flag = true
			// and set myRand to rnd
			myRand = rnd
		}
	}
	// at this point you can either use myRand as a float64 or output it as a formatted
	// string with the appropriate verb to meet the requirements of the assignment
	fmt.Printf("%.2f\n", myRand)
}
```

---

## Question 72

Question:  
Generate a cryptographically secure random int whose value is between 10 and 100 using the crypto/rand package.

Hints:

1. The crypto/rand package is Go's cryptographically secure pseudo random number generator;
1. This package has only a limited number of functions, including .Int, .Prime, and .Read;
1. This package needs to be used with the math/big package because crypto/rand.Int() needs big.NewInt to supply the upperbound;
1. As such the random number generated is of \*big.Int type;
1. Unfortunately, you cannot compare a \*big.Int type with other types with normal logical operators. To this end, you will have to use bigIntNum.Cmp() to do so.

Solution:

```golang
package main

import (
	"crypto/rand"
	"fmt"
	"math/big"
)

// the func to generate a cryptographically secure random number. It returns the number
// type *big.Int
func genCryptoRnd(min int64) (myRnd *big.Int) {
	flag := false
	// convert int64 nFloor to type *big.Int
	nFloor := big.NewInt(min)
	// start for loop
	for !flag {
	// rand.Int generates a cryptographically secure pseudo random int using
	// rand.Reader and big.NewInt that gives the upperbound of the range starting from 0
    rnd, _ := rand.Int(rand.Reader, big.NewInt(100))
	// comparing *big.Int to a primitive type can only be done with the .Cmp(type)
	// method with values ranging from -1 (x < y) to 0 (x == y) to 1 (x > y)
	// note that since the ceiling is set in big.NewInt(100), there is no need
	// to compare it to a supplied ceiling
	if rnd.Cmp(nFloor) > -1 {
		// if the above conditions are valid, set flag to true to exit loop and myRnd
		// to rnd
		flag = true
		myRnd = rnd
		}
	}
	return
}

func main() {
	// define the floor
	var min int64 = 10
	// run the genCryptoRnd() func to get the required random number
	x := genCryptoRnd(min)
	fmt.Println(x)
}
```

---

## Question 73

Question:  
Generate a random float where the value is between 5 and 95 using Go's crypto/rand package.

Hints:

1. Remember to use the math/big package because crypto/rand.Int() needs big.NewInt to supply the upperbound.

Solution:

```golang
package main

import (
	"crypto/rand"
	"fmt"
	"math/big"
)


// func to generate a cryptographically secure pseudo random number. Takes a floor
// and ceiling *big.Int types as args. Returns a random *big.Int number between
// these two values
func getMyRnd(max, min *big.Int) (rndN *big.Int) {
	// set up flag for the for loop
	flag := false
	for !flag {
		// use the rand.Int func to generate the random number
		rnd, err := rand.Int(rand.Reader, max)
		// using the .Cmp() to check that the number generated is smaller than the floor
		if err == nil && rnd.Cmp(min) > 0 {
			// if so, stop the loop and set rnd to rndN
			flag = true
			rndN = rnd
		}
	}
	return
}

func main() {
	// create the floor and ceiling as *big.Int types
	max, min := big.NewInt(95), big.NewInt(5)
	// call the getMyRnd() func
	myRnd := getMyRnd(max, min)
	fmt.Println(myRnd)
}
```

---

## Question 74

Question:  
Generate a cryptographically secure pseudo random number of type int. The floor and ceiling values should be supplied to the program from the CLI.

Hints:

1. For cryptographically secure pseudo random numbers, use the crypto/rand package;
1. Remember to use the math/big package because crypto/rand.Int() needs big.NewInt to supply the upperbound;
1. The second arg in rand.Int() is exclusive of your ceiling, so if you want a ceiling of 10, the second arg has to be 11.

Solution:

```golang
package main

import (
	"crypto/rand"
	"fmt"
	"math"
	"math/big"
	"os"
	"strconv"
)

// func to test the args. Takes arg string, returns n int and err error
func testArgs(arg string) (n int, err error) {
	// attempt to check if arg is a float
	myNumFlt, err := strconv.ParseFloat(arg, 64)
	if err == nil {
		// if it is a float, round it and convert to int
		n = int(math.Round(myNumFlt))
		err = nil
		return
	}
	// if not a float, check to see if it is an int
	myNumInt, err := strconv.Atoi(arg)
	if err == nil {
		n = myNumInt
		err = nil
		return
		// else set n to 0 and provide an error message
	} else {
		n = 0
		err = fmt.Errorf("One of your arguments is not a valid number")
	}
	return
}

// Func to validate the args of the user. Takes []string, returns two ints, and an error
func validFunc(args []string ) (nFloor, nCeiling int, err error){
	// submit arg[1] (first user arg) to testArgs()
	nFirst, err := testArgs(args[1])
	if err != nil {
		// in cases of error, set the ints and err as below
		nFloor, nCeiling, err = 0, 0, err
	}
	// submit arg[2] (second user arg) to testArgs()
	nSecond, err := testArgs(args[2])
	if err != nil {
		// in cases of error, set the ints and err as below
		nFloor, nCeiling, err = 0, 0, err
	}
	// check which is the smaller int, and set smaller and greater ints to
	// nFloor and nCeiline respectively
	if nFirst < nSecond {
		nFloor, nCeiling = nFirst, nSecond
	} else {
		nFloor, nCeiling = nSecond, nFirst
	}
	return
}

// the func to generate the random number. Takes floor and ceiling ints of
// type *big.Int. Returns the random number of type *big.Int.
func getRand(min, max *big.Int) (rndGen *big.Int) {
	//flag for the for loop
	flag := false
	// Start the for loop to generate a random number between the supplied floor
	// and ceiling
	for !flag {
		rnd, _ := rand.Int(rand.Reader, max)
		// if the random number < than floor, set rndGen to rnd and flag to true
		if rnd.Cmp(min) > 0 {
			rndGen = rnd
			flag = true
			}
		}
	return
}

func main() {
	args := os.Args
	// checks length of args. If args != 3, program stops
	if len(args) != 3 {
		fmt.Printf("You have not supplied enough arguments to the program\n")
		os.Exit(1)
	}
	// if there are 3 args, code starts the validation process for the two args
	// supplied by the user
	if len(args) == 3 {
		min, max, err := validFunc(args)
		if err != nil {
			fmt.Println(err)
		}
		// converting min and max to *big.Int types
		minBig, maxBig := big.NewInt(int64(min)), big.NewInt(int64(max))
		myRnd := getRand(minBig, maxBig)
		// print out the random number generated
		fmt.Printf("Your random number in the range of %v and %v is %v\n", min, max, myRnd)
	}
}
```

---

## Question 75

Question:  
Generate a cryptographically secure pseudo random number of type int. This program should now prompt the user to supply the floor and ceiling values upon execution.

Hints:

1. For cryptographically secure pseudo random numbers, use the crypto/rand package;
1. Remember to use the math/big package because crypto/rand.Int() needs big.NewInt to supply the upperbound;
1. The second arg in rand.Int() is exclusive of your ceiling, so if you want a ceiling of 10, the second arg has to be 11;
1. The values supplied by the user will be of type string. Add validation to check that the string resolves to an int, or to a float (if to a float, round it and convert it to an int). Reject anything else;
1. Do not accept ints of the same value otherwise there will be no range.

Solution:

```golang
package main

import (
	"bufio"
	"crypto/rand"
	"fmt"
	"math"
	"math/big"
	"os"
	"strconv"
	"strings"
)

// the func to generate the random number. Takes floor and ceiling ints of
// type *big.Int. Returns the random number of type *big.Int.
func getRand(min, max *big.Int) (rndGen *big.Int) {
	//flag for the for loop
	flag := false
	// Start the for loop to generate a random number between the supplied floor
	// and ceiling
	for !flag {
		rnd, _ := rand.Int(rand.Reader, max)
		// if the random number < than floor, set rndGen to rnd and flag to true
		if rnd.Cmp(min) > 0 {
			rndGen = rnd
			flag = true
			}
		}
	return
}

// func to get an integer  from the user. Called from func getInput() Returns int64
// sets up a while loop that uses a reader and then checks the input to see whether
// it is an int or a float, or otherwise.
func getInt() (n int64) {
	reader := bufio.NewReader(os.Stdin)
	flag := false
	for !flag {
		thisInt, _ := reader.ReadString('\n')
		thisInt = strings.TrimSpace(thisInt)
		nFlt, err := strconv.ParseFloat(thisInt, 64)
		if err == nil {
			n = int64(math.Round(nFlt))
			flag = true
			return
		}
		nInt, err := strconv.Atoi(thisInt)
		if err == nil {
			n = int64(nInt)
			flag = true
			return
		}
		fmt.Printf("Your supplied input is invalid! Please supply an integer or a float:\t")
	}
	return
}

// func getInput requests the user to supply values to serve as the floor and ceiling
// to define the range from where the get the cryptographically secure pseudo random
// number. Two temp variables, min and max will be used to get the initial values.
// This will serve to allow a comparison between max and min and reject max unless
// max > min
func getInput() (floor, ceiling int64) {
	fmt.Println("This program will generate a cryptographically secure pseudo random from a range delimited by floor and ceiling ints that you supply.\n")
	fmt.Printf("Please supply an integer to serve as the floor of the range. Floats will also be accepted, by they will be rounded and converted to ints. Everything else will be rejected:\t")
	min := getInt()
	fmt.Printf("Please supply an integer to serve as the ceiling of the range. Floats will be accepted but rounded up and converted to an int. Ceiling will also have to be higher than the floor:\t")
	max := getInt()
	floor, ceiling = min, max
	if max == min {
		flag := false
		for !flag {
			fmt.Printf("Your ceiling is the same value of your floor. Please supply a higher value for your ceiling:\t")
			max := getInt()
			if max > min {
				// once max is finally greater than min, set ceiling to max and exit
				// the loop
				ceiling = max
				flag = true
			}
		}
	}
	return
}

func main() {
	min, max := getInput()
		// converting min and max to *big.Int types
		minBig, maxBig := big.NewInt(min), big.NewInt(max)
		myRnd := getRand(minBig, maxBig)
		// print out the random number generated
		fmt.Printf("Your random number in the range of %v and %v is %v\n", min, max, myRnd)
	}
```

---

## Question 76

Question:  
Write a program to generate a cryptographically secure even pseudo random integer. The range is between 0 and 10 inclusive. You can hardwire the values of the floor and ceiling in the code itself. No need to take them in as args from the CLI or prompt the user for them.

Hints:

1. Remember that your number has to be even.
1. The second arg in rand.Int() is exclusive of your ceiling, so if you want a ceiling of 10, the second arg has to be 11;
1. Comparing the rnd number with another one can be done with rnd.Cmp();
1. But modulus is a different matter. You'll have to first convert the rnd number to a string, then the string to an int, and then carry out the comparisons that way.

Solution:

```golang
package main

import (
	"crypto/rand"
	"fmt"
	"math/big"
	"strconv"
)

// this func generates a cryptographically secure even pseudo random number. Takes in
// min of type int and max of type int64 to serve as the floor and ceiling. Returns the random
// even number as type *big.Int
func genEvenRnd(min int, max *big.Int) (rnd *big.Int) {
	flag := false
	// start the while-loop using a flag
	for !flag {
		myRnd, err := rand.Int(rand.Reader, max)
		// since carrying out modulus between *big.Int and int with % is difficult
		// the strategy here converts the myRnd *big.Int to a string
		rndStr := fmt.Sprintf("%v", myRnd)
		// and then converts the string to an int, which it then uses for the logical
		// comparisons in the if-clause below.
		rndInt, _ := strconv.Atoi(rndStr)
		// conditions are that there is no error, that the generated rnd is greater
		// than min, and that it is even
		if err == nil && rndInt >= int(min) && rndInt % 2 == 0 {
			rnd = myRnd
			flag = true
		}
	}
	return
}

func main() {
	// create the ceiling as *big.Int type
	max := big.NewInt(10)
	// create the floor as an int - this will be used to ensure that the random
	// number will be greater than or equal to the floor
	min := 0
	rnd := genEvenRnd(min, max)
	fmt.Println("Your cryptographically secure even pseudo random number is: ", rnd)
	}
```

---

## Question 77

Question:  
Write a program to output a cryptographically secure pseudo random number, which is divisible by 5 and 7, between 0 and 10 inclusive.

Hints:

1. Remember that your number has to be divisible by 5 and by 7;
1. Comparing the rnd number with another one can be done with rnd.Cmp();
1. But modulus is a different matter. You'll have to first convert the rnd number to a string, then the string to an int, and then carry out the comparisons that way;
1. No need to use a floor value for this, just a ceiling one;
1. No need to take the ceiling from CLI args or the user, you can just hardwire it into the code.

Solution:

```golang
package main

import (
	"crypto/rand"
	"fmt"
	"math/big"
	"strconv"
)

// func to get the required rnd num. Takes max *big.Int returns rnd *big.Int, a
// random number between 0 and max that is divisible by both 5 and 7
func getRnd(max *big.Int) (rnd *big.Int) {
	flag := false
	for !flag {
		myRnd, err := rand.Int(rand.Reader, max)
		// converting the generated rnd to a string
		myRndStr := fmt.Sprintf("%v", myRnd)
		// converting the resultant string into an int
		rndInt, _ := strconv.Atoi(myRndStr)
		if err ==  nil && rndInt % 5 == 0 && rndInt % 7 == 0 {
			rnd = myRnd
			flag = true
		}
	}
	return
}

func main() {
	// remember that max is exclusive of the value of your floor, hence max == 1001
	// if you want your floor to be 1000
	max := big.NewInt(1001)
	rnd := getRnd(max)
	fmt.Println("The cryptographically secure pseudo random number from the range between 0 and %v and that is divisible by both 5 and 7 is: ", rnd)
}
```

---

## Question 78

Question:  
Write a program to generate an array with 5 random integers between 100 and 200 inclusive. The type can be either int of some type of \*big.Int

Solution:

```golang
package main

import (
	"crypto/rand"
	"fmt"
	"math/big"
)

// func to generate the cryptographically secure pseudo random number within the range
// floor and ceiling. Takes floor and ceiling *big.Int, returns rnd *big.Int
func getRnds(floor, ceiling *big.Int) (rnd *big.Int) {
	flag := false
	for !flag {
		myRnd, err := rand.Int(rand.Reader, ceiling)
		// the comparison with floor is through myRnd.Cmp()
		if err == nil && myRnd.Cmp(floor) >= 0 {
			rnd = myRnd
			flag = true
		}
	}
	return
}

func main() {
	// define an empty array of type *big.Int with a capacity of 5
	myArr := make([]*big.Int, 0, 5)
	// creating the floor and ceiling. Since the 2nd param of rand.Int is exclusive,
	// the value of max has to be greater than your desired floor.
	min, max := big.NewInt(100), big.NewInt(201)
	// start the loop to populate the array.
	for len(myArr) < 5 {
		// start appending random numbers to the array
		myArr = append(myArr, getRnds(min, max))
	}
	fmt.Println(myArr)
}
```

---

## Question 79

Question:  
Write a program to generate an array with 5 random integers between 1 and 1000 inclusive. Each of the five integers must be divisible by both 5 and 7. The type can be either int of some type of \*big.Int

Hints:

1. Since the range is from 1 to 1000, there is no need for a floor since that is the starting point that rand.Int assumes.

Solution:

```golang
package main

import (
	"crypto/rand"
	"fmt"
	"math/big"
	"strconv"
)

// func to generate the required random. Takes ceiling of type *big.Int and returns
// rnd of type *big.Int
func getRands(ceiling *big.Int) (rnd *big.Int) {
	flag := false
	for !flag {
		myRnd, err := rand.Int(rand.Reader, ceiling)
		// converting myRnd to string
		myRndStr := fmt.Sprintf("%v", myRnd)
		// converting the rnd to int
		myRndInt, _ := strconv.Atoi(myRndStr)
		// checking that there are no errors and that the rnd is divisible by 5 and 7
		if err == nil && myRndInt % 5 == 0 && myRndInt % 7 == 0 {
			rnd = myRnd
			flag = true
		}
	}
	return
}

func main() {
	// declaring an array of type *big.Int with a capacity of 5
	myArr := make([]*big.Int,0, 5 )
	max := big.NewInt(1001)
	// starting to loop to populate the array with 5 random ints of type *big.Int
	for len(myArr) < 5 {
		myArr = append(myArr, getRands(max))
	}
	fmt.Println(myArr)
}
```

---

## Question 80

Question:  
Write a program to generate a cryptographically secure pseudo random integer between 7 and 15 inclusive. Each of the five integers must be divisible by both 5 and 7. The type can be either int of some type of \*big.Int

Solution:

```golang
package main

import (
	"crypto/rand"
	"fmt"
	"math/big"
)

// func to get a rnd int between floor and ceiling. Takes 2 *big.Int params, returns
// a *big.Int rnd
func genRnd(floor, ceiling *big.Int) (rnd *big.Int) {
	flag := false
	for !flag {
		myRnd, err := rand.Int(rand.Reader, ceiling)
		if err == nil && myRnd.Cmp(floor) >= 0 && myRnd.Cmp(ceiling) <= 0 {
			rnd = myRnd
			flag = true
		}
	}
	return
}

func main() {
	// set the values for the floor and ceiling vars as type *big.Int
	// the ceiling is set to 16 because rand.Int is exclusive
	min, max := big.NewInt(7), big.NewInt(16)
	rnd := genRnd(min, max)
	fmt.Println(rnd)
}
```

---

## Question 81

Question:  
Write a program to compress and decompress the string "hello world!hello world!hello world!hello world!".

Hints:

1. Use the compress/zlib package;

Solution:

```golang
package main

import (
	"bytes"
	"compress/zlib"
	"fmt"
	"io"
	"log"
)

// func to compress the input. Takes a pointer of type bytes.Buffer, and the input
// as a byte array. Compresses the input.
func comp(in *bytes.Buffer, strToCompress []byte) {
	// creates the compression writer using the bytes.Buffer
	writeCompress := zlib.NewWriter(in)
	// uses the compression writer to compress the input
	writeCompress.Write(strToCompress)
	// closes the writer
	writeCompress.Close()
	// remove the echoes to print out the compressed string
	// fmt.Println(inBytesBuffer)
}

// func to decompress the compressed string. Takes two bytes.Buffer types pointing to
// bytes.Buffer
func decomp(in, out *bytes.Buffer) {
	// creating the decompression reader
	readDecompress, err := zlib.NewReader(in)
	// the error handling
	if err != nil {
		log.Fatal(err)
	} else {
		// copies the data in readDecompress to the out bytes.Buffer
		io.Copy(out, readDecompress)
		// converting the out bytes.Buffer to a string
		decompressedStr := out.String()
		// printing out the decompressed string
		fmt.Println(decompressedStr)
	}
}

func main() {
	// creating two variables of type bytes.Buffer that will be used to create and read
	// a zlib writer and reader
	var inBytesBuffer bytes.Buffer
	var outBytesBuffer bytes.Buffer
	// the string to be compressed. You can take it from os.Args or prompt the user for
	// it. The string is converted to a byte array.
	myString := []byte("hello world!hello world!hello world!hello world!")
	// compressing the input by passing a pointer to inBytesBuffer
	comp(&inBytesBuffer, myString)
	// decompressing the input by passing pointers to both inBytesBuffer
	// and outBytesBuffer
	decomp(&inBytesBuffer, &outBytesBuffer)
 }
```

---

## Question 82

Question:  
Wite a program to print the running time of the execution of a for-loop that prints numbers 1 - 100 both inclusive. Each number should be printed with its running time.

Hints:

1. Use the time package;
1. Register the starting point in time of the loop by creating a time.Time type from time.Now();
1. At each iteration, calculate the difference in time from the starting point by getting a time.Duration type from time.Now(start) with start being the time.Time type used to get the time of initialization.

Solution:

```golang
package main

import (
	"fmt"
	"time"
)

// func that runs a loop and prints its time of execution from the starting point of
// time from the beginning of the loop.
func timeLoop() {
	// creates a type time.Time to serve as the starting point for timing each iteration
	// of the loop
	start := time.Now()
	for i := 1; i <= 100; i++ {
		// the second value returns a time.Duration type that prints the difference
		// in time between the moment it is called and the supplied time.Time type
		fmt.Printf("Iteration: %v, time: %v\n", i, time.Since(start))
	}
}

func main() {
	timeLoop()
}
```

---

## Question 83

Question:  
write a program to shuffle and print the array []int{3,6,7,8}.

Hints:

1. Use the shuffle package from math/rand;
1. rand.Shuffle() takes n int for the number of times to execute the shuffle, and a swap function that switches arr[i] with arr[j].

Solution:

```golang
package main

import (
	"fmt"
	"math/rand"
	"time"
)

// func that shuffles array. Takes an []int arr and then shuffles it.
func shuffleMyArr(arr []int) {
	// make a call to rand.seed to ensure that you get different sequences of shuffles
	// every time you run this program
	rand.Seed(time.Now().UnixNano())
	// rand.Shuffle takes an int for the number of times to shuffle, and the swap
	// function to do the shuffling
	rand.Shuffle(len(arr), func(i, j int) {
		arr[i], arr[j] = arr[j], arr[i]
	})
}

func main() {
	// create the array
	myArr := []int{3,6,7,8}
	// shuffle the array
	shuffleMyArr(myArr)
	// print the shuffled array
	fmt.Println(myArr)
}
```

---

## Question 84

Question:  
Write a program to generate all sentences where subject is in []string{"I", "You"} and verb is in []string{"Play", "Love"} and the object is in []string{"Hockey","Football"}.

Hints:

1. The strategy is to nest a loop that ranges over a []string within the other loops that do the same;
1. With golang's range keyword, you can get either the index, or the value, or both from the loop, so the choice is yours whether to form each sentence by getting an element from a string by array notation such arr[elem] or the actual value of the element itself.

Solution:

```golang
package main

import (
	"fmt"
)

// function to generate every possible sentence from a number of []string arrays. Takes
// 3 []string arrays and generates the sentences by ranging them.
func genSen(a, b, c []string) {
	// starting the structure of nested loops to range over the []string arrays
	// in this example, the code is retrieving the actual elements from each []string
	// instead of the index
	for _, i := range a {
		for _, j := range b {
			for _, k := range c {
				fmt.Printf("%v %v %v\n", i, j, k )
			}
		}
	}
}

func main() {
	// defining the []string arrays
	nom := []string{"I", "You"}
	verb := []string{"Play", "Love"}
	acc := []string{"Hockey","Football"}
	genSen(nom, verb, acc)
}
```

---

## Question 85

Question:  
Write a program to print array []int{5,6,77,45,22,12,24} after removing even numbers.

Hints:

1. A golang array of a fixed length is its own type so you can't just delete the elements.

Solution:

```golang
package main

import (
	"fmt"
)

// func that takes an []int and returns another one containing just the integers
func delEvens(arr []int) (oddArr []int) {
	// ranging over the []int
	for _, elem := range arr {
		// if the element is odd, append it to oddArr []int
		if elem % 2 != 0 {
			oddArr = append(oddArr, elem)
		}
	}
	return
}

func main() {
	x := []int{5,6,77,45,22,12,24}
	odds := delEvens(x)
	fmt.Println(odds)
}
```

---

## Question 86

Question:  
Write a program to print an int[] array that contains only the numbers in []int{12,24,35,70,88,120,155} that are divisible by 5 and 7.

Hints:

1. A golang array of a fixed length is its own type so you can't just delete the elements.

Solution:

```golang
package main

import "fmt"

// func that takes an arr []int and returns one containing only the elements
// from the first arr that are divisible by both 5 and 7
func pickInts(arr []int) (fivesAnd7s []int) {
	for _, elem := range arr {
		if elem % 5 == 0 && elem % 7 == 0 {
			fivesAnd7s = append(fivesAnd7s, elem)
		}
	}
	return
}

func main() {
	myArr := []int{12,24,35,70,88,120,155}
	siftedArr := pickInts(myArr)
	fmt.Println(siftedArr)
}
```

---

## Question 87

Question:

Write a program to print the []int{12,24,35,70,88,120,155} array after removing the 0th, 2nd, 4th,6th numbers.

Solution:

```golang
package main

import "fmt"

// func that takes an arr []int and returns one containing only the elements
// the index of which is even
func pickInts(arr []int) (oddIndices []int) {
	for index, elem := range arr {
		if index % 2 == 0 {
			oddIndices = append(oddIndices, elem)
		}
	}
	return
}

func main() {
	myArr := []int{12,24,35,70,88,120,155}
	siftedArr := pickInts(myArr)
	fmt.Println(siftedArr)
}
```

---

## Question 88

Question:

Write a program to generate a [][][]int 3D array. The array should consist of 3 columns and 5 rows of arrays each element of which is 0. Generate the first array of 8 elements each of which is 0 dynamically.

Hints:

1. This array will contain 3 arrays;
1. Each of which contains 5 arrays;
1. Each of which contains 8 elements all of which are 0;

Solution:

```golang
package main

import "fmt"

// func that generates the elemental array and populates it with the element. Takes
// elem, lnt int, and returns an []int
func makeElemArr(elem, lnt int) (arr []int) {
	for i := 0; i < lnt; i++ {
		arr = append(arr, elem)
	}
	return
}

// func that generates the 3d array. Takes rows, cols int, and arr []int. Returns
// threeDArr [][][]int
func genFullArr(rows, cols int, arr []int) (threeDArr [][][]int) {
	// create the slice for the cols
	colsArr := make([][]int, 0)
	// start the loop to populate the cols with the arr []int
	for i := 0; i < cols; i++ {
		colsArr = append(colsArr, arr)
	}
	// finally start the loop to populate the rows with the colsArr
	// which will finalise the 3d array
	for j :=0; j < rows; j++ {
		threeDArr = append(threeDArr, colsArr)
	}
	return
}

func main() {
	elem, length := 0, 8
	rows, cols := 3, 5
	baseArr := makeElemArr(elem, length)
	fullArr := genFullArr(rows, cols, baseArr)
	fmt.Println(fullArr)
}
```

---

## Question 89

Question:

Write a program to print an []int after removing the elements at the 0th, 4th, and 5th indices of []int{12,24,35,70,88,120,155}.

Solution:

```golang
package main

import "fmt"

// func that takes []int and returns a copy of the []int with the elements at the 0th,
// 4th & 5th indices filtered out.
func filterArr(arr []int) (filteredArr []int) {
	for idx, elem := range arr {
		if idx != 0 && idx != 4 && idx != 5 {
			filteredArr = append(filteredArr, elem)
		}
	}
	return
}

func main() {
	myArr := []int{12,24,35,70,88,120,155}
	filterTheArr := filterArr(myArr)
	fmt.Println(filterTheArr)
}
```

---

## Question 90

Write a program to print an []int after removing the element 24 in []int{12,24,35,24,88,120,155}.

Solution:

```golang
package main

import "fmt"

// func to filter the array by the provided element. Takes an elem int, and arr []int.
// Returns a newArr []int with the supplied elem filtered out.
func filterArr(elem int, arr []int) (newArr  []int) {
	for _, value := range arr {
		if value != elem {
			newArr = append(newArr, value)
		}
	}
	return
}

func main() {
	// original array
	originalArr := []int{12,24,35,24,88,120,155}
	// the element to be removed
	elem := 24
	filteredArr := filterArr(elem, originalArr)
	fmt.Println(filteredArr)
}
```

---

## Question 91

Question:

With three given arrays []int{1,3,6,78,35,55}, []int{12,24,35,24,88,120,155}, []int{3,3,24,222,308} write a program to make an []int whose elements are intersection of the above given arrs.

Hints:

1. One way of doing is to create an empty structure to store a unique copy of each element in each array;
1. Once you have populate such a structure, copy each of its elements into a new []int.

Solution:

```golang
package main

import "fmt"

// func that takes in variadic parameters of type []int, returns []int containing only
// the unique elements of each element in each supplied []int
func intersect(arr  ...[]int) (set []int) {
	// this program uses a map to store a unique copy of each element of each submitted
	// []int
	arrMap := make(map[int]bool)
	// the variadic parameter consists of an array of each argument submitted to the
	// func. In this case, the arguments are []ints themselves, so arr is an []int
	// of []ints that you have to range over.
	for _, value := range arr {
		// Once you access the top-level []ints in arr, you need to access the elems
		// in each []int
			for _, val := range value {
				if arrMap[val] == false {
					arrMap[val] = true
				}
			}
	}
	// once all unique elements have been stored in the map, we can start copying
	// every element in that map in the []int we are going to return
	for value := range arrMap {
		if arrMap[value] {
			set = append(set, value)
		}
	}
	return set
}

func main() {
	// The arrays to intersect
	arrA := []int{1,3,6,78,35,55}
	arrB := []int{12,24,35,24,88,120,155}
	arrC := []int{3,3,24,222,308}
	set := intersect(arrA, arrB, arrC)
	fmt.Println(set)
}
```

---

## Question 92

Question:

With a given []int{12,24,35,24,88,120,155,88,120,155}, write a program to print this []int after removing all duplicate values with original order reserved.

Hints:

1. A valid strategy is to create map[int]bool;
1. Create a new []int;
1. Then start a reverse loop counting down from the length of the []int;
1. If the map[arr[i]] == false, then add the current i to new []int;
1. And then set map[arr[i]] to true as this will stop the loop from adding an already included i.

Solution:

```golang

package main

import "fmt"


// func that takes an arr []int, and returns another one with duplicate elements
//filtered out and stored in an order reverse to that of arr []int
func reverseFilter(arr []int) (processedArr []int) {
	// create the map[int]bool
	mpp := make(map[int]bool)
	// start the reverse loop from len(arr) - 1 counting down to 0
	for i:= len(arr) - 1; i >= 0; i--  {
		// if there is no record of arr[i] in mpp[int]bool
		if !mpp[arr[i]] {
			// add arr[i] to the procssedArr
			processedArr = append(processedArr, arr[i])
			// and turn mapp[arr[i]] to true
			mpp[arr[i]] = true
		}
	}
	return
}

func main() {
	arr := []int{12,24,35,24,88,120,155,88,120,155}
	getArr := reverseFilter(arr)
	fmt.Println(getArr)

}
```

---

## Question 93

Question:

Define a class Person and a child class called Gender. Give it an external interface called Get() to define the GetGender() method allowing you to get the gender ("male" or "female" of the Person once you have defined it .

Hints:

1. To define classes in Go, use structs;
1. To create a child class, simply create a struct within the Person Struct;;
1. To make them external, capitalise them.

Solution:

```golang
package main

import (
	"fmt"
)

// creating a public (externally accessible) struct in global scope
type Person struct {
	name, surname string
	Gender struct {
		Gender string
	}
}

// creating an External interface to provide a method to an external struct
type Get interface {
	GetGender() string
}

//func to use Get() from Get External interface on person struct
func (Person Person) GetGender() string {
	return fmt.Sprintf("The gender of %v %v is %v.", Person.name, Person.surname, Person.Gender.Gender)
}

func main() {
	aMale := Person{name: "John", surname: "Doe"}
	aMale.Gender.Gender = "male"
	fmt.Println(aMale.GetGender())
	aFemale := Person{name: "Jane", surname: "Doe"}
	aFemale.Gender.Gender = "female"
	fmt.Println(aFemale.GetGender())
}
```

---

## Question 94

Question:

Write a program that counts and prints the numbers of each character in a SINGLE string supplied as an argument at the CLI.

Example:

1. If the following string is supplied as an argument program: abcdefgabc;
1. Then, the output of the program should be: a,2 c,2 b,2 e,1 d,1 g,1 f,1.

Hints:

1. You can do this by creating a map[string]int the values of which is the number of iteration of the string;
1. There is an added challenge however, the output has to be printed in its original order with not character repeated more than once in the output. Unfortunately, Golang's map are printed in random order;
1. To solve this problem, in this solution, once the map[string]int was created, the original array was filtered to eliminate all iterations of a character except the first one, and then the filtered array was used to loop through map in order and add the retrieved keys:values to a string.

Solution:

```golang
package main

import (
	"fmt"
	"os"
	"strings"
)

// func to return the supplied arr sorted in its original order except that each char
// occurs only one in it.
func filterArr(arr []string) (filteredArr []string) {
	// create a map[string]bool. Once a value occurs in an array, its corresponding
	// value in the map is set to true.
	mpp := make(map[string]bool)
	for _, v := range arr {
		// if the value in mapp is false, set it to true. This will ensure that only
		// one iteration of a character is stored as a key in the mpp
		if !mpp[v] {
			mpp[v] = true
		}
	}
	// start populating the filteredArr by looping over arr.
	for k, _ := range arr {
		// If the corresponding key in mpp is true, add it to filteredArr
		if mpp[arr[k]] {
			filteredArr = append(filteredArr, arr[k])
			// and then set that key in mpp to false, preventing its inclusion again.
			mpp[arr[k]] = false
		}
	}
	return
}

// func to count the number of times each character in the supplied string occurs.
// Takes a string as arg, returns another string.//
func countChars(myStr string) (myOutputString string) {
	// split the supplied string into an array
	arr := strings.Split(myStr, "")
	// create a map the values of which are the numbers of each key
	myMap := make(map[string]int)
	// start looping through arr, and for every iteration of the key, add 1 to
	// myMap[arr[k]]
	for k, _ := range arr {
		myMap[arr[k]] += 1
	}
	// before we start building the return string, we submit the original arr to
	// filteredArr() to filter out any iteration of a character more than 1.
	// filteredArr() returns the arr sorted in its original order except that each char
	// occurs only one in it.
	filteredArr := filterArr(arr)
	// starting the creation of string taking the k:v from myMap according to the order
	// they are stored in filteredArr.
	for _, v := range filteredArr {
		myOutputString += fmt.Sprintf("%v:%v, ", v, myMap[v])
	}
	return
}

func main() {
	args := os.Args
	// test args for length. Only one argument supplied from the CLI so len(args)
	// have to be 2 only.
	if len(args) == 2 {
		// submit the argument to countChars()
		countedCharacters := countChars(args[1])
		// print out the counted characters
		fmt.Println(countedCharacters)
		// if len(args) != 2, inform the user.
	} else {
		fmt.Println("Invalid number of strings supplied! Please run the program with one string supplied as an argument.")
	}
}
```

---

## Question 95

Question:

Write a program that accepts a string as a series of arguemnts from the CLI and print it in reverse order.

Example:

1. If the following string is given as input to the program: rise to vote sir;
1. Then, the output of the program should be: ris etov ot esir.

Hints:

1. Use an inverse loop to append the characters into a slice in inverse order.

Solution:

```golang
package main

import (
	"fmt"
	"os"
	"strings"
)

func reverseString(arr []string) (finalString string) {
	// If the arr consists of more than one argument, then it is an array of
	// independent strings. The first step is to join the entire argument into one
	// string
	initString := strings.Join(arr, " ")
	// split initString
	strArr := strings.Split(initString, "")
	// create a slice to append the characters in strArr in inverse order
	finalSlc := make([]string, 0)
	// starting an inverse loop
	for i := len(strArr) - 1; i >= 0; i-- {
		finalSlc = append(finalSlc, strArr[i])
	}
	// joining the inverted loop and set to final String
	finalString = strings.Join(finalSlc, "")
	return
}

func main() {
	args := os.Args
	// test args for length. len(args) should be >= 2
	if len(args) >= 2 {
		// submit the argument to reverseString()
		reversedString := reverseString(args[1:])
		// print out the counted characters
		fmt.Println(reversedString)
		// if len(args) != 2, inform the user.
	} else {
		fmt.Println("No strings supplied! Please run the program with at least one string supplied as an argument.")
	}
}
```

---

## Question 96

Question:

Write a program that accepts a string as a series of arguemnts from the CLI and prints the characters that have even indexes. For this exercise, accept only one argument supplied from the CLI. If more are supplied, ignore them.

Example:

1. If the following string is given as input to the program: H1e2l3l4o5w6o7r8l9d;
1. Then, the output of the program should be: Helloworld.

Solution:

```golang
package main

import (
	"fmt"
	"os"
	"strings"
)

// func that takes myStr string, filters out all elements with an odd-numbered index
//and returns evenStr string.
func filterString(myStr string) (evenStr string) {
	strSlc := make([]string, 0)
	myStrArr := strings.Split(myStr, "")
	for idx, v := range myStrArr {
		if idx % 2 == 0 {
			strSlc = append(strSlc, v)
		}
	}
	evenStr = strings.Join(strSlc, "")
	return
}

func main() {
	args := os.Args
	// test args for length. len(args) should be >= 2
	if len(args) >= 2 {
		// submit the argument to reverseString()
		filteredString := filterString(args[1])
		// print out the counted characters
		fmt.Println(filteredString)
		// if len(args) != 2, inform the user.
	} else {
		fmt.Println("No strings supplied! Please run the program with one string supplied as an argument.")
	}
}
```

---

## Question 97

Question:

Write a program that prints all permutations of [1,2,3]

Hints:

1. Solution adapted from: [Generate all permutations](https://yourbasic.org/golang/generate-permutation-slice-string/)

Solution:

```golang
package main

import "fmt"

// Perm calls f with each permutation of a.
func permF(a []int, f func([]int)) {
    perm(a, f, 0)
}

// Permute the values at index i to len(a)-1.
func perm(a []int, f func([]int), i int) {
    if i > len(a) {
        f(a)
		 return
    }
    perm(a, f, i+1)
    for j := i + 1; j < len(a); j++ {
        a[i], a[j] = a[j], a[i]
        perm(a, f, i+1)
        a[i], a[j] = a[j], a[i]
    }
}

func main() {
	arr := []int{1,2,3}
	permF(arr, func(a []int) {
		fmt.Println(arr)
	})
}
```

---

## Question 98

Question:

Write a program to solve this puzzle: We count 35 heads and 94 legs among the chickens and rabbits in a farm. How many rabbits and how many chickens do we have?

Hints:

1. This is a system of equations resolving like this:  
   i. chickens + rabbits = 35;  
   i. 2(chickens_legs) + 4(rabbits_legs) = 94.
1. To resolve run through every possible combination of the known total number of chickens and rabbits (35), counting the resultant legs every time to see if which combination of chickens and rabbits resolves in 94 legs.

Solution:

```golang
package main

import "fmt"

// func that takes two ints and outputs the answer as a string
func solve(nHeads, nLegs int) (sol string) {
	// creating the variable to test for 4 legs (the rabbit)
	var j int
	// starting the loop from 0 to the total number of heads
	for i := 0; i <= nHeads; i++ {
		// j to heads minus the current i
		j = nHeads - i
		// if adding (current i * 2) to (current j * 4) == number of legs,
		// we have a solution
		if (2 * i) + (4 * j) == nLegs {
			// generating a string with the solution
			sol = fmt.Sprintf("Chickens: %v, Rabbits: %v", i, j)
			return
		} else {
			// no solutions were found:
			sol = "No solution found!"
		}
	}
	return
}

func main() {
	nHeads := 35
	nLegs := 94
	solution := solve(nHeads,nLegs)
	fmt.Println(solution)
}
```

---

## Question 99

```golang

```

---

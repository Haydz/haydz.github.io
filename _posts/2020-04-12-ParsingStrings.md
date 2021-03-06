---
layout: posts
title: "Golang Parsing Strings"
---

I have been working with Golang strings and how to manipulate them. Working from other blogs posts I've found. When I sit down to code, I seem to forget everything from the previous session. This post is to be a cheat sheet for myself on string manipulation.

**References Can be found here**
* https://medium.com/@TobiasSchmidt89/effective-text-parsing-in-golang-163d13784288
* https://golangcode.com/writing-to-file/
* https://medium.com/golangspec/in-depth-introduction-to-bufio-scanner-in-golang-55483bb689b4


## FILE with data being used
To give a practical application to this post, I have included a rudimentary SSH auth log I found from the internet (googles). I have repeated lines and changed data so it could be manipulated more.

Find it below
[SSH auth Log](/images/sshinvalid.txt)
Code to play with this auth log based on the below can be found here on  
[Github](https://github.com/Haydz/blackhatgo/blob/master/src/texto/ssh_cutgrepsort.go)

## Ingesting a file
So first off we need data to play with.  
We could work with a simple string like:

`testString := "a long string"`

But that is no fun.
### Opening a File
So this is how to open a file & check for errors:
{%highlight go linenos %}
file, err := os.Open("sshinvalid.txt")
if err != nil {
	fmt.Println("opening file error", err)
}

{% endhighlight %}


### Reading a file
If the file is open, we will now want to read the file.

Use the scanner package:
> Package scanner provides a scanner and tokenizer for UTF-8-encoded text. It takes an io.Reader providing the source, which then can be tokenized through repeated calls to the Scan function. For compatibility with existing tools, the NUL character is not allowed.

In short: it scans UTF-8-encoded text

Need to read the file and split it (file is from the above example)

{%highlight go linenos %}
scanner := bufio.NewScanner(file)
scanner.Split(bufio.ScanLines)
{% endhighlight %}


### Reading line by line + Adding to an array
Generally the data needs to be stored into a variable so that it can be manipulated.
Create a string slice to place the data in, then loop through each line.

`scanner.Scan()` holds the Boolean of true or false if there is text
`scanner.Text()` holds the data we want to manipulate

Create a string slice to place the data in, then loop through each line of `Scanner.Text()` 

{%highlight go linenos %}
var txtlines []string

for scanner.Scan() {
	txtlines = append(txtlines, scanner.Text())
}

{% endhighlight %}


### Closing file
Once placing the data into a variable, we can close the file.  
I prefer to store data into a variable because it is easier for me to read. You are welcome to edit the data within the `for scann.Scan()` loop directly instead of storing it into a variable.


{%highlight go linenos %}
file.Close
{% endhighlight %}


### Code up to this point:
{%highlight go linenos %}
func main() {

	file, err := os.Open("sshinvalid.txt")
	if err != nil {
		fmt.Println("opening file error", err)
	}

	scanner := bufio.NewScanner(file)
	scanner.Split(bufio.ScanLines)
	var txtlines []string

	for scanner.Scan() {
		txtlines = append(txtlines, scanner.Text())
	}
	file.Close()
{% endhighlight %}


## What has been done so far  
* Opening a file
* reading the data in line by line
* storing the lines into an variable (slice)
* closing the file



## Manipulating Data

### Finding a value in string
To search through a string for a value, the `strings.Contains()` function is used.

`scanner.Text(), "word"` is how the syntax would be for using the Scan.

Since we have data in a slice, we will have to loop through it.

Example slice, which we loop through to test if `string` is in a string.
{%highlight go linenos %}
	testSlice:= []string{"the bbq", "the string has", "not much at all"}
	for _, value := range testSlice{
	fmt.Println(strings.Contains(value,"string"))
	}
{% endhighlight %}
 
 The Go Playground code to see live:  
* https://play.golang.org/p/D2nzknlclvH

To print the line, an IF ELSE statement can be used:
{%highlight go linenos %}
if strings.Contains(value, "string") == true {
			fmt.Println(value)
		}
{% endhighlight %}

### Separating via whitespace
#### Similar to linux: cut -d " " 

To separate a string via white space (words) use `strings.Fields()` function.
Syntax being : `strings.Fields(value)`

Using the the first value from testSlice: `testSlice[0]`:
{%highlight go linenos %}
wordBroken := strings.Fields(testSlice[0])
{% endhighlight %}
Using testSlice from before, but looping through it
{%highlight go linenos %}

for _, value := range testSlice  {
		wordBreakDown := strings.Fields(value)
		fmt.Println("==breaking sentence into words==")
		for _, value := range wordBreakDown {
			fmt.Println(value)
		}

	}
{% endhighlight %}

[The Go Playground code](https://play.golang.org/p/wyVKZg4A9g4)
The output for this is below:  
![](/images/GolangString/image_1.png)


### Separating by a delimiter
I definitely had to research this.

To separate by something other than a space, use the `strings.FieldFunc()`. Which comes in the format of
`func FieldsFunc(s string, f func(rune) bool) []string`

The example given is [from](https://golang.org/pkg/strings/#FieldsFunc):
> package main
>
import (
	"fmt"
	"strings"
	"unicode"
)
>
func main() {
	f := func(c rune) bool {
		return !unicode.IsLetter(c) && !unicode.IsNumber(c)
	}
	fmt.Printf("Fields are: %q", strings.FieldsFunc("  foo1;bar2,baz3...", f))
}


This is really difficult to understand.  
It is easier to understand this function as giving it a a second parameter of a function that returns a bool value (true or false). Another way, is a function that confirms true or false if a separator is in the stings. (least that is how I simplify it.) This function is within the function.

So cutting a comma from `testSlice:= "the bbq, the string has, not much at all"` would look like:

{%highlight go linenos %}
	testSlice := "the bbq, the string has, not much at all"

	cuttingByTwo := strings.FieldsFunc(testSlice, func(r rune) bool {
		if r == ',' {
			return true
		}
		return false
	})
	fmt.Println(cuttingByTwo)
{% endhighlight %}

Which outputs:


![](/images/GolangString/image_2.png)

[The Go Playground code](https://play.golang.org/p/qXqlRJ_pJ8Q)



### Separate by 2 delimiters (or more)
The process is the same as one delimiter that is not space, you just add an OR statement with the 2nd delimiter.

The example string will be: `testSlice:= "we want just the port number: [8080]"`
{%highlight go linenos %}
testSlice:= "we want just the port number: [8080]"

	cuttingByTwo := strings.FieldsFunc(testSlice, func(r rune) bool {
		if r == '[' || r == ']' {
			return true
		}
		return false
	})
	fmt.Println(cuttingByTwo[1])
{% endhighlight %}

[The Go Playground](https://play.golang.org/p/njUEWhAADhA) code	


To do this via the command line you would do:

`echo "we want just the port number: [8080]" | cut -d "[" -f2 | cut -d "]" -f1 8080`

	
	
Hope this helps with parsing strings.
	

	
	





 



























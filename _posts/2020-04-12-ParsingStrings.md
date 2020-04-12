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

`scanner.Scan()` holds the boolean of true or false if there is text
`scanner.Text()` holds the data we want to manipular

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
Using testSlice from before, but looping through itr
{%highlight go linenos %}

for _, value := range testSlice  {
		wordBreakDown := strings.Fields(value)
		fmt.Println("==breaking sentence into words==")
		for _, value := range wordBreakDown {
			fmt.Println(value)
		}

	}
{% endhighlight %}




THIS IS for value
To separate a string by a delimeter use `strings.FieldsFunc` function.
Syntacx being



 



























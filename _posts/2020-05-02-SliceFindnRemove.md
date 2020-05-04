---
layout: posts
title: "Slice Find & Remove Cheat Sheet"
---

This post is a cheat sheet for removing values from a Slice (technically creating a new slice).

Use case:
* Allow 1 or more options, as an option is chosen it no longer becomes available as an option to choose


The code right here is the use case listed above used in one of my programs..
{%highlight go linenos %}
package main

import (
	"fmt"
	"strings"
	"bufio"
	"os"
)

func remove(s []string, i int) []string {
    s[len(s)-1], s[i] = s[i], s[len(s)-1]
    return s[:len(s)-1]
}

func Find(a []string, x string) int {
	for i, n := range a {
		if x == n {
			return i
		}
	}
	return len(a)
}

func main() {
    //slice to show options chosen
	var dataToAdd []string
	//creating reader for reading in input
	reader := bufio.NewReader(os.Stdin)
	//fields to select
	fieldsToChoose := []string{"created", "updated", "summary", "status", "priority", "assignee"}
	//unending loop until "ENTER" is pressed.
	for x := 0; x < 2; {
		fmt.Println("Please Enter Fields to print out")
		fmt.Println(fieldsToChoose)
		
		value, _ := reader.ReadString('\n')
		value = strings.TrimSpace(value)

		if value == "" {
			break
		}
		//remove chosen field from options list
		fieldsToChoose = remove(fieldsToChoose, Find(fieldsToChoose, value))
		//append option to a list of chosen options
		dataToAdd = append(dataToAdd, value)
		

	}
	fmt.Println(dataToAdd)
	
}



{% endhighlight %}

# Slice General  
Slices are a key data type in Go. Each key is a number and the value can be arbitrary.

A slice can be defined like:


{%highlight go linenos %}
testSlice := []string{"created", "updated", "summary", "status"} "priority", "assignee"}
{% endhighlight %}


Choosing a value from the Slice can be done with the integer location:

{%highlight go linenos %}
fmt.Println(testSlice[0])
{% endhighlight %}

# Removing a value
Removing a value is not as easy as points to the location and giving it a blank value. 

This will not work as intended, the BLANK value will still be there.

{%highlight go linenos %}
	testSlice [0] = ""
	fmt.Println(testSlice[0])
{% endhighlight %}

## The correct way
This is a two step process.

1) Identifying the location of value you want to remove. 
2) Creating a new slice without that value

A way I found on [stackoverflow](https://stackoverflow.com/questions/37334119/how-to-delete-an-element-from-a-slice-in-golang) was using a slice of integers.

The idea is to swap the value you want removed with the last value in the slice and then create a new slice 1 size shorter. Thus dropping the last slice.

The example given is:  
{%highlight go linenos %}
func remove(s []int, i int) []int {
    s[len(s)-1], s[i] = s[i], s[len(s)-1]
    return s[:len(s)-1]
}
{% endhighlight %}
[The Go Playground](https://play.golang.org/p/cssHAwjAcak) code here

This works fine on supplying the location of the value. Hence why Step 1 is required.


### Finding the location in the slice you want to remove
This finds the location of a string value within a slice:

{%highlight go linenos %}
func Find(a []string, x string) int {
	for i, n := range a {
		if x == n {
			return i
		}
	}
	return len(a)
}
{% endhighlight %}

Pass the function the slice you want to use and the string value you want to find and it will print its int position in the slice. such as:
![](/images/slices1/image_1.png)

[The Go Playground](https://play.golang.org/p/sGGkl6W8Yxo) code to try.

With the location identified we can pass it to the remove function above.


### Finding and Removing    
Lets work with a slice with strings:
testSlice := []string{"apple", "banana", "orange"}

The remove function above has to be converted to allow strings. That means accepting strings and returning a string. It looks like:

{%highlight go linenos %}
func remove(s []string, i int) []string{
	s[i] = s[len(s)-1]
	fmt.Println("test",s[i])
	// We do not need to put s[i] at the end, as it will be discarded anyway
	return s[:len(s)-1]
}
{% endhighlight %}


So with the testSlice slice we will remove the string "banana", which from above is the int location 1 in the slice.

{%highlight go linenos %}
func main() {
	testSlice := []string{"apple", "banana", "orange"}
	fmt.Println("Location of banana within testSlice")
	fmt.Println(Find(testSlice , "banana"))
}
{% endhighlight %}

We pass the 1 integer to the remove variable and we will have a new slice without the string banana.

This works here:
[The Go Playground](https://play.golang.org/p/oPuGwmaZff6)
![](/images/slices1/image_2.png)

We can combine these together like so:

{%highlight go linenos %}
	testSlice := []string{"apple", "banana", "orange"}
	fmt.Println(remove(testSlice , Find(testSlice ,"banana")))
{% endhighlight %}

![](/images/slices1/image_3.png)


# All the code together
{%highlight go linenos %}
package main

import (
	"fmt"
)

func remove(s []string, i int) []string {
    s[len(s)-1], s[i] = s[i], s[len(s)-1]
    return s[:len(s)-1]
}

func Find(a []string, x string) int {
	for i, n := range a {
		if x == n {
			return i
		}
	}
	return len(a)
}


func main() {

	
	
	testSlice := []string{"apple", "banana", "orange"}
	fmt.Println("Find banana location and remove from slice (create new slice)")
	fmt.Println(remove(testSlice , Find(testSlice ,"banana")))
	
	
}

{% endhighlight %}
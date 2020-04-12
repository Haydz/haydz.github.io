---
layout: posts
title: "Golang Parsing Strings"
---

# Parsing Strings in Golang

I have been working with Golang strings and how to manipulate them. Working from other blogs posts I've found. When I sit down to code, I seem to forget everything from the previous session. This post is to be a cheat sheet for myself on string manipulation.

**References Can be found here**
* https://medium.com/@TobiasSchmidt89/effective-text-parsing-in-golang-163d13784288
* https://golangcode.com/writing-to-file/
* https://medium.com/golangspec/in-depth-introduction-to-bufio-scanner-in-golang-55483bb689b4



## Ingesting a file
So first off we need data to play with.  
We could work with a simple string like:

`testString := "a long string"`

But that is no fun.

So this is how to open a file & check for errors:
{%highlight go linenos %}
file, err := os.Open("sshinvalid.txt")
if err != nil {
	fmt.Println("opening file error", err)
}

{% endhighlight %}












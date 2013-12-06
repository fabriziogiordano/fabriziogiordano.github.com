---
layout: post
title: Golang find smallest number in array
excerpt: Golang find smallest number in array testing syntax highlighter
---


```
package main

import "fmt"

func main() {
	x := []uint {
		48,94,23,
		3,45,54,
	}

	min := x[0]

	for _, value := range x {
		if value < min {
			min = value
		}
	}
	fmt.Println(min)
}
```
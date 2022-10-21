---
title: "Project Euler [Draft]"
excerpt: "Implementing the same algorithm in Python, Swift and Go."
last_modified_at: 2023-03-17T17:15:00-03:00
tags: 
  - go
---

```go
package main

import "fmt"

func main() {
	i := 0
	s := 0
	for {
		if i >= 1000 {
			break
		}
		if (i%3 == 0) || (i%5 == 0) {
			s += i
		}
		i++
	}
	fmt.Println(s)
}
```




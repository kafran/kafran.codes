---
title: "Swift's OptionSet: an awesome bitwise operation use-case"
excerpt: "I have been avoiding that part of the book which talks about bitwise operators until I saw Swift's OptionSet on iOS frameworks."
date: 2022-11-16 13:00:00 -0300
image: "/assets/images/posts/2022-11-15-swift-optionset/coqueiro.jpeg"
tags: 
  - swift
---

I don't have a Computer Science degree. I didn't have the opportunity to mess around with complex computer science topics in college. Nonetheless, I always had the curiosity to [understand how computers work](https://www.edx.org/course/introduction-computer-science-harvardx-cs50x), thus bits and bytes and binaries weren't new to me. Even so, for a while, I have avoided reading [that part of the book that talks about bitwise operators](https://docs.swift.org/swift-book/LanguageGuide/AdvancedOperators.html) when learning a new language. Some books even warn you: "You don't need this unless you are doing really complex stuff". I could never understand the real utility of using bitwise operators as I never had to do bit twiddling myself for the kind of problems I have been solving so far.

But since I bought my first Raspberry Pi board in September 2012 I have been fascinated by IoT and embedded systems. Especially with all these new technologies and powerful microcontrollers that have been popping out in the market since then. Eventually, bitwise operation was a topic that ended up on my table again. And when I finally got it, it was mind-blowing.

<figure style="width: 500px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/posts/2022-11-15-swift-optionset/microbit.jpeg" alt="BBC Microbit board">
  <figcaption>Can you believe this little guy has only 128KB of memory.</figcaption>
</figure>

The iPhone in your pocket probably has more processing power and memory than a satellite fleeing around the globe. So, bitwise operators are not a great deal anymore and someone can get away with not knowing them, as it was for me. But when working in a constrained environment like the Microbit computer above you start to get worried about how efficient your code can be in terms of memory.

## Why use bitwise operators?

As the name suggests, bitwise operators works on the individual bits.

> Bitwise operators enable you to manipulate the individual raw data bits within a data structure. They’re often used in low-level programming, such as graphics programming and device driver creation. Bitwise operators can also be useful when you work with raw data from external sources, such as encoding and decoding data for communication over a custom protocol.

<cite>The Swift Programming Language Book</cite>
{: .small}

I won't go into the details of how these operators work as [The Swift Programming Language Book](https://docs.swift.org/swift-book/LanguageGuide/AdvancedOperators.html#ID29) do a much better job. I will try to retain myself on an interesting use case so we can move on to what interest: Swift's OptionSet.

Imagine you want to store a boolean value. How much memory would it take? The smallest amount of space a variable can take is 1 byte. The reason for this is that it is the smallest unit of addressable space that a CPU can reference. So, even a boolean that only has the values of true or false and therefore should only take up 1 bit still uses a full byte and has the remaining 7 bits padded out. This is not good if you are trying to save memory.

```swift
let bool = true  // 0b0000_0001
var bool = false // 0b0000_0000
```

Most applications have multiple flags. Think about the Unix file permissions, for example. A user can have permission to read, write, execute, or all at once. When you `chmod 777 file` from your terminal, this is exactly what you're doing, you are turning flags on and off. To make the most out of the available space programmers would combine multiple flags into a single byte allowing them to store up to 8 different boolean values. So, in one byte you can store up to 8 boolean values.

```swift
let x: UInt8 = 0b0000_0001 // execute - in base 10 this 1
let w: UInt8 = 0b0000_0010 // write - in base 10 this is 2
let r: UInt8 = 0b0000_0100 // read - in base 10 this is 4

let rwx: UInt8 = 0b0000_0111 // read, write, execute - in base 10 this is 7
```

That's why the flag to set permission to read, write and execute is 7. Because the binary integer `0b0000_0111` is the decimal integer `7`. However, to manipulate these individual bits (to turn them on and off), we need some way to identify the specific bits we want to manipulate. Unfortunately, the bitwise operators don’t know how to work with bit positions. Instead, they work with bit masks.

### Bit masks 

A bit mask is a predefined set of bits that are used to select which specific bits will be modified by subsequent operations. In the example above we set 3 masks, one for read, one for write, and another for execute. So, continuing with the example, suppose we want to set the permission to read and write:

```swift
// Masks
let x: UInt8 = 0b0000_0001 // execute
let w: UInt8 = 0b0000_0010 // write
let r: UInt8 = 0b0000_0100 // read

// To set (turn on) a bit we use the bitwise operator OR (|)
let rw: UInt8 = r | w // 0b0000_0110 - in base 10 this is 6
let rwx: UInt8 = r | w | x // 0b0000_0111 - in base 10 this is 7
```
For more detail on all other operators and how these operators work read the excellent [Swift Programming Language Book](https://docs.swift.org/swift-book/LanguageGuide/AdvancedOperators.html#ID29).

But, wait a minute, this whole thesis started promising memory efficiency. The above example doesn’t actually save any memory. 3 booleans would normally take 3 bytes. But the above example uses 4 bytes (3 bytes to define the bit masks, and 1 byte for the flag itself)!

Think about scale. Bit flags make the most sense when you have many identical flag variables. In the example above, we are dealing with one permission set only: the user permissions (the owner permissions, in Unix terms). Now imagine that besides the user you want to set the permissions for the group and others. Or worst, imagine setting the permission for 100 users. Instead of having one permission set (the owner), now you have 100. If you use 3 Booleans per permission set (one for each possible state), you’d use 300 bytes of memory. With bit flags, you’d use 3 bytes for the bit masks, and 100 bytes for the bit flag variables, for a total of 108 bytes of memory -- approximately 3 times less memory.

Ok but this is all about Swift and iOS development, why bother to save a few bytes of memory, right? Probably your use case won't scale to tens of thousands or even millions of similar objects to be worth the added complexity.

Well, there’s another case where bit flags and bit masks can make sense, and UIKit and SwiftUI make good use of it. Imagine you have a function that can take any combination of 8 or more different options – for the sake of convenience and simplicity I will keep working on an 8-bit base. One way to write that function would be to use 8 individual Boolean parameters:

```swift
func someFunc(
    option1: Bool,
    option2: Bool,
    option3: Bool,
    option4: Bool,
    option5: Bool,
    option6: Bool,
    option7: Bool,
    option8: Bool,
) {}
```
Crazy, right? Now imagine you want to call this function with options 2 and 7 set to `true`:

```swift
someFunc(
    option1: false,
    option2: true,
    option3: false,
    option4: false,
    option5: false,
    option6: false,
    option7: true,
    option8: false,
)
```
Well, thanks to [Swift's argument label](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID166) this doesn't sacrifice readability but I hope you understand the mess.

## Swift's OptionSet

Swift's OptionSet solves exactly this problem. Take for example the `.padding()` modifier on SwiftUI – used to add a specified amount of padding to one or more edges of the view. The `.padding()` modifier and many other SwiftUI and UIKit functions receive an OptionSet. When you apply a `.padding()` with `[.top, .bottom, .leading, .trailing]` you are not passing an Array of Enum, you are passing an OptionSet.

Option sets all conform to RawRepresentable by inheritance using the OptionSet protocol. The raw value of an option set instance stores the instance’s bitfield. The raw value must be of a type that conforms to the FixedWidthInteger protocol, such as UInt8 or Int. In turn, the FixedWidthInteger protocol adds binary bitwise operations, bit shifts, and overflow handling to the operations supported by the BinaryInteger protocol.

Continuing the example above, we could define an OptionSet:

```swift
struct MyEightOptions: OptionSet {
    let rawValue: UInt8 // Stores our flags

    static let option1 = MyEightOptions(rawValue: 0b0000_0001) // 1
    static let option2 = MyEightOptions(rawValue: 0b0000_0010) // 2
    static let option3 = MyEightOptions(rawValue: 0b0000_0100) // 4
    static let option4 = MyEightOptions(rawValue: 0b0000_1000) // 8
    static let option5 = MyEightOptions(rawValue: 0b0001_0000) // 16
    static let option6 = MyEightOptions(rawValue: 0b0010_0000) // 32
    static let option7 = MyEightOptions(rawValue: 0b0100_0000) // 64
    static let option8 = MyEightOptions(rawValue: 0b1000_0000) // 128

    static let all: MyEightOptions = [
        .option1,
        .option2,
        .option3,
        .option4,
        .option5,
        .option6,
        .option7,
        .option8,
    ]
}
```

And then have it in our function instead of all those parameters:

```swift
func someFunc(options: MyEightOptions) {
    if options.contains([.option2, .option7]) {
        print("\(options)") 
    }
} 

someFunc(options: [.option2, .option7]) // MyEightOptions(rawValue: 66)
```
Much cleaner, right? Also, we have context now. In the example above MyEightOptions(rawValue: 66) stores de integer 66 wich is the binary integer `0b0010_0100` with option2 and option7 turned on.

I hope this article has helped you to understand these SwiftUI and UIKit constructs and how OptionSet works behind the scenes.

## About the image

This is close to my house in the city of João Pessoa, in the Northeast of Brazil. I love this area. A courious fact, aparently [coconut trees are more dangerous than sharks](https://en.wikipedia.org/wiki/Death_by_coconut).

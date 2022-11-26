---
title: "SwiftUI: Understanding Core Data"
excerpt: "Core Data is an object graph and persistence framework available on iOS since iPhone SDK 3.0 and it's starting to show its age."
date: 2022-10-22 15:40:00 -0300
image: "/assets/images/posts/2022-10-22-understanding-core-data/caju.jpeg"
tags: 
  - swiftui
  - ios
  - core data
---

When I started on mobile development I tried the three main flavors of it: Android Native, iOS Native and Flutter. Besides being an Apple costumer myself, the developer experience is one of [the reasons why I decided to dive into iOS Native development](https://kafran.codes/why-ios-development/). Apple delivers solutions to complex problems throughout it's rich ecosystem of frameworks and APIs so developers can focus on what matters: solve people's problems instead of computers' problems.

Core Data is an object graph and persistence framework amongst the list of frameworks provided by Apple. It's available on iOS since iPhone SDK 3.0. Yep, it's really old and mature, which in software usually translates to "stability". But equally, it's starting to show its age when it comes to integrating the framework into new ones like SwiftUI.

Core Data has undoubtedly contributions to give to the [hot topic around SwiftUI and MVVM](https://developer.apple.com/forums/thread/699003) since the introduction of a new property wrapper to integrate the framework into SwiftUI: `@FetchRequest`.

<figure style="width: 148px; height: 320px;" class="align-right">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/posts/2022-10-22-understanding-core-data/coredata.gif" alt="A Core Data sample app">
  <figcaption>Core Data sample app.</figcaption>
</figure>
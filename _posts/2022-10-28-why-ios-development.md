---
title: "Why I decided to become an iOS Developer"
excerpt: "I got bored of working with Data Science and decided to try to make mobile apps. But why iOS?"
last_modified_at: 2022-10-22T15:40:00-03:00
image: "/assets/images/drawings/the-software-smith/the-software-smith.jpeg"
tags: 
  - ios
---

My background is not in Computer Science. I hold a bachelor's degree in Business Administration and a master's degree in Public Policy Management. So I've been more on the management side for the majority of my career. For the last ten years I have been working for the Brazilian Federal Government, firstly as business manager, then data analyst and finally data engineer. I didn't seek this path but the job made me search for different tools to solve different problems and this brought me into the software development field.

For a while I used to excel in Excel, but the need to crush more and more data every day – and to better communicate my ideas – brought me to tools like R and Python. Eventually, the government's low maturity level to working with data showed up and I had to become a data engineer as well. Soon I would have to be concerned about performance, data structure, and algorithms. How to sort all this data, how to read a big file on a limited amount of memory, how to process all this raw data and bulk load it into a SQL Server instance? Not only that but I had to start to think about clean code and design patterns, otherwise, I would drown in all that spaghetti code. And that is how I ended up interested in software engineering.

<figure style="width: 400px" class="align-right">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/posts/2022-10-28-why-ios-development/storytelling.jpg" alt="Book storytelling with data by Cole NussBaumer Knaflic">
  <figcaption>For a while this was my bedside book.</figcaption>
</figure>

And how did I end up leaning to become an iOS developer? Well, firstly I got bored of all this data field. I enjoyed the software development part of the job and I couldn't envision in the mid-term how I could become a better software engineer doing what I have been doing. Secondly, the backend field is too abstract for me. I like the idea of working close to the user experience, seeing the little shiny things, writing some code and seeing a button, and clicking the button and seeing some response. Also, it's easier to explain to friends "I make apps" instead of "I make REST APIs" when they ask what I do for a living :).

So, in 2020, I decided to try the mobile development world. I tried the three major technologies: Android Native, iOS Native, and Flutter. And there were reasons to try these three.

Android Native
: Apple devices are expensive, thus the Android market in Brazil is huge. According to websites like Statista and Statcounter Apple accounts for less than 15% of Brazilian market. Thus between 2020 and 2021, I took some classes in Android development and started my mobile development career on Android. As someone mostly used to languages like Python and R, I loved the Kotlin language. But, being an iPhone/Macbook user myself it was a little bit frustrating not to be able to use what I have been doing, and this is important to keep motivation while learning.

Flutter (or, why not React Native?)
: After learning about Android development, in 2020 there was a new kid in the playground gaining traction really quickly. And like everybody changing careers in the tech industry, I had to try the shiny new thing myself. Also, it would allow me to run the app on both Android and iOS. Flutter is an amazing technology to build "cross-platform" apps for Windows, Linux, MacOS, iOS and Android. Flutter was different from React Native as it draws its own components on the screen instead of bridging to the native ones. This brings whole new possibilities for beautiful animations and amazing customization, without sacrificing performance. Moving from Kotlin to Dart – the language used by the Flutter framework – felt initially weird. So many features were missing, but the language is evolving with the framework and I even started to enjoy it.

iOS Native
: After a while on Android and Flutter, a few things still didn't feel right. The developer experience on those two platforms wasn't great, but what really drove me toward iOS development – besides being an Apple client myself – was the fact that Apple managed to create a true software business with a rich ecosystem. Even to become a developer for Apple's platforms the developer needs to pay for a subscription – I won't get into the merits of whether this is right or not, or if it's cheap or not – but Apple tries to deliver some value to the developer with a better tool chain and support than the competition. Thus, Apple's users are used to quality and amazing software and they are willing to pay for it. And last but not least, Swift is awesome.

## The Apple ecosystem as a business

The main reason that made me want to deepen my knowledge and skills in iOS development on my journey to become a mobile developer was Apple's business model. Apple created a solid software development market with a rich app store. Apple's business model is not centered on ads and thus the users are inclined to pay for the apps. 

Meanwhile, Android users are used to shitty apps full of ads. I remember when I first changed from an Android phone to an iPhone. My family and friends warned me in advance "you know you gonna have to pay for the apps, right?". Coincidence, or not, apps in the App Store supported by ads are usually made with cross-platform technologies like Flutter or React Native.

You don't see an Android indie dev community as strong as the iOS' one. The reality is: It's more difficult to make money on Android than on iOS when the product is the app itself. I had no idea if I would even find a job to work making mobile apps, so thinking about entrepreneurship and making my own apps worked as another motivational trigger.

## The Developer Experience

The Apple's development ecosystem free the developer from thinking about architecture and how to solve common problems to focus on the product and the user experience. [Until recently the Android documentation was very unopinionated](https://developer.android.com/topic/architecture#recommended-app-arch) about which architecture the developers should follow or the "right" way and best practices to build an app. Meanwhile, [Apple always had a strong opinion and tried to lead the way on how an app should be organized](https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/MVC.html). Apple gives the developer tools and frameworks to build the best apps they can: Swift Charts, Core Data, SpriteKit, WeatherKit, to name a few. Under Android and Flutter developers heavely relies on third party libraries to solve the same problems, which can be frustrating, specially if you are alone to think about every aspect of your product.

---
title: "Why I decided to become an iOS Developer"
excerpt: "I got bored with working in the Data field (Analytics/Science/Engineering) and decided to make mobile apps. But why iOS?"
date: 2022-10-28 15:40:00 -0300
image: "/assets/images/drawings/the-software-smith/the-software-smith.jpeg"
tags: 
  - ios
  - career
---

My background is not in Computer Science. I hold a bachelor's degree in Business Administration and a master's degree in Public Policy Management. So I've been more on the management side for the majority of my career. For the last ten years I have been working for the Brazilian Federal Government, firstly as business manager, then data analyst and finally data engineer. I didn't seek this path but the job made me search for different tools to solve different problems and this brought me into the software development field.

For a while I used to excel in Excel, but the need to crush more and more data every day – and to better communicate my ideas – brought me to tools like R and Python. Eventually, the government's low maturity level to working with data showed up and I had to become a data engineer as well. Soon I would have to be concerned about performance, data structure, and algorithms. How to sort all this data, how to read a big file on a limited amount of memory, how to process all this raw data and bulk load it into a SQL Server instance? Not only that but I had to start to think about clean code and design patterns, otherwise, I would drown in all that spaghetti code. And that is how I ended up interested in software engineering.

<figure style="width: 400px" class="align-right">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/posts/2022-10-28-why-ios-development/storytelling.jpg" alt="Book storytelling with data by Cole NussBaumer Knaflic">
  <figcaption>For a while this was my bedside book.</figcaption>
</figure>

But I got bored with all this data field. I enjoyed the software development part of the job, but the rest of it was just boring and I couldn't envision in the mid-term how I could become a better software engineer doing what I had been doing. So I started to look for something else. I like the idea of working close to the user experience, seeing the little shiny things, writing some code and seeing a button, and clicking the button and seeing some response. Thus, mobile development seemed to be the right path to follow.

In 2019, I decided to try the mobile development world. I tried the three major technologies available: Android Native, Flutter, and iOS Native, in this order.

Android Native
: Apple devices are expensive, thus the Android market in Brazil is huge. According to websites like Statista and Statcounter Apple accounts for less than 15% of the Brazilian market. So, It seemed reasonable to start with Android. Thus, I took some classes in Android development and started my mobile development career on Android. As someone mostly used to Python and R, I loved the Kotlin language. But, being an iPhone/Macbook user myself it was a little bit frustrating not to be able to use what I had been doing, and this is an important motivation keeper while learning.

Flutter (or, why not React Native?)
: There was a new kid in the block gaining traction really quickly. And like everybody changing careers in the tech industry, I had to try the shiny new thing myself. Since I had this wish to develop my own products, it would also allow me to run the app on both Android and iOS. Flutter is an amazing technology to build "cross-platform" apps for Windows, Linux, MacOS, iOS, and Android. Flutter is different from React Native as it draws its own components on the screen instead of bridging to the native ones. This brings whole new possibilities for beautiful animations and amazing customization, without sacrificing performance. Moving from Kotlin to Dart – the language used by the Flutter framework – felt initially weird. So many features were missing, but the language is evolving with the framework and I even started to enjoy it.

iOS Native
: After a while on Android and Flutter, a few things still didn't feel right. The developer experience on those two platforms wasn't great. Well, people seem to love Flutter for its hot reload – especially Android developers – but SwiftUI drives the same amount of amusement without having to deal with all the external dependencies to build a full-featured app. But what drove me toward iOS development – besides being an Apple client myself – was the fact that Apple managed to create a true software business with a rich ecosystem and users accustomed to beautiful and useful apps and willing to pay for them. Apple clearly had a business model in place. I had no idea if I would even get a job as a mobile developer and since I had this wish to develop my own products,  investing my time to be knowledgeable on Apple's platforms made sense to me.

## The Apple ecosystem as a business

The main reason that made me want to deepen my knowledge and skills in iOS development on my journey to become a mobile developer was Apple's business model. Apple created a solid software development market with a rich app store. Apple's business model is not centered on ads and thus the users are inclined to pay for the apps. 

Meanwhile, Android users are used to shitty apps full of ads. I remember when I first changed from an Android phone to an iPhone. My family and friends warned me in advance "you know you gonna have to pay for the apps, right?". Coincidence, or not, apps in the App Store supported by ads are usually made with cross-platform technologies like Flutter or React Native.

You don't see an Android indie dev community as strong as the iOS' one. The reality is: It's more difficult to make money on Android than on iOS when the product is the app itself. I had no idea if I would even find a job to work making mobile apps, so thinking about entrepreneurship and making my own apps worked as another motivational driver.

## The Developer Experience

Ok, this can drive hot discussions as developers tend to treat languages and tools as sports teams. Despite having my personal choices I always tried to keep the mindset of "the right tool for the right task". But I really enjoyed the developer experience on Apple's ecosystem. It's really friendly for newcomers. 

Don't get me wrong, iOS development is hard and complex, it can be daunting. The framework is huge, the Swift language is huge. But, so do Android and Flutter. The difference is Apple better stewards the ecosystem as a whole. For better or for worst Apple can get really opinionated about how things should be done. For example, [until recently the Android documentation was very unopinionated](https://developer.android.com/topic/architecture#recommended-app-arch) about which architecture the developers should follow or the "right" way and best practices to build an app. Meanwhile, [Apple has advocated for MVC since the beginning](https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/MVC.html). Another example is Apple introducing the Combine framework and the way state management is handled through SwiftUI. Meanwhile, the hot topic on Flutter is around which state management approaches should be used.

The amount of time I lost thinking about architecture, dependency injection, state management, etcetera, while learning Android and Flutter was humongous. Ok, it was amazing to learn about all this stuff, but I don't think they should be on the front door. I just want to build an app. A real one, full-featured, and which solves a problem. For newcomers like me, being free to think about the app and the problem it solves is a big step and I think this is why Apple's platforms have better apps than any other platform.

In episode [234: More Product. Less Architecture?](https://fragmentedpodcast.com/episodes/234/) of the Fragmented Podcast I felt personally represented. It's almost like Donn and Kaushik were talking about all the pain I suffered to learn Android and Flutter.

Also, with all the furor around Flutter – and cross-platform development in general – calming down it's starting to be clear that we are heading to a cross-platform same-ecosystem future. With SwiftUI, it was never been easier to deliver a seamless experience to the whole Apple ecosystem: Macs, iPhones, iPads, Watches, and TV. Maybe Flutter will have more value for developers inside the Android ecosystem than Apple's, with Android's components being integrated into the framework at a much faster pace. If you are not a bank or another industry in which your product is not the app itself, you are in a much better place if you stick with the native technologies.

Of course, Apple's ecosystem has its own flaws as well. Many developers criticize the same business model which brought me to it in the first place. Some frameworks, like Core Data, are starting to show their age, etcetera. But I think this is an amazing time to be starting as an iOS developer.

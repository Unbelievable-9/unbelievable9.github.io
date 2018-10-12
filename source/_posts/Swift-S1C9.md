---
title: Swift-S1C9
date: 2016-08-24 15:26:13
categories: Swift 基础
tags: Swift
---

## 读书笔记

这章就是传说中的 **迷之问号 ？感叹号 ！** 😂 😂 😂

<!--more-->

以来马特大神就拿自己开涮

`
But what if I become unemployed? Maybe I’ve won the lottery and want to give up work altogether (I wish!).
`

我只想说，我也想这么 Maybe 一次~

个人觉得，关于 Optionals 这种类型，重要的其实不在于语法本身，而在于去理解 Swift 为什么要提出这种策略。马特大神的纯文字总结首先附上

`
This means that if you are handling a non-optional type then you are guaranteed to have a value and don't need to worry about if there is a value or not. There always is one. Similarly, if you are using an optional type then you know you must handle the nil case. It takes away the ambiguity introduced by using sentinel values.
`

马特大神用一了一个盒子的比喻，来解释 Optionals 的内在原理。在讲盒子之前，马特大神又开始低调的秀他那丰富的知识面

**Schrödinger's cat**

可能你知道这个人是谁，但我只记得大学物理的某节课讲过这个哥们儿的一个方程，而我当时的状态不是在坐飞机也不是在坐火箭，我是在坐宇宙飞船 😩

但是这个哥们儿的猫是个什么情况？查资料后发现是个著名实验，聚精会神的看完介绍，分分觉得自己吃了没有文化的亏。

哎，还是努力读书吧 😶

- 关于盒子

  这个例子，不得不说是我看过介绍 Optionals 类型里面文章里面，最通俗易懂的方式了。其实就像马特大神所说，对一个种类型加上 ？了之后，其实就是给它套了一个盒子，盒子永远都在那里，你可以随时打开它（感叹号 ！），也可以随时查看他（直接引用）。

  至于为什么要这么做，这也是 Swift 强调类型安全的重要体现。当你加上这层盒子了之后，你就应该时刻警惕，它可能里面什么都没有，当没有这个盒子的时候，你完全不用担心，绝逼里面有值~

  这对于编写大型工程的时候非常有帮助，记得在写 Objective-C 代码的时候，时刻都在判读一个变量是否等于 nil，nil 也是许多 Bug 的源头。现在 Swift 有了 Optionals 和 普通变量的区分之后，编写代码时，不只是就是心中了然了，代码也能时刻提醒自己了。

- Mini-exercise

  ```swift
  import Foundation

  let myFavoriteSong: String?

  //More Than 10 Acutally...
  myFavoriteSong = nil
  ```

- Unwrapping

  关于 Force Unwrapping (直接使用 ！)，马特大神用了一个特别贴切的词语 **sparingly**，来形容使用它的频率，同时也说了到了不要像在 Objective-C 那样，每次都去判断 Optionals 是否为 nil。

  那么应该怎最才最安全同时又很简洁呢？

  第一种方法：

  **If Let Binding**

  是不是觉得很熟悉？！在学习 Control Flow 的那个 Chapter中，if let 的用法就在讲 case 语句的时候用到了，这里再次出现！

  这次更新的用法是，if let 关键字不只可以定义一个变量，还可以一次性定义多个变量，非常方便。

  关于原理马特大神也讲的很清楚了，这里就不再敖述。

- Mini-exercise

  **1.**

  ```swift
  import Foundation

  let myFavoriteSong: String? = "Lemuria"

  if let unwrappedMyFavoriteSong = myFavoriteSong {
      print("My favorite song is \(unwrappedMyFavoriteSong).")
  } else {
      print("I don't have a favorite song.")
  }
  ```

  `
  Console: My favorite song is Lemuria.
  `

  **2.**

  ```swift
  import Foundation

  let myFavoriteSong: String? = nil

  if let unwrappedMyFavoriteSong = myFavoriteSong {
      print("My favorite song is \(unwrappedMyFavoriteSong).")
  } else {
      print("I don't have a favorite song.")
  }
  ```

  `
  Console: I don't have a favorite song.
  `
- Nil coalescing

  这是马特大神推荐的第二种打开盒子的方法，更加简洁。

  改写 Mini-exercise 来作为示例：

  **1.**

  ```swift
  import Foundation

  let myFavoriteSong: String? = "Lemuria"

  let unwrappedMyFavoriteSong = myFavoriteSong ?? "I don't have a favorite song."

  print(unwrappedMyFavoriteSong)
  ```

  `
  Console: Lemuria
  `

  **2.**

  ```swift
  import Foundation

  let myFavoriteSong: String? = nil

  let unwrappedMyFavoriteSong = myFavoriteSong ?? "I don't have a favorite song."

  print(unwrappedMyFavoriteSong)
  ```

  `
  Console: I don't have a favorite song.
  `

  两种方法各有千秋，记住 if let 和 ?? 这两个东西就可以啦 😈

- Challenges

  **A**

  ```swift
  var age: Int = nil
  ```

  普通变量必须有值，不能为 nil ！

  **B C**

  ```swift
  import Foundation

  func divideIfWhole(value: Int, by divisor: Int) -> Int? {
      let result: Int?

      if value % divisor == 0 {
          result = value / divisor
      } else {
          result = nil
      }

      return result
  }

  //If Let Binding
  if let answer = divideIfWhole(10, by: 2) {
      print("Yep, it divides \(answer) times.")
  } else {
      print("Not divisible.")
  }

  //Console: Yep, it divides 5.

  //Nil Coalescing
  let answer = divideIfWhole(10, by: 3) ?? 0

  if answer != 0 {
      print("Yep, it divides \(answer) times.")
  } else {
      print("Not divisible.")
  }

  //Console: Not divisible.
  ```

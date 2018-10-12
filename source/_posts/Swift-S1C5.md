---
title: Swift-S1C5
date: 2016-08-17 14:38:40
tags: Swift
---

## 读书笔记

- If Else

  这个没什么特别的，马特一句话地点题

  `
  In other words, the order of your else- if conditions matters!
  `

  <!--more-->

  马特再用单词点题

  **Scope (作用域)**

  **Ternary Conditional Operator (三运算符)**

  真不是我懒，学过编程的，看懂标题就知道内容是啥了。。。

- Mini-exercise

  ```swift
  import UIKit

  let myAge = 25

  if myAge >= 13 && myAge <= 19 {
      print("You are a teenager. 😁")
  } else {
      print("You are not a teenager. 🙁")
  }
  ```

  马特你非跟 Teenager 过不去是么，还老让读者输入自己的真实年龄！

- Switch

  只有一句话，**喜大普奔!**

  `
  They work with any data type!
  `

  - Pattern Matching

    马特大神在讲 Switch 的时候秀了一手 **let-where** 语法的使用方法，本菜鸡第一次见到，觉得很是厉害。

    初步看来，这里存在隐式引用:

    ```swift
    let number = 10

    switch (number) {
    case let x where x % 2 == 0:
      print("Even")
    default:
      print("Odd")
    }
    ```

    这里第一个 case 里用 let 申明了一个 x 常量，并用 where 添加判断条件，但是 x 常量初始赋值并没有显式的体现，但是很好理解 x 的初始值肯定是等于 number (纯表面理解)。这里写下来作为记录，可能以后还会遇到。

    马特大神在后续的例子里，用 Switch 做引子，帮大家把 **Tuple Underscore Interpolation 和 let-where** 全部串起来给大家秀了一波，真是个好老师 👏

- Mini-exercise

  **1.**

  ```swift  
  import UIKit

  let age: Int = 25

  switch (age) {
  case let x where x >= 0 && x < 3:
      print("Infant")
  case let x where x >= 3 && x < 13:
      print("Child");
  case let x where x >= 13 && x < 20:
      print("Teenager")
  case let x where x >= 20 && x < 40:
      print("Adult")
  case let x where x >= 40 && x < 61:
      print("Middle Aged")
  case let x where x >= 61:
      print("Elderly")
  default:
      print("Maybe you were not even born yet :D")
  }
  ```

  **2.**

  ```swift
  import UIKit

  let personInfo: (name:String, age: Int) = ("Unbelievable9", 25)

  switch (personInfo) {
  case let (name, age) where age >= 0 && age < 3:
      print("\(name) is a Infant")
  case let (name, age) where age >= 3 && age < 13:
      print("\(name) is a Child");
  case let (name, age) where age >= 13 && age < 20:
      print("\(name) is a Teenager")
  case let (name, age) where age >= 20 && age < 40:
      print("\(name) is an Adult")
  case let (name, age) where age >= 40 && age < 61:
      print("\(name) is a Middle Aged")
  case let (name, age) where age >= 61:
      print("\(name) is an Elderly")
  default:
      print("Maybe you were not even born yet :D")
  }
  ```

- Challenge

  **A**

  **lastName** 的 Scope 只在 if 或者 else if 内，这段 Code 在作用域外是无法访问的

  **B**

  ```swift
  let coordinates = (1, 5, 0)

  "On the x/y plane"

  let coordinates = (2, 2, 2)

  "x = y = z"

  let coordinates = (3, 0, 1)

  "On the x/z plane"

  let coordinates = (3, 2, 5)

  "Nothing special"

  let coordinates = (0, 2, 4)

  "On the y/z plane"
  ```

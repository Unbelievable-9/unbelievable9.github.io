---
title: Swift-S1C2
date: 2016-08-15 11:13:31
categories: Swift 基础
tags: Swift
---

## 读书笔记

- Float 和 Double 在 Swift 中的使用

  `
  A Float takes up less memory than a Double but generally, memory use for numbers isn't a huge issue and you'll see Double used in most places.
  `
  感觉以前撸代码的时候，没事就喜欢用 Float，但是马特大神说了，其实 Double 一下没关系的。

  <!--more-->

- 灵活的Swift

  - 写个数字都可以用下划线了，也太人性化了

    ```swift
    var number: Int = 0
    number = 1_000_000
    ```

  - 变量命名可以用emoji...

    ```swift
    var 🐵👑: String = "孙悟空"
    ```

  - 类型转换跟OC不太一样

    Swift (不同类型之间，不支持自动转换，强类型):

    ```Swift
    var integer: Int = 1
    var decimal: Double = 3.14
    integer = Int(decimal)
    ```

    Objective-C (OC不强制转换的话，自动进行简单的取整转换):
    ```objc
    int integer = 1;
    double decimal = 3.14;
    integer = (Int)decimal
    ```
- Mini-exercises

  ```swift
  import UIKit

  let myAge: Int = 25
  var averageAge: Double = Double(myAge)

  averageAge = (averageAge + 30.0) / 2.0
  ```

- Tuple (元组，为什么我觉得这个翻译这么甜)

  - 推荐这个[最佳实践](http://www.jianshu.com/p/15262607659c)，看完之后有种 "居然还可以这么玩儿"的感触

  - 关于下划线 _

    `
    You'll find that you can use the underscore throughout Swift to ignore a value
    `

- Mini-exercises

  ```swift
  import UIKit

  let constantTuple: (Int, Int, Int, Double)

  let dateInfo:(month: Int, day: Int, year: Int, averageTemperature: Double) = (15, 8, 2016, 33.0)

  let (_, day, _, temperature) = dateInfo

  print(day)
  print(temperature)

  var newDateInfo = dateInfo

  newDateInfo.averageTemperature = 30.0

  print(newDateInfo.averageTemperature)
  ```

- Mini-exercises

  Constant Tuple

  ![Constant Tuple](https://ooo.0o0.ooo/2016/12/16/5853aa76e1566.png)

  First Value of Constant Tuple

  ![First Value](https://ooo.0o0.ooo/2016/12/16/5853aa770609b.png)

- Challenges

  - A

    **Section 1 is valid.**

    **Yes, it is valid code.**

  - B

    **Double.**

    **8.**

  **我觉得我太认真了** 👿

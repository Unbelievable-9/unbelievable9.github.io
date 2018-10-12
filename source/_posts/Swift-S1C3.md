---
title: Swift-S1C3
date: 2016-08-15 15:26:42
categories: Swift 基础
tags: Swift
---

## 读书笔记

- 求余数 (%) 可以用浮点类型

  <!--more-->

- 关于位运算

  平时用的少，知道原理左乘右除，看看马特大神怎么说

  `
  So you'll see shifting only for binary twiddling, which you probably won't see unless you become an embedded systems programmer!
  `

- 普通预算

  没有什么特别的，除了再次强调 Swift 是强类型语言

- Mini-exercise

  - 1

    **evenOdd can only be 0 or 1.**

  - 2

    **answer is 13.**

- 布尔预算

  没什么特别的，带大家认识了下 [George Boole](https://en.wikipedia.org/wiki/George_Boole)

- Mini-exercise
  - 1

    ```swift
    import UIKit

    let myAge = 25

    let isTeenager = myAge >= 13 && myAge <= 19
    ```

    看到结果，哥觉得自己真的老了 😢

  - 2

    ```swift
    import UIKit

    let myAge = 25

    let theirAge = 30

    let isTeenager = myAge >= 13 && myAge <= 19

    let bothTeenagers = (myAge >= 13 && myAge <= 19) && (theirAge >= 13 && theirAge <= 19)
    ```

    看到这个题目时瞬间温暖，马特你是悄悄的在安慰读者吧  😊

- Challenge

  - A

    **1. 4610**

    **2. 5600**

    **3. 4601**

  - B

    **true**

    **false**

    **true**

    **true**

  - C

    **coordinates(sameCoordinates) == otherCoordinates -> false**

    **coordinates(sameCoordinates) != otherCoordinates -> true**

    **coordinates == sameCoordinates -> true**

    **coordinates != sameCoordinates -> false**

    **不能使用 "&&"**

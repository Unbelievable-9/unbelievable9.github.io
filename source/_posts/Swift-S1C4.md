---
title: Swift-S1C4
date: 2016-08-15 17:10:27
categories: Swift 基础
tags: Swift
---

## 读书笔记

- "电脑编程"

  在讲字符串基本原理的时候，居然看见马特大神引用中文了，并不想说的太玄乎，就是单纯记录下还觉得挺有意思的。

  <!--more-->

- Interpolation

  这个是 Swift 独有的字符串处理方式，相比于 Objective-C 的 NSString, 因为 Swift 自身的特性，在代码编写时感觉会轻松很多。
  但是要注意，这个特性虽然非常 Handy, 但是**没有办法格式化输出结果**，比如对于 Double 类型的变量或常量，不能控制小数点保留位数。马特大神也觉得稍微有点遗憾~

  为了认真！举个例子：

  - Objective-C

    ```objc
    NSString *name = @"Jack";
    int age = 25;

    NSString *message = [NSString stringWithFormat:@"Hello my name is %@, I'm %d years old.", name, age];
    ```

  - Swift

    ```swift
    let name = "Jack"
    let age = 25

    let message = "Hello my name is \(name), I'm \(age) years old."
    ```

- 一个关于咖啡的故事

  利用 **café** 这个字符串，讲到了关于字符串的存储机制，这里有两个生僻的概念:

  - Grapheme Cluster

    这个马特举了两个例子，对于 café 中的 **é**，以及对于emoji不用颜色的表情。个人理解就是对于这种特殊的字符(如拉丁文，emoji以及韩文等)，在显示上大家理所当然的认为 **café** 是有4个字母的单词，但是其实存储时，它可能有5个 code point, 多一个 combining character，也有可能直接只用 **é** 对应的 Unicode, 那么这种情况才是4个 code point。

    同时马特强调, 在存储的时对于上述4个和5个 code point的情况，在其他语言中可能判断两个字符串不相等，但在Swift中，判断结果为相等。

    感觉这个细节扣的实在是，**太到位了**

  - Canonicalization

    这个就更抽象了，应该是 Swift 处理字符串时用到的一种技术，Google 无果。感叹马特大神的水平，基础读物就能读到这些底层的概念，作者的水平真是深不可测。

- Mini-exercise

  ```swift
  import UIKit

  let firstName = "Jack"
  let lastName = "Zhao"
  let fullName = firstName + " " + lastName

  let myDetails = "Hello, my name is \(fullName)"

  ```

- Challenge

  - A

    除了第一个其他三个都 **Valid**

    name 用 let 申明的，是常量，不能改变它的值

  - B

    sum: 10 multiplied by 5 equals 50

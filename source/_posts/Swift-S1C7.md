---
title: Swift-S1C7
date: 2016-08-18 14:20:10
tags: Swift
---

## 读书笔记

这章应该是 Section 1 最为重要的一章了，相比于 Chapter 8 9 阐述的新特性，函数对于任何一个编程语言的重要性都是不言而喻的。同时，Swift 已经将函数的地位升级，究竟是怎么升级的，为什么要升级，我就来跟着马特大神一探究竟吧~

<!--more-->

- 函数参数命名
  Swift 的函数参数添加方式，我感觉有点混搭风，看起来挺像 C C++ 的套路，但是又有着 Objective-C 的影子。下面我尝试总结一下，以带有两个参数的函数为例:

  - 基本形式

    ```swift
    import Foundation

    func multiplyValueOf(multiplier: Int, value: Int) -> Int {
        return multiplier * value
    }

    let result = multiplyValueOf(2, value: 3)
    ```

    在调用时，可以看到基本形式中，第一个参数 **不显示参数名的**，第二个参数的 **参数名直接为调用时显示的参数名**

  - 自定义参数名

    这里分为两种情况，代码举例

    ```swift
    import Foundation

    func multiplyValueOf(multiplier: Int, and value: Int) -> Int {
        return multiplier * value
    }

    let result = multiplyValueOf(2, and: 3)
    ```

    在第二个参数名前，可自定义显示参数名，这里为 **and**，与基本形式相比可以知道，如果没有指定的自定义参数名，**对于第二个参数, Swift 默认以参数名作为调用时显示的参数名**。

    如果我想彻底的自定义呢？

    ```swift
    import Foundation

    func multiply(firstValue multiplier: Int, secondValue value: Int) -> Int {
        return multiplier * value
    }

    let result = multiply(firstValue: 2, secondValue: 3)
    ```

    对于第一参数，也是可以自定义参数名，方法雷同。与此同时，如果去掉上面代码的第二个参数自定义名，结果会怎么样呢？

    ```swift
    import Foundation

    func multiply(firstValue multiplier: Int, secondValue: Int) -> Int {
        return multiplier * secondValue
    }

    let result = multiply(firstValue: 2, secondValue: 3)
    ```

    可以看到，第二个参数还是遵照之前的原则，**对于第二个参数, Swift 默认以参数名作为调用时显示的参数名**

    这命名方式灵活得来让我有点不知所措啊，还能这么玩儿的 😂

    但是还没完

  - 省略参数名

    如果我非要不显示任何参数名，咋办？！

    根据上面的总结我们知道，Swift 对于第一个参数，默认不显示参数名，除非你自定义，对于第二个参数名，默认以第二个参数名作为调用时显示的参数名，那么这就有点尴尬了。来看代码

    ```swift
    import Foundation

    func multiply(multiplier: Int, _ secondValue: Int) -> Int {
        return multiplier * secondValue
    }

    let result = multiply(2, 3)
    ```

    看到 Underscore 的时候，其实我的内心是崩溃，这哪里是灵活，这都快玩儿出花来了。

    平复下心情，让我们来回顾下马特大神的之前说的话

    `
    You'll find that you can use the underscore throughout Swift to ignore a value
    `

    原来这个自定义参数名也是可以用下划线忽略的。。。

- Pass by Value or Reference

  值传递还是引用传递，这个地方马特大神讲的很清楚。并且 Swift 很人性的利用 inout 和 & 这两个标记，提示开发人员，你究竟用的哪种传递。

  看到 inout 这个关键字的时候，觉得马特大神的解释非常贴切:

  `
  It's as if the parameter goes in to the function and then comes back out again, thus the keyword inout.
  `

- Mini-exercises

  - 1

    ```swift
    import Foundation

    func printFullName(firstName: String, lastName: String) -> Void {
        print(firstName + " " + lastName)
    }

    printFullName("Jack", lastName: "Zhao")
    ```

  - 2

    ```swift
    import Foundation

    func printFullName(firstName: String, _ lastName: String) -> Void {
        print(firstName + " " + lastName)
    }

    printFullName("Jack", "Zhao")
    ```

  - 3

    ```swift
    import Foundation

    func calculateFullName(firstName: String, lastName: String) -> String {
        let fullName = firstName + " " + lastName

        return fullName
    }

    let myFullName = calculateFullName("Jack", lastName: "Zhao")
    ```

  - 4

    ```swift
    func calculateFullName(firstName: String, lastName: String) -> (fullName: String, length: Int) {
        let fullName = firstName + " " + lastName

        return (fullName, fullName.characters.count)
    }

    let result = calculateFullName("Jack", lastName: "Zhao")

    let myFullName = result.fullName

    let lengthOfMyFullName = result.length
    ```

- 函数地位的升级

  在 Swift 中函数可以像变量一样使用，马特提到最多的就是，在函数之间传递函数，并提到这个特性的好处

  ```
  It's extremely useful to be able to pass functions to other functions, and it can help you write reusable code.
  ```

  这里没有距离的原因，可能是需要大型点的例子才能展示如马特说的代码复用技巧吧。后续我会去搜集一些相关的资料然后发到博客。

- Challenge

  - A

    ```swift
    import Foundation

    func isNumberDivisible(number: Int, by byNumber: Int) -> Bool {
        if number % byNumber == 0 {
            return true
        } else {
            return false
        }
    }

    func isPrime(number: Int) -> Bool {
        if number < 0 {
            return false
        }

        for i in 2...Int(sqrt(Double(number))) {
            if isNumberDivisible(number, by: i) {
                return false
            }
        }

        return true
    }

    isPrime(6)
    isPrime(13)
    isPrime(8893)
    ```

  - B

    ```swift
    import Foundation

    func fibonacci(number: Int) -> Int {
        if number <= 0 {
            return 0
        } else if number == 1 || number == 2 {
            return 1
        }

        return fibonacci(number - 1) + fibonacci(number - 2)
    }

    fibonacci(1)
    fibonacci(2)
    fibonacci(3)
    fibonacci(4)
    fibonacci(5)
    fibonacci(10)
    ```

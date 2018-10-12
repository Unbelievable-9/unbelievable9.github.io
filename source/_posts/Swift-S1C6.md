---
title: Swift-S1C6
date: 2016-08-18 10:56:20
tags: Swift
---

## 读书笔记

- Range

  看了下 Apple 官方 API 文档，Range 是一个结构体，这都不是最重要的，最重要的是这个:

  ```swift
  let closedRange = 1...3
  let halfOpenRange = 1..<3
  ```

  这个点点点语法，简直是太 Handy 了！

  <!--more-->

- For Loop

  这个太经典了，不过 For 循环配合 Range 再配合 Type Inference 让 Swift 的 For 循环看起来实在是太精炼了。

  马特给大家展示了一个 Playground 的可视化效果，听说这个功能已经被好多人玩儿坏了，后续找找 Demo 给大家共享下。

- While Loop

  讲死循环的时候槽点又来了，配图的哥们大喊 **Command-Option-Esc** 想起了年少时动不动就喜欢 **Ctrl-Alt-Del** 的自己。

  Swift 中条件后置的 While 循环，叫 repeat-while，记得第一次接触编程世界的 C 语言里，它叫 do-while。

- 循环中的关键字

  - break continue

    这两个关键字基本的功能完全没变，不必多说

  - Labeled Statements

    这个东西刚看到的时候，着实反应了一会儿，类似给每个循环命名，在配合 break 或 continue 的时候，可以在嵌套循环时，改变外层循环的行为。

    Swift 中的这一特性，一下让编码变得十分灵活，文章的最后我尝试采用这种特性，写一个 99 乘法表~

- Challenge

  - A

    **sum: 15**
    **6 Iterations**

    **10**

- 99 乘法表

  要兑现承诺，主要想试试这个 **Labeled Statements**

  ```swift
  import Foundation

  rowLoop: for row in 1...9 {
      columnLoop: for column in 1...9 {
          if column > row {
              //根据 99 乘法表的样式，列数大于行数时应该换行
              print("")

              continue rowLoop
          }

          var tempString = ""

          if String(column * row).characters.count > 1 {
              //计算结果为2位时 不多加空格
              tempString = "\(column) * \(row) = \(column * row)"
          } else {
              if column == 1 {
                  //计算结果为1位且为第一行时，因为所有结果都是1位，不多加空格
                  tempString = "\(column) * \(row) = \(column * row)"
              } else {
                  //计算结果为一位且不为第一行是，与其他结果为两位的对齐，所以多加一个空格
                  tempString = "\(column) * \(row) = \(column * row) "
              }
          }
          //在 Swift 2.0 中 print 和 println 合并，默认行位已换行符结尾
          //这里可以指定结尾字符，指定为空格分隔符
          print(tempString, terminator:" ")
      }
  }
  ```

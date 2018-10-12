---
title: Swift-S1C8
date: 2016-08-18 17:39:47
tags: Swift
---

## 读书笔记

关于 **闭包** 这个词，第一次在看到的时候，只感觉非常头晕，完全体会不到这个中文翻译的精髓在哪里。想当初，在刚看到 Objective-C 中 Block 用法时，也是同样的心情，直到后来一个 **匿名函数** 的翻译才让我茅塞顿开。

那么 **闭包** 作为中文，应该怎么理解呢？

<!--more-->

在经过一些调研之后，我觉得在知乎上的 [这个话题](http://www.zhihu.com/question/24084277) 中，包含了各位前辈的真知灼见，我个人比较喜欢寿司的那个答案。

- 基本用法

  根据书上的 Code Snippet，整理了个备忘录

  ```swift
  import Foundation

  //带有 Closure 的函数
  func operateNumbers(x: Int, _ y: Int, operation: (Int, Int) -> Int) -> Int {
      let result = operation(x, y)

      print(result)

      return result
  }

  //完整调用方法
  operateNumbers(1, 2, operation: { (a: Int, b: Int) -> Int in
      return a + b
  })

  //省略返回值的调用方法
  operateNumbers(3, 4, operation: { (a: Int, b: Int) in
      a - b
  })

  //最简洁的调用方法
  operateNumbers(5, 6, operation: {
      $0 * $1
  })

  //Trailing Closure Syntax
  //只有在 Closure 作为函数最后一个参数时才可以这么使用
  operateNumbers(7, 8) {
      $0 / $1
  }
  ```

- Trailing Closure Syntax (尾随闭包)

  Closure 和 Swift 中的函数类似，在参数引用的时候，有些变化方式，非常灵活。看到这个 **尾随闭包** 的时候，觉得很有意思，所以去查了一些资料，发现这个语法还是很常用的。

  [CocoaChina 里面有一篇文章](http://www.cocoachina.com/swift/20160106/14862.html) 对于 Closure 的实际应用情况，讲的比较到位。

  可以直接参阅 Closure 部分内容

  - View Controller 传值

    作者首选举了一个 View Controller 之间传值的例子，在用 Objective-C 写程序的时候，这种事我一般都用 Delegate 来做，其实也可以用 Block 来做，个人习惯问题。因为我觉得一个 Controller 里面有各种各样的 Delegate 的话，感觉像拼积木一样，很有层次感。

    看完这个例子实在是手痒，就自己新建工程写了一次，感觉虽然 iOS SDK 的 API 基本没有变化，但是真正在用 Swift 去实现的时候，还是各种不适应，还需要勤加练习。

    测试工程主要的目的就是， 视图控制器1 跳转到 视图控制器2，在 视图控制器2 中的 TextField 里面输入内容，跳转回 视图控制器1 时把输入的内容传回 视图控制器1 并显示，如果没有内容则还原显示。功能很简单，下面附上主要的代码:

    **RootViewController.swift**

    ```swift
    /*

     File Name:      RootViewController
     Author:         Unbelievable9
     Created Time:   2016-08-22
     Description:    根视图控制器

     2016 Unbelievable9 All Rights Reserved.

     */

    import UIKit

    class RootViewController: UIViewController {
        //传递参数内容显示 Label
        @IBOutlet weak var parametersLabel: UILabel!

        @IBAction func TapToGoToSecondViewController(sender: AnyObject) {
            //获取 Storyboard
            let storyboard = UIStoryboard(name: "Main", bundle: NSBundle.mainBundle())

            //从 Storyboard 初始化第二个视图控制器
            let secondViewController =
                storyboard.instantiateViewControllerWithIdentifier("Second View Controller") as! SecondViewController

            //闭包函数回调实现
            secondViewController.onInputStringCallback = { (inputString: String) -> Void in
                self.parametersLabel.text = inputString
            }

            //压入第二视图控制器
            self.navigationController?.pushViewController(secondViewController, animated: true)
        }
    }
    ```

    **SecondViewController.swift**

    ```swift
    /*

     File Name:      SecondViewController
     Author:         Unbelievable9
     Created Time:   2016-08-22
     Description:    第二视图控制器

     2016 Unbelievable9 All Rights Reserved.

     */

    import UIKit

    //自定义闭包函数
    typealias inputStringClosure = (String) -> Void

    class SecondViewController: UIViewController {
        //内容输入 TextField
        @IBOutlet weak var inputTextField: UITextField!

        var onInputStringCallback: inputStringClosure?

        @IBAction func TapToGoBackToRootViewController(sender: AnyObject) {
            //内容输入判断
            if self.inputTextField.text != nil && self.inputTextField.text != "" {
                if self.onInputStringCallback != nil {
                    //闭包函数回调
                    self.onInputStringCallback!(self.inputTextField.text!)
                }
            } else {
                //闭包函数回调
                self.onInputStringCallback!("No Parameter")
            }

            //弹回根视图控制器
            self.navigationController?.popViewControllerAnimated(true)
        }

        //Swift 中的 Dealloc
        deinit {
            print("\nSecond View Controller is Destroyed.")
        }
    }
    ```

    实现这个基本功能，还牵扯到了即将来临的 Chapter 8 的一些内容，这里当提前热热身。在参考别人代码以及自己尝试模仿实现的时候，给我的感觉就是 Swift 的 Closure 和 Objective-C 的 Block 其实在本质上都是一个东西，只是在两种语言环境下，需要一段时间去适应，多加练习应该不是难事。

  - 数组常用闭包函数

    这一部分内容，完全就是在展示 **尾随闭包** 语法使用的典型案例，这里还牵扯到了一些函数式编程的思想，看起来非常的酷，这里不做过多的讨论！

- Challenge

  **A.**

  ```swift
  import Foundation

  func repeatTask(times: Int, task: () -> Void) -> Void {
      for _ in 1...times {
          task()
      }
  }

  //简洁写法
  repeatTask(10, task: {
      print("Swift Apprentice is a great book!")
  })

  //尾随闭包写法
  repeatTask(10) {
      print("Swift Apprentice is a great book!")
  }
  ```

  **B.**

  ```swift
  import Foundation

  //斐波那契递归函数
  func fibonacci(number: Int) -> Int {
      if number <= 0 {
          return 0
      } else if number == 1 || number == 2 {
          return 1
      } else {
          return fibonacci(number - 1) + fibonacci(number - 2)
      }
  }

  //题目所需计算函数
  func mathSum(times: Int, operation: (Int) -> Int) -> Int {
      var result = 0

      for i in 1...times {
          result += operation(i)
      }

      return result
  }

  //平方数 1-10 求和
  //简洁写法
  mathSum(10, operation: {
      $0 * $0
  })

  //尾随闭包写法
  mathSum(10) {
      $0 * $0
  }

  //斐波那契数 1-10 求和
  mathSum(10, operation: fibonacci)
  ```

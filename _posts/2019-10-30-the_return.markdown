---
layout: post
title:      "The Return"
date:       2019-10-31 03:10:12 +0000
permalink:  the_return
---

What is "void value expression" error?

```def kind ((side_a, side_b, side_c))
    if side_a == side_b && side_a == side_c && side_b == side_c
      "equilateral"
    elsif
      side_a == side_b || side_b == side_c || side_a == side_c
       "isosceles"
    elsif
      "scalene"
    elsif
      side_a + side_b != side_c
      raise TriangleError
    end
  end```

https://doughughes.net/2018/07/06/ruby-void-value-expression-errors-explained/

The answer taken from the link above basically means that the error is generated because the Return expectation didn't match with Ruby's process of automatically returning values in a method. If I used the word "return" 

"It’s important to know that the return keyword immediately terminates execution of the method and returns the specified value (or nil)."

so In this case I got this error becuase I didn't understand that I didn't need to add return to the method. That is implied and done automatically as a part of Ruby.


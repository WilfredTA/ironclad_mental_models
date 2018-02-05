# Mental models for recursion

## Table of contents

### [Introduction to recursion](#introduction-to-recurision-1)
### [Exponent](#exponent-1)

## Introduction to recursion

Problems that you can solve with recursion have a recursive structure. This
usually means that the problem, a) is possible to reduce into smaller problems,
and b) has a knowable base case.

Tips for writing recursive problems:

1) Use simple base cases

Avoiding "arms length" base cases can be a good idea to keep the logic of your
code simple and easy to understand. For example, if you are writing a function
that can compute raise a base to a power of `exp`, base cases like this are
unnecessarily specific, and take away from some of the simplicity you can
achieve in a recursive solution.

```rb
return 1 if exp == 0
return base if exp == 1
return base * base if exp == 2
```

If you structure your problem right, all you need for your base case is the
first one - `return 1 if exp == 0`.

2) Be clear and consistent in terms of what's the return value of the recursive algorithm.

## Exponent

Write a function that takes a number (base) and an exponent. Raise the base to
the power of a given exponent.

**Solution 1: Simplest recursive solution - positive numbers**

This is perhaps the most straight-forward way to solve the exponent/to the power
of problem using recursion. Note that this first solution will only work for
positive exponents.

```rb
def power(base, exponent)
  if exponent == 0
    return 1
  else
    power(base, exponent - 1)
  end
end
```

Here's an example of what the callstack would look if we call `power(2,3)`

exponent|recursive call               |return value
--------|-----------------------------|------------
0       |                             | 1
1       |2 * power(2, (1-1)) => 2 * 1 | 2
1       |2 * power(2, (2-1)) => 2 * 2 | 4
2       |2 * power(2, (2-1)) => 2 * 4 | 8

Runtime - O(n):

Essentially, what we're trying to find the cost of exponent ``(exponent - 1)`` + the base case`( 0(1))`. This means that our runtime complexity is `O(exponent)`.
https://cs.muic.mahidol.ac.th/courses/ds/lects/lect03.pdf

Size - O(n): Only n number of stacks required at any one time.

To understand recursion, let's also take look at an iterative solution.

**Solution 2: Simple iterative solution**

```rb
def power(base, exponent)
  result = 1.0
  if exponent > 0
    exponent.times do |_|
      result *= base
    end
  else
    (-1 * exponent).times do |_|
      result /= base
    end
  end

  result
end
```

Notes on negative powers:

1) Dealing with negativity: One of the easiest ways to deal with a negative
   exponent is to make it positive and have it divided by 1.
2) Dealing with decimals. If we want to find `power(2, -2)`, then our algorithm   
   will run 1/4 as its final operation. In Ruby this will return 0, but the
   answer we're looking for is `0.25`. Therefore using `1.0` ensures that we'll
   return be able to return the correct decimal number (  a float).

Runtime - O(n):  
Size - O(n): Only n number of stacks required at any one time.

**Solution 3: More efficient solution - positive numbers**

By only making recursive calls for the exponent / 2, we can halve the size of
our call stack and halve the size of our problem space at each call.

```rb
def power(base, exponent)
  if exponent == 0
    return 1
  elsif exponent % 2 == 0
    half = power(base, exponent / 2)
    return half * half
  else
    half = power(base, exponent / 2)
    return base * half * half
  end
end
```

Runtime - O(log(n)): For every n in 1..exponent, we perform n/2
computations.  
Size - O(log(n)): Only log(n) number of stacks required at any one time

**Solution 4: Negative & positive powers recursive solution**

Here's our final recursive solution which includes our earlier optimization and
and also works for negative powers as well.

Runtime - O(log(n))  
Space - O(log(n))

```rb
def power(base, exponent)
  if exponent == 0
    return 1
  elsif (exponent < 0)
    positive_exponent = -1 * exponent
    return 1.0 / power(base, positive_exponent);
  elsif exponent % 2 == 0
    half = power(base, exponent / 2)
    return half * half
  else
    half = power(base, exponent / 2)
    return base * half * half
  end
end
```

**Solution 5: Tail optimized**

Tail optimization is another important technique in recursion. Normally, the
number of stacks is `n` deep where `n` is the problem size. With a tail
optimized problem, we can calculate the answer from the bottom level of the
stack. The significance of this is that the preceding stacks are dropped by the
smart compiler since they don't need to be maintained, reducing the space
complexity of the algorithm.

```js
let power = (base, power_of, acc=base) => {
  if (power_of === 0) {
    return 1
  } else if (power_of === 1) {
    return acc
  } else {
    return power(base, power_of - 1, base * acc);
  }
}
```


# Mental Models for Backtracking Algorithms

## Introduction to Backtracking
Backtracking is essentially a depth first search, but with an undetermined about of branches (unlike a binary tree). Therefore, to make sure each root is hit, we use a loop rather than a predetermined number of recursive calls per method call.

You have to maintain the state of the solution at one level or another of the decision tree. This can be achieved by using an immutable value that is added to. I.e., passing a new string as input to each recursive call, or by mutating an object during each recursive call and reversing those mutations right after a recursive call returns.

If a recursive call is guaranteed to add at most one element to a cumulative array of solutions, then pop that array when the recursive call returns. *Make sure to couple the recursive call and the popping; if the recursive call doesn't happen, then the popping shouldn't happen either.*

To construct the correct solution, you can either offset decisions to the dead-end logic or the branching logic. More efficient solutions use smarter branching since smarter branching logic reduces the number of incorrect solutions that are produced in the first place. The tradeoff here is "ease" vs "performance"; offsetting more logic to dead-end logic is usually easier but less performant. It is a good initial brute force approach, especially for nontrivial problems.


## Table of Contents
1. Permutations
2. Subsets
3. Combinations
4. Permutations with Duplicates
5. Subsets with Duplicates
6. Combination Sum
7. Palindrome Partitioning
8. Generate Parenthesis



### Permutations


### Subsets


### Combinations


### Permutations with Duplicates


### Subsets with Duplicates


### Combination Sum


### Palindrome Partitioning

### Palindrome Partitioning
- before adding to the solution, need to decide if the string is palandrome first(T/F)
- add the palindrome substring into solution, range is start..i+1
- recursion stops when we done iterating through each char in the given string
- reset the conditions for the solution

example diagram:
branching for input "aab", number represents the indices: 
```
                   aab
                /   |    \
              0,0  0,1  0,2 
              a    aa   aab
             / \    |     \
           1,1 1,2  2     nil
            a  ab   b(2)
            /
           b
```
Return value: `[['a','a','b'],['aa', 'b']]`, skip value: `[['a','ab'],['aab']]`

Coded solution:
```
def partition(s)
  result = []
  partition_helper(s, 0, [], result)
  result
end

def partition_helper(s, start_idx, solution, result)
  if start_idx == s.length
    result << solution.clone
  else
    (start_idx..s.length-1).each do |index|
      substring = s.slice(start_idx..index)
      if check_pal(substring)
        solution << substring
        partition_helper(s, index + 1, solution, result)
        solution.pop
      end
    end
  end
end

def check_pal(substring)
  (0..substring.length/2).each do |index|
    if substring[index] != substring[substring.length-index-1]
      return false
    end
  end
  true
end


```

### Generate Parenthesis

Given a number *n*, generate every possible combination of *n* well-formed *pairs* parenthesis.

Example: if *n* = 3, return:
```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

Thinking process:
- write the two parans "(" and right paran ")", length of each side has to be equal to n
- during the generating process, 
- 1: you have to make sure the length of "(" is greater than  the length of ")" before you 
     try to add new ")" => add the left parans first before adding right 
  2. only write the valid parans into solution, be sure to mutate the string

Coded solution:
```
def generate_parenthesis(n)
  result = []
  generate_parenthesis_helper(n,0,0,"",result)
  result
end

def generate_parenthesis_helper(n,left,right,solution,result)
  # add solution to the result
  if left == n && right == n
    result << solution.clone
  end
  
  if (left < n)
    solution << "("
    generate_parenthesis_helper(n,left+1,right,solution,result)
    solution.chop!
  end
  
  if (right < left)
    solution << ")"
    generate_parenthesis_helper(n,left,right+1,solution,result)
    solution.chop!
  end
end


```




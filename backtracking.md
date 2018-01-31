
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
Track state: An index to start the substring at (as start position), a results array (as result) and an array of substrings in current traversal tree (as solution)

Dead end logic: If position > last index of the string then put current array of substrings into result

Branch logic:
Loop through string. Generate a substring from start position to current index. If substring is a palindrome, add it so the current solution array and then recurse down a branch of the tree, setting the start position to the index of the current_char + 1 (to make sure the same letter at the same index is not used more than once).


Decision tree for input "aab": 
```
          "a"            "aa"     "aab"
          / \               \
        "a" "ab"             "b"
       / 
     "b"
```
Return value: `[['a','a','b'],['aa', 'b']]`

Coded solution:
```
def partition(s)
    result = []
    partition_helper(s, result, [], 0)
    result
end


def partition_helper(string, result, solution, position)
  
  if position == string.length 
    result << solution.clone unless solution.empty?
  else
    i = position
    while i < string.length do
      substring = string[position..i]
      if substring == substring.reverse
        solution << substring
        partition_helper(string, result, solution, i + 1)
        solution.pop
      end
      
      i += 1
    end
  end
end


```

### Generate Parenthesis







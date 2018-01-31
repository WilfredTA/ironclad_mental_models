
# Mental Models for Backtracking Algorithms

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
Track state: An index to start the substring at (as position), a results array (as result) and an array of substrings in current traversal (as solution)

Dead end logic: If position > last index of the string

Branch logic:
Loop through string, generating substring at position..current_idx
If this substring is a palindrome, then recurse into next branch, setting the start position to current index + 1 so that letters already in the solution are not reconsidered


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







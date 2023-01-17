# Valid Anagram [[LeetCode](https://leetcode.com/problems/valid-anagram/)]
**Difficulty: EASY**\
**Language: Python3**

## Solution 1. Hash Table
``` python
def isAnagram(s: str, t: str) -> bool:
    # check if length of both string is equal
    if (len(s) != len(t)): 
        return False

    # create hash table for both `s` and `t`
    s_count, t_count = {}, {}
        
    # construct hash table that counts number of each alphabets in the string (we know both string has same length)
    for i in range(len(s)):
        s_count[s[i]] = 1 if s_count.get(s[i]) is None else s_count[s[i]] + 1
        t_count[t[i]] = 1 if t_count.get(t[i]) is None else t_count[t[i]] + 1
            
    # compare between `s_count` and `t_count` if they are equal
    for key in s_count.keys():
        if (s_count[key] != t_count.get(key)):
            return False
        
    # return `True` if no difference is found
    return True
```
**Time Complexity: `O(n)`**\
**Space Complexity: `O(n)`**\
**(Assuming the length of `s` is `n` and the length of `t` is `m` where `n > m`)**

if the length of `s` and `t` differs, then we immediately return `False` with `O(1)` time. However if they are the same, then we construct hash table for both string by iterating every indices of the string (both string have same length anyway), this costs `O(n)` because the hash operations within the loop takes `O(1)` time.
Now when we compare the hash tables, this will take `O(n)` times as we loop through every keys in the hash table. Finally, returning `True` if the comparison end without finding any difference in the tables. Overall, the whole process will take `O(n)`.

For space complexity of the algorithm, we are constructing two hash maps when `n = m`. Hence it will take up `O(n + n) = O(n)` space.

## Solution 2. Sorting
``` python
def isAnagram(s: str, t: str) -> bool:
    # Sort both strings and return the sorted result (assume the sorting algorithm will take `O(n log n)` time and `O(1)` space)
    return sorted(s) == sorted(t)
```
**Time Complexity: `O(n log n)`**\
**Space Complexity: `O(1)`**\
**(Assuming the length of `s` is `n` and the length of `t` is `m` where `n > m`)**

When we sort both string alphabetically, the sorted result must be equal if they are anagrams.

The time consumed for sorting `s` is `O(n log n)` and `t` is `O(m log m)` but since we assumed `n > m`, we can simplify it into `O(n log n)`.

Now for the space complexity, since the algorithm does not use any extra memory space for sorting (as assumption), we have `O(1)`.

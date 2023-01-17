# Contains Duplicate [[LeetCode](https://leetcode.com/problems/contains-duplicate/)]
**Difficulty: EASY**\
**Language: Python3**

## Solution 1. Brute Force
``` python
def containsDuplicate(nums: List[int]) -> bool:
    # loop through each index in `nums`
    for i in range(len(nums)):

        # search for any duplicate for `nums[0:i]`
        for j in range(i):

            # if duplicate is found, return `True`
            if (nums[i] == nums[j]):
                return True

    # if loop end with no duplicate return `False`
    return False
```
**Time Complexity: `O(n^2)`**\
**Space Complexity: `O(1)`**

Since we are looping over `i`, which depends on the size of `nums` given, `n` this is `O(n)`. Also for each loop, we have another loop, `j` which depends on the size of `i` (which `i` depends on `n`) hence another `O(n)`. Now within the nested loops, we have simple `O(1)` operations, we end up with time complexity of `O(n * n) = O(n^2)`.

On the otherhand, we do not use any extra memory space, we get space complexity of `O(1)`.

## Solution 2. Sort and Search
``` python
def containsDuplicate(nums: List[int]) -> bool:
    # Sort `nums`
    nums.sort()
    
    # loop through each index in `nums` except for the last one (so we can always compare the one next to it)
    for i in range(len(nums) - 1):
        
        # compare between the number of index and the number next to it (we already sorted the list, so any duplicate must sit next to each other)
        if (nums[i] == nums[i + 1]):
            return True
    
    # if loop end with no duplicate return `False`
    return False
```
**Time Complexity: `O(n log n)`**\
**Space Complexity: `O(1)`**

First of all, best sorting algorithm consumes at least `O(n log n)` time. After the sorting, the loop over `i` depends on the size of the `nums` given, `n` resulting `O(n)`. Additionally, the comparison in each loop take `O(1)` time, so the whole loop only takes `O(n)`. However since, `O(n log n)` time is already consumed from sorting, by the asymptotic analysis, total time complexity of the algorithm is `O(n log n)`.

Now for the space complexity, since the algorithm does not use any extra memory space, we have `O(1)`.

## Solution 3. Hash Set
``` python
def containsDuplicate(nums: List[int]) -> bool:
    # create a set
    hash = set()

    # run through each number in the `nums`
    for n in nums:

        # if `hash` contains the number return True 
        if n in hash:
            return True
            
        # otherwise add the number to `hash`
        hash.add(n)

    # if looped ended with no duplicate found, return False
    return False
```
**Time Complexity: `O(n)`**\
**Space Complexity: `O(n)`**

In this case, we create a hash set to record which value we've been check in the past. From the first loop over `n` which iterates over `nums` depends on `n`, the size of `nums` which takes `O(n)` times. within every iterations, we check if the number exists within the `hash` already, if it does return `True` otherwise, add the number to the `hash` for record. But due to the properties of hash set, checking a hash set and adding a new number to hash set only costs `O(1)` time. Therefore, the algorithm overall take time complexity of `O(n)`.

However, for the size complexity, the size of hash set increases overtime as we checks over the elements in the list (upto `n` elements). Hence, the space complexity of the algorithm is `O(n)`.

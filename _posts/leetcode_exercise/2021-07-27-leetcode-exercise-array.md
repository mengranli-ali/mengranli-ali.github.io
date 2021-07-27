---
layout: post
title: "Leetcode Exercise: Array"
subtitle: 'Array related Qs'
author: "Mengran"
header-style: text
tags:
  - Python
  - Leetcode
  - Array
---

### Max Consecutive Ones

Given a binary array nums, return the maximum number of consecutive 1's in the array.

**Example 1:**

Input: nums = [1,1,0,1,1,1]

Output: 3

Explanation: The first two digits or the last three digits are consecutive 1s. The maximum number of consecutive 1s is 3.

**Example 2:**
Input: nums = [1,0,1,1,0,1]

Output: 2

**_Solution:_**

Step 1: initialize 2 variables to 0 ( one for counting and other for maximum count)

Step 2: using a loop (loop through the nums list) to check whether the number is 1
- if it is 1 then increment a counter by 1 ( note: counter is initially 0)
- check if the maximum count is greater than the counter, if yes then assign the counter value to maximum count
- if it is not 1 then assign 0 to counter


Step 3: after looping through the list return the maximum count

```vim
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        max_ = 0                  #maximum count
        c = 0                     #counter
        for i in nums:
            if i == 1:
                c += 1
                
                # if max_ < c:
                #    max_ = c
                
                max_ = max(max_, c)
                
            else:
                c = 0
        return max_

```

```vim
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        count = 0
        result = 0
        for i in range(len(nums)):
            if nums[i] == 0:
                count = 0
                
            else:
                count += 1
                result = max(count, result)
                
        return result
```

**One-line Solution:**

Steps:

- Converting the array into string
- Separating the string by '0'
- creates a list of 1 sequences
- which are mapped by len
- which creates an array with the length of each sequence
- Max acquires the largest sequence number and returns it

```vim
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        return max(list(map(len, ("".join(list(map(str, nums)))).split('0'))))


    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        return max(map(len, ''.join(map(str, nums)).split('0')))
```


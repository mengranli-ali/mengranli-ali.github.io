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

### Find Numbers with Even Number of Digits

Given an array nums of integers, return how many of them contain an even number of digits.

**Example 1:**

Input: nums = [12,345,2,6,7896]

Output: 2

Explanation: 

- 12 contains 2 digits (even number of digits). 
- 345 contains 3 digits (odd number of digits). 
- 2 contains 1 digit (odd number of digits). 
- 6 contains 1 digit (odd number of digits). 
- 7896 contains 4 digits (even number of digits). 
- Therefore only 12 and 7896 contain an even number of digits.

**Example 2:**

Input: nums = [555,901,482,1771]

Output: 1 

Explanation: 

Only 1771 contains an even number of digits.

**_Solution 1:_**

```vim
class Solution:
    def findNumbers(self, nums: List[int]) -> int:
        totalEven = 0
        
        for num in nums:
            digitCount = 0
            while num >= 1:
                num /= 10
                digitCount += 1
            
            if digitCount % 2 == 0:
                totalEven += 1
                
        return totalEven

```

**_Solution 2:_**

Using len(str) to count digits:

```vim
def findNumbers(self, nums: List[int]) -> int:
	return sum([len(str(num)) % 2 == 0 for num in nums]) 
```

**_Solution 3:_**

Turn it into string

```vim
def findNumbers(self, nums: List[int]) -> int:
	res = 0
	for num in nums:
		if len(str(num)) % 2 == 0:
			res += 1
	return res
```


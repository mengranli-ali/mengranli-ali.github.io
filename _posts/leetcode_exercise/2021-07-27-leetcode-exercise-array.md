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

### Squares of a Sorted Array

Given an integer array `nums` sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

**Example 1:**

Input: nums = [-4,-1,0,3,10]

Output: [0,1,9,16,100]

Explanation: 

After squaring, the array becomes [16,1,0,9,100].

After sorting, it becomes [0,1,9,16,100].

**Example 2:**

Input: nums = [-7,-3,2,3,11]

Output: [4,9,9,49,121]

**Solution 1:**

Explanation:

- Square of negative numbers is positive. (square of zero is zero) eg square of -4 is `(-4) * (-4) = 16`
- Since input is sorted (can include negative numbers), the squares of each number will follow a shape as shown in pic below.
- We have to start with 2 pointers: one pointing to left most and the other pointing to right most.
- Keep comparing the 2 pointers and add maximum among the two into the results list.
- Since we are adding in reverse order, we will have to reverse the list at the end. (or else use deque and appendleft)
- Keep moving pointers until all numbers processed.


```vim
class Solution:
    
    def sortedSquares(self, A: List[int]) -> List[int]:
        
        # if dont want to use deque, use regular list/stack instead and reverse it at the end
        results = collections.deque() # to use appendleft func
    
        left = 0
        right = len(A) - 1
        
        while left <= right:
            
            pow_left = int(math.pow(A[left], 2))
            pow_right = int(math.pow(A[right], 2))
            
            if pow_left >= pow_right:
                results.appendleft(pow_left)
                left += 1
            else: # pow_left < pow_right
                results.appendleft(pow_right)
                right -= 1
                
        return results
```

**Solution 2:**

```vim
class Solution:
    def sortedSquares(self, A: List[int]) -> List[int]:
        return(sorted([x*x for x in A]))
        
    def sortedSquares(self, A: List[int]) -> List[int]:
        return sorted([v**2 for v in A])
```

**Solution 3:**

```vim
def sortedSquares(self, A: List[int]) -> List[int]:
        return_array = [v**2 for v in A]
		return_array.sort() # This is in place!
		return return_array
```

**Solution 4:**

```vim
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        for i in range(len(nums)):
            nums[i] *= nums[i]
        nums.sort()
        return nums
```


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

### Duplicate Zeros

Given a fixed length array `arr` of integers, duplicate each occurrence of zero, shifting the remaining elements to the right.

Note that elements beyond the length of the original array are not written.

Do the above modifications to the input array **in place**, do not return anything from your function.

**in-place操作**，意思是所有的操作都是**”就地“**操作，不允许进行移动，或者称作原位操作，即不允许使用临时变量。

**Example 1:**

Input: [1,0,2,3,0,4,5,0]

Output: null

Explanation: 

After calling your function, the input array is modified to: [1,0,0,2,3,0,0,4]

**Example 2:**

Input: [1,2,3]

Output: null

Explanation: After calling your function, the input array is modified to: [1,2,3]

**Thinking：**
- The problem statement clearly states that we are to modify the array in-place. That does not mean we cannot use another array. We just don't have to return anything.
- A better way to solve this would be without using additional space. The only reason the problem statement allows you to make modifications in place is that it hints at avoiding any additional memory.
- The main problem with not using additional memory is that we might override elements due to the zero duplication requirement of the problem statement. How do we get around that?
- If we had enough space available, we would be able to accommodate all the elements properly. The new length would be the original length of the array plus the number of zeros. 

Solution:

Start from the back and adjust items to correct locations. If item is zero then duplicate it.

```vim
class Solution:
    def duplicateZeros(self, arr: List[int]) -> None:
        zeroes = arr.count(0)
        n = len(arr)
        for i in range(n-1, -1, -1):
            
            # Every number in the original array is shifted to the right by the number of zeros so far.
            # Because of the cutoff, we are going to check if the new position of the number is inside the array.
            if i + zeroes < n:
                arr[i + zeroes] = arr[i]
            
            # This is checking if there is a Θ that should be included.
            if arr[i] == 0: 
                zeroes -= 1
                if i + zeroes < n:
                    arr[i + zeroes] = 0
```

Your input: `[1,0,2,3,0,4,5,0]`

Your answer: `[1,0,0,2,3,0,0,4]`

Expected answer: `[1,0,0,2,3,0,0,4]`



**Logic behind:**

original arr:
`[1, 0, 2, 0, 3, 0]`

num of zeros so far:
`[0, 1, 1, 2, 2, 3]`

arr with duplicate 0s (Θ means a duplicate 0):
`[1, Θ, 0, 2, Θ, 0, 3, Θ, 0]`

arr after cutoff：
`[1, Θ, 0, 2, Θ, 0]`

This algorithm goes backwards and applies correct shifting distance to every element.

1.Why backwards?

If we would start shifting from left to right, then we would be overwriting elements before we have had the chance to shift them,
that is why we go backwards instead.

We make sure we have shifted out an element before we shift another one into its original position.

2.What is the correct shift distance?

The duplication of a zero pushes all elements to the right of it by one.
This means also that every element is shifted to the right as many times as there are zeroes to the left of it.

E.g. in the array `[1,0,2,0,3]` , 1 will not move, 2 will shift one position and 3 will shift two positions.
As we go backwards, every time we bypass a zero (and duplicate it), the shift distance decreases for the elements we haven't shifted yet, because there is one less zero in front of them.

3.Why the < n checks?

Shifts push some of the elements out of the array. We do the < n checks to make sure we write down only elements that are shifted to a valid position inside the array and we ignore the ones falling off the end.


**Simple Solution:**

```vim
class Solution:
	def duplicateZeros(self, arr: List[int]) -> None:
		i = 0
		n = len(arr)
		while(i<n):
			if arr[i]==0:
				arr.pop()
				arr.insert(i,0)
				i+=1
			i+=1
```
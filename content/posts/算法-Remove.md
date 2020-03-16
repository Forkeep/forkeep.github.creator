---
title: "算法 Remove Duplicates from Sorted Array"
date: 2020-03-16T10:42:55+08:00
draft: true
---


# 算法-Remove Duplicates from Sorted Array

[Remove Duplicates from Sorted Array](https://leetcode.com/explore/featured/card/top-interview-questions-easy/92/array/727/)

**Example 1:**

```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
```

**Example 2:**

```
Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
```



>  在这个题目中遇到了一个in-place algorithm 原地算法 ,简单来说就是不开辟新空间的算法，节省空间复杂度



思路：

遍历一遍这个数组，因为这个题目有一些先天条件就是他会按顺序排序，我们主要的任务就是把这重复的找出来往后移或者删掉。

**js代码实现：**

```javascript
var removeDuplicates = function(nums) {
    if(nums.length ===1){
        return 1
    }
   let j=0
    for(let i=1;i<nums.length;i++){
        if(nums[i] === nums[j]){
            nums.splice(i,1)
            i=j
        }else{
            j+=1
        }
//             i=i-1
//         }else{
//             j+=1
//         }
    
         
    }
    return nums.length
};
```



**LeetCode上大神的代码：**

```js
var removeDuplicates = function(nums) {
    let lastIndex = 0;
    
    if (nums.length <=1) return nums.length;
    
    for (let i = 1; i < nums.length; i++) {
        if (nums[i] > nums[i-1]) {
            lastIndex++;
            nums[lastIndex] = nums[i];
        }
    }
        
    return lastIndex + 1;
};
```


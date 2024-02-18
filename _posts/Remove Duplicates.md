---
title: Remove Duplicates from Sorted Array
date: 2024-02-10
tags:
  - Leetcode
---


[26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in nums.

Consider the number of unique elements of nums to be k, to get accepted, you need to do the following things:

Change the array nums such that the first k elements of nums contain the unique elements in the order they were present in nums initially. The remaining elements of nums are not important as well as the size of nums.
Return k.




1st Solution (Use Set)

```js
var removeDuplicates = function(nums) {

    //[1,1,2] -> [1,2,_]
    let result = new Array(nums.length).fill('_')
    let set = new Set(nums)

    let i = 0;
    for(const v of set.values()){
        nums[i] = v;
        i++;
    }
    
    return set.size
}

```


2nd Solution Use two pointer 

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {

    //[1,1,2] -> [1,2,_]

    if(nums.length === 0) return []
    
    let j = 1;
    for(let i = 1; i < nums.length; i++){
        if(nums[i - 1] !== nums[i]){
            nums[j] = nums[i]
            j++
        }
    }
    return j

}
```
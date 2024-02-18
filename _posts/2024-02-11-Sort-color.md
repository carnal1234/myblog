---
title: Sort Color
date: 2024-02-11
tags:
  - Leetcode

---
75. Sort Colors

Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.


1st Approach. Use Bubble sort to sort array.

Time Complexity: O(N2)
Auxiliary Space: O(1)

- does not require any additional memory space.
- stable sorting algorithm, meaning that elements with the same key value maintain their relative order in the sorted output.


```js

var sortColors = function(nums) {
    let j = 0;
    let swapped = false;
    
    for(let i = 0; i < nums.length; i++){
        swapped = false;
        for(j = 0; j < nums.length - i - 1; j++){
            if(nums[j] > nums[j+1]){
                let temp = nums[j];
                nums[j] = nums[j + 1];
                nums[j + 1] = temp;
                swapped = true;
            }
            
        }
        if(!swapped) break;
        

    }
};

  


```


2nd Approach. Dutch national flag algor

Use 3 pointer, low mid and high to keep track of array. < low is 0. Between low and mid is 1. > high is 2.

```js
var sortColors = function(nums) {
    let low = 0;
    let mid = 0;
    let high = nums.length - 1;

    for(; mid<= high; ){

        if(nums[mid] === 1){
            mid++;
        }else if(nums[mid] === 0){
            nums[mid] = nums[low];
            nums[low] = 0;
            low++;
            mid++;
        }else if(nums[mid] === 2){
            nums[mid] = nums[high];
            nums[high] = 2;
            high--;
        }

        
    }
};

```
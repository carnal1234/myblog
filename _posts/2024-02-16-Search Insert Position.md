---
title: Search Insert Position
date: 2024-02-16
tags:
  - Leetcode

---

[35. Search Insert Position](https://leetcode.com/problems/search-insert-position/)



Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with `O(log n)` runtime complexity.

1st Solution:

Use Binary search to find target and return low index if not found


```js

var searchInsert = function(nums, target) {

//Check for special case

if(target < nums[0]) return 0;

if(target > nums[nums.length - 1]) return nums.length


let low = 0;

let high = nums.length - 1;

let mid = -1;

while(high >= low){

	mid = Math.floor((low + high) / 2);

	console.log(low, nums[low], mid, nums[mid], high, nums[high])

	if(nums[mid] === target) return mid;

  

	if(nums[mid] > target){ // Mid is 20 but target is 10

		high = mid - 1;

	}else{

		low = mid + 1;

	}

}

return low;

};
```



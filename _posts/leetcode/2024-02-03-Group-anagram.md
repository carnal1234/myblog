---
title: Group-anagrams
date: 2024-02-03
tags:
  - Leetcode
categories: Leetcode

---


49. Group-anagrams

Given an array of strings strs, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

Example 1:

Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
Example 2:

Input: strs = [""]
Output: [[""]]
Example 3:

Input: strs = ["a"]
Output: [["a"]]




1st Solution. Use sort to compare two string is anagram. Then use it as key

```js

let resultObj = {}
let result = []
for(let str of strs){
  let sorted_str = str.split("").sort().join("")
       
       if(!resultObj.hasOwnProperty(sorted_str)){
           resultObj[sorted_str] = [str]
        //   console.log(resultObj[sorted_str])
            // result[sorted_str].push(str)
       }else{
          resultObj[sorted_str].push(str)
       }
    }

    // console.log(resultObj)
    
    Object.values(resultObj).forEach(v => result.push(v))
    //console.log(result)
    return result



```


2nd solution. Create array of occurence based on ascii. Then iterate through string with the key as its occurence arr.

```js
let CharOccurence = function(str){
    
    let arr = Array(26).fill(0)
    
    let alphabet = 'a'
    
    for(let c of str){
        let index = c.charCodeAt(0) - 'a'.charCodeAt(0)
        arr[index]++;
    }
    return arr
}



let groupAnagrams_V2 = function(strs){
    
    let resultMap = new Map()
    
    for(let str of strs){
        let arr_occurence = CharOccurence(str).join('#')
         
        if(!resultMap.has(arr_occurence) ) {
            resultMap.set(arr_occurence, [str])
        }
        else {
            let r = resultMap.get(arr_occurence).concat(str)
            resultMap.set(arr_occurence, r)
        }
    }
    
    result = []
    for(const value of resultMap.values()){
        result.push(value)
    }
    return result
}
```


     
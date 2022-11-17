---
title: 两数之和
date: 2022-11-17 11:20:57
update: 2022-11-17 11:20:57
lang: zh
tags:
  - 
  - 
categories:
  - 
  - 
description: 
cover: 
keywords: 
---
[[toc]]

### 自己实现的
自己动手实现的
```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
function twoSum(nums, target) {
    const count = {}
    for (let i = 0; i < nums.length; i++) {
        const num = nums[i];
        if (count[num] === void 0) {
            count[num] = {
                sub: target - num,
                idx: i
            };
        }
        if (count[count[num].sub] !== void 0 && count[count[num].sub].idx !== i) {
            return [count[count[num].sub].idx, i]
        }
    }
    return []
}
```

### 别人实现的
leetcode上看见别人的实现,发现自己还得努力

```javascript
var twoSum = function(nums, target) {
    const map = new Map();
    for(let i = 0; i < nums.length; i++){
        const item = nums[i];
        if(map.has(item)){
            return [map.get(item), i]
        }
        map.set(target - item, i);
    }
};
```
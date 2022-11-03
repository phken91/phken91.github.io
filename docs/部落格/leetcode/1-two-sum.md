---
title: "1. Two Sum"
description: "#1 解題思路"
tags:
    - leetcode
    - easy
    - javascript
hide:
    - footer
---

# 1. Two Sum

## 問題敘述

循例先把問題的鏈接po出來: [1. Two Sum](https://leetcode.com/problems/two-sum/)

問題很簡單，就是從一個數組找到一個和的的組合。同時測試組也保證一定會有答案，所以在處理上就比較簡單（大概？）

先來看下範例 

## 例子 1

<pre>
輸入: nums = [2,7,11,15], target = 9
輸出: [0, 1]
答案解釋: 因為數組的第 <b><code>0</code></b> 個和第 <b><code>1</code></b> 個相和得到目標 <b><code>9</code></b>。
</pre>

## 例子 2

<pre>
輸入: nums = [3,2,4], target = 6
輸出: [1, 2]
</pre>

## 解答思路

根據題型，我們先來推導大致做法。我們需要對數組的做一個比對，比如`target = 6`，這裡我把數組的每個`value`拿出來減去`target`再搜尋一下數組有沒有符合的數字然後返回一個新的數組。

首先我提供一個基於`js`的方法來解這問題

### 暴力破解

```js
let twoSum = (nums, target) => {
    for(let i = 0; i < nums.length; i++) {
        let left = target - nums[i];
        let search = nums.findIndex((x, y) => x - left == 0 && y != i);
        if (search > -1) return [i, search];
    }
}
```

這方法是較為暴力的解法，如果在數組大小不大的情況下還行。但在實戰中，這方法的執行時間就會取決於數組的大小。那有沒有更好的方法呢？答案是有的，來看看下方的解法。

### Hash Table

```js
let twoSum = (nums, target) => {
    let hash = new Map();
    for(let i = 0; i < nums.length; i++) {
        const looking = target - nums[i];
        if (hash.has(looking)) {
            return [hash.get(looking), i]
        }

        hash.set(nums[i], i);
    }
}
```

這方法的好處是使用額外的空間去儲存已經被遍歷過的value，然後在下一個value被提取出來時能更快的進行比對、同時執行的速度也比暴力破解的速度更快。

可以參考兩種解法的速度比較（取自leetcode的submit結果）

|方法|時間|使用的記憶體|
|---|---|---|
|暴力破解|1266 ms|43.7 MB|
|Hash Table|126 ms| 46.1 MB|

#### 知識點
1. [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)
2. [Array.prototype.findIndex](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)
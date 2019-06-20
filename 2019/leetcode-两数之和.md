# leetcode-两数之和

## 题目
给定一个整数数组`nums`和一个目标值`target`，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。
你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。
**示例：**
```
	给定 nums = [2, 7, 11, 15], target = 9
	因为 nums[0] + nums[1] = 2 + 7 = 9
	所以返回 [0, 1]
```

## 解

### 第一次commit
> 自己的解法

两层遍历，第一层遍历记录fNum，然后第二层遍历查看加上fNum是不是等于`target`，如果等于`target`的话，直接把第一层和第二层的下标return出去。
````js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    for (let i = 0; i < nums.length; i++) {
        let fNum = nums[i];
        for (let j = i + 1; j < nums.length; j++) {
            let sNum = nums[j];
            if (fNum + sNum === target) {
               return [i, j];
            }
        }
    }
};
````

### 第二次commit
> 看过答案后，使用Map对象(实际上普通对象也可以)

一层遍历，在遍历的时候将数据以key=数字，value=数组的下标来保存。
````js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    let m = new Map();
    // 遍历
    for (let i = 0; i < nums.length; i++) {
        let fNum = nums[i];
        // 取到target与当前fNum的差
        let v = target - fNum;
        // m对象中是否有target与当前fNum的差，如果有的话直接return就可以了
        if (m.has(v)) {
            return [i, m.get(v)];
        }
        // 没有的话继续往m对象中添加数据
        m.set(nums[i], i);
    }
};
````

## 总结

这个计算可以使用两层遍历，也可以使用对象，通过查看target与当前fNum的差，是否在对象中存在来判断，如果存在的话直接return出去就可以了。



## 题目地址(1. 两数之和)

https://leetcode-cn.com/problems/two-sum

## 题目描述

```
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

示例:

给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

## 前置知识

- 哈希表

## 公司

- 字节
- 百度
- 腾讯
- adobe
- airbnb
- amazon
- apple
- bloomberg
- dropbox
- facebook
- linkedin
- microsoft
- uber
- yahoo
- yelp

## 思路

最容易想到的就是暴力枚举，我们可以利用两层 for 循环来遍历每个元素，并查找满足条件的目标元素。

伪代码：

```java
for(int i = 0; i < n; i++) {
  for(int j = 0; j < i;j ++){
    if (nums[i] + nums[j] == target) return [j, i]
  }
}
```

不过这样时间复杂度为 O(N^2)，空间复杂度为 O(1)，时间复杂度较高，我们要想办法进行优化。

这里我们可以增加一个 Map 记录已经遍历过的数字及其对应的索引值。这样当遍历一个新数字的时候就去 Map 里查询 **target 与该数的差值 diff 是否已经在前面的数字中出现过**。如果出现过，说明 diff + 当前数 = target，我们就找到了一组答案。

## 关键点

- 求和转换为求差
- 借助 Map 结构将数组中每个元素及其索引相互对应
- 以空间换时间，将查找时间从 O(N) 降低到 O(1)

## 代码

- 语言支持：JS, Go，CPP

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
const twoSum = function (nums, target) {
  const map = new Map();
  for (let i = 0; i < nums.length; i++) {
    const diff = target - nums[i];
    if (map.has(diff)) {
      return [map.get(diff), i];
    }
    map.set(nums[i], i);
  }
};
```

Go Code:

```go
func twoSum(nums []int, target int) []int {
	m := make(map[int]int)
	for i, _ := range nums {
		diff := target - nums[i]
		if j, ok := m[diff]; ok {
			return []int{i, j}
		} else {
			m[nums[i]] = i
		}
	}
	return []int{}
}
```

CPP Code:

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& A, int target) {
        unordered_map<int, int> m;
        for (int i = 0; i < A.size(); ++i) {
            int t = target - A[i];
            if (m.count(t)) return { m[t], i };
            m[A[i]] = i;
        }
        return {};
    }
};
```

**复杂度分析**

- 时间复杂度：$O(N)$
- 空间复杂度：$O(N)$

## **反思**

```cpp
unordered_map<int, int> m;
//map定义

m[A[i]] = i;
//map更新过程

/*
哈希表中 key：value（int：int）；
更新过程中向量中的值作为哈希表的key存入，value是值的索引；
这样做的原因后面会提到
*/

int t = target - A[i];
if (m.count(t)) return { m[t], i };
//判断是否存在符合条件的两个数
/*
t为target和当前遍历值的差；
m.count(t) 在哈希表m中检索是否存在key为t的条目，若有返回1；
由于count函数检索key，按照题目要求，若之前遍历的值中存在target和当前数值的差，则算法结束；
因此将之前遍历过的数用key存储，用count函数检索；
*/
/*
return {m[t],i} 是因为m[t]是与差值相同的数的索引，i是当前数的索引，因此这两个索引对应的数符合题目要求；
*/

```


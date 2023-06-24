---
title: "[编程算法]LeetCode算法题研究(一): 数组"
date: 2023-6-18 22:23:54
tags: [日常学习, LeetCode, 数组算法, Python]
categories: 编程算法
description: "[第28篇] 从本篇开始研究各种经典算法的Python解法，第一篇以数组开始。"
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/algorithm.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/28-Leetcode_algorithm_arrays.jpg
katex: true
---

# 前言

年初回家后到现在一篇新文章都没写，非常惭愧。最近面试发现对方问的最基本的算法问题都只能答上来个大概的思路，一操作就卡壳，意识到不刷刷算法题熟悉一下编程的基本功是很难找到工作了。所以打算在继续日语学习的同时每天抽点时间刷刷LeetCode算法题，"程序员"就得有点"程序员"的样子。

学习的目标是熟悉一下各种经典算法的Python解法，尤其是熟悉一下各种算法的基础写法，避免以后写出一些脱裤子放屁的代码贻笑大方。第一篇就以最经典的数组相关算法开始吧。

# 正文

## 1. 两数之和(<font color="#00dd00">简单</font>)

**题目要求：**

给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。你可以按任意顺序返回答案。

**示例 1：**

输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。

**我的解答思路：(暴力破解)**

看到题目的第一反应是用target数去依次减num列表中的数并查看结果是否与该项之后的某个数字相同，如果相同返回这两个数字的下标。时间复杂度$O(N^2)$, 空间复杂度$O(1)$。

```python
def twoSum(self, nums: List[int], target: int) -> List[int]:
    for i1,n1 in enumerate(nums):
        for i2,n2 in enumerate(nums[i1+1:],):# 对于每个数，从它后面那个数开始遍历剩下的数
            if n2 == target - n1: # 需要注意后面的数组的第0位是原数值的i1+1位，因此要加回
                return [i1, i1+i2+1]
```

执行用时：2348 ms, 在所有 Python3 提交中击败了36.38%的用户

内存消耗：16.8 MB, 在所有 Python3 提交中击败了22.35%的用户

**官方解法：(哈希表)**

创建一个哈希表，对于每一个 `x`，我们首先查询哈希表中是否存在 `target - x`，然后将 `x` 插入到哈希表中，即可保证不会让 `x` 和自己匹配。时间复杂度$O(N)$， 空间复杂度$O(N)$。

```python
def twoSum(self, nums: List[int], target: int) -> List[int]:
    hashtable = dict()
    for i, num in enumerate(nums):
        if target - num in hashtable:
            return [hashtable[target - num], i]
        hashtable[nums[i]] = i # 如果哈希表中没有结果，则将i的下标作为值存进这个键中
    return []
```

执行用时：48 ms, 在所有 Python3 提交中击败了63.32%的用户

内存消耗：17.5 MB, 在所有 Python3 提交中击败了5.09%的用户

## 26. 删除有序数组中的重复项(<font color="#00dd00">简单</font>)

**题目要求：**

给你一个 升序排列 的数组 nums ，请你 原地 删除重复出现的元素，使每个元素 只出现一次 ，返回删除后数组的新长度。元素的 相对顺序 应该保持 一致 。然后返回 nums 中唯一元素的个数。考虑 nums 的唯一元素的数量为 k ，你需要做以下事情确保你的题解可以被通过：

- 更改数组 nums ，使 nums 的前 k 个元素包含唯一元素，并按照它们最初在 nums 中出现的顺序排列。nums 的其余元素与 nums 的大小不重要。
- 返回 k 。

**示例 1：**

输入：nums = [1,1,2]
输出：2, nums = [1,2,_]
解释：函数应该返回新的长度 2 ，并且原数组 nums 的前两个元素被修改为 1, 2 。不需要考虑数组中超出新长度后面的元素。

**我的解答思路：**

因为题目给定不需要考虑数组长度和k后面的元素，且数组为升序，因此只需要将数组遍历一次，依次将大于前数的元素放在数组的前k项即可。因为数组本身是升序排列，即使数组完全没有重复元素也不会出现大于当前元素的元素被提前覆盖的情况。时间复杂度$O(N)$， 空间复杂度$O(1)$。

```python
def removeDuplicates(self, nums: List[int]) -> int:
    last_num = -inf
    k = 0
    for num in nums:
        if num > last_num:
            nums[k] = num
            last_num = num
            k += 1     
    return k
```

执行用时：52 ms, 在所有 Python3 提交中击败了35%的用户

内存消耗：17.3 MB, 在所有 Python3 提交中击败了28%的用户

**官方解法：(双指针)**

所谓的双指针就是用一快一慢两个指针记录上一个改变前的数和下一个要被比较的数，如果两数不同就给慢指针下一格赋上快指针的值，然后继续用快指针遍历数组。时间复杂度$O(N)$， 空间复杂度$O(1)$。

```python
def removeDuplicates(self, nums: List[int]) -> int:
    slow, fast = 0, 1
    while fast < len(nums):
        if nums[fast] != nums[slow]:
            slow = slow + 1
            nums[slow] = nums[fast]
        fast = fast + 1
    return slow + 1
```

执行用时：40 ms, 在所有 Python3 提交中击败了84.28%的用户

内存消耗：17.4 MB, 在所有 Python3 提交中击败了9.49%的用户

**对比研究之后发现我的解法和官方的双指针解法的主要速度差距在于`for循环`和`while循环`，在将`num`换成用`nums[i]`表示后，算法的表现就与双指针一致了。**

## 35. 搜索插入位置(<font color="#00dd00">简单</font>)

**题目要求：**

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。请必须使用时间复杂度为$O(\log N)$的算法。

**示例 :**

```
输入: nums = [1,3,5,6], target = 5
输出: 2
输入: nums = [1,3,5,6], target = 2
输出: 1
输入: nums = [1,3,5,6], target = 7
输出: 4
```

**我的解答思路：**

对于已经排序的数组，找到插入位置非常简单，但我不知道什么样的算法算是$O(\log N)$的时间复杂度，因此我做题的时候没有管这个要求，也能通过。时间复杂度$O(N)$， 空间复杂度$O(1)$。

```python
# 用while循环 执行40ms 超过60%
def searchInsert(self, nums: List[int], target: int) -> int:
    i = 0
    if nums[-1] < target:
        return len(nums)
    else:
        while nums[i] < target:
            i += 1
        return i
# 用for循环 执行48ms 超过20%
def searchInsert(self, nums: List[int], target: int) -> int:
    for i, num in enumerate(nums):
        if num >= target:
            return i
    return len(nums)
```

**官方解法：(二分法)**

看了官方题解才知道二分法可以更快找到插入位置，也是所谓的时间复杂度为$O(\log N)$的算法。

```python
    def searchInsert(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1 # 将左右下标定义到列表的两端
        while left <= right: 
            middle = left + (right - left) // 2 # 找到左右中间偏左的元素
            if nums[middle] == target: 
                return middle
            elif nums[middle] > target: # 如果中间元素大于目标值，说明目标在左半边
                right = middle - 1 # 中间值不是目标，因此可以把右边界-1
            else:
                left = middle + 1
        # 如果nums[middle] > target，元素应插入的位置是 middle，而循环结束时 left = middle
        # 如果nums[middle] < target，元素应插入的位置是 middle+1，而循环结束时 left = middle +1
        return left 
```

执行用时：36 ms, 在所有 Python3 提交中击败了80.35%的用户

内存消耗：16.7 MB, 在所有 Python3 提交中击败了24.41%的用户

[第28篇]


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

## 两数之和(<font color="#00dd00">简单</font>)

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

[第28篇]


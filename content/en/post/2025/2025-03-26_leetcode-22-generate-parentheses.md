---
title: Generate Parentheses
description: leetcode No.22
date: 2025-03-26
categories:
    - Development
tags:
---

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

Example 1:
Input: n = 3
Output: `["((()))","(()())","(())()","()(())","()()()"]`
Example 2:
Input: n = 1
Output: `["()"]`


## 1. Forthright Solution

```py
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        # check combine
        def process(sub_comb):
            res = {}
            for item in sub_comb:
                for index in range(len(item)+1):
                    if index == 0:
                        temp = ("()"+ item)
                    elif index == len(item):
                        temp = (item + "()")
                    else:
                        temp = (item[0:index] + "()" + item[index:])
                    if temp not in res:
                        res[temp] = 1
            return list(res.keys())

        if n == 1:
            return ["()"]
        sub_comb = self.generateParenthesis(n-1)
        return process(sub_comb)
```


## Research


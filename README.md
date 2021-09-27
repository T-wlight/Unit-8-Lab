## Title address (1014. Best combination of sightseeing)

https://leetcode-cn.com/problems/best-sightseeing-pair/

## Title Description

```

Given a positive integer array A, A[i] represents the rating of the ith sightseeing attraction, and the distance between two attractions i and j is j - i.

The score of a pair of sightseeing attractions (i < j) is (A[i] + A[j] + i - j): the sum of the ratings of the attractions minus the distance between them.

Returns the highest score a pair of sightseeing attractions can achieve.

Example.

Input: [8,1,5,2,6]
Output: 11
Explanation: i = 0, j = 2, A[i] + A[j] + i - j = 8 + 5 + 0 - 2 = 11

Hint.

2 <= A.length <= 50000
1 <= A[i] <= 1000


Translated with www.DeepL.com/Translator (free version)
```

## Pre-requisite knowledge

- Dynamic Planning

## Ideas

The easiest way to think is to combine two and two to find the largest, proper timeout, let's look at the code.

```python
class Solution:
    def maxScoreSightseeingPair(self, A: List[int]) -> int:
        n = len(A)
        res = 0
        for i in range(n - 1):
            for j in range(i + 1, n):
                res = max(res, A[i] + A[j] + i - j)
        return res
```

Let's think about how to optimize. In fact, we can iterate through the array and for each item `A[j] - j` of the array we go ahead and find the `maximum` A[i] + i (so that we can guarantee the maximum result).

We consider using dynamic programming to solve this problem, and we use dp[i] to denote the maximum value of `A[i] + i` for the first i items of the array A.

```python
class Solution:
    def maxScoreSightseeingPair(self, A: List[int]) -> int:
        n = len(A)
        dp = [float('-inf')] * (n + 1)
        res = 0
        for i in range(n):
            dp[i + 1] = max(dp[i], A[i] + i)
            res = max(res, dp[i] + A[i] - i)
        return res
```

As we actually found above, dp[i + 1] is only related to dp[i], which is a signal for spatial optimization. We can actually use a variable to record this instead of using an array unnecessarily, see below for the code.

## Key Points Analysis

- Space for Time
- dp space optimization

## Code

```python
class Solution:
    def maxScoreSightseeingPair(self, A: List[int]) -> int:
        n = len(A)
        pre = A[0] + 0
        res = 0
        for i in range(1, n):
            res = max(res, pre + A[i] - i)
            pre = max(pre, A[i] + i)
        return res
```

## Tips

Python code is more efficient if you use if else instead of max, so try it.

```python
class Solution:
    def maxScoreSightseeingPair(self, A: List[int]) -> int:
        n = len(A)
        pre = A[0] + 0
        res = 0
        for i in range(1, n):
            # res = max(res, pre + A[i] - i)
            # pre = max(pre, A[i] + i)
            res = res if res > pre + A[i] - i else pre + A[i] - i
            pre = pre if pre > A[i] + i else A[i] + i
        return res
```

**Complexity Analysis**

- Time complexity: $O(N)$
- Space complexity: $O(N)$


---
title: "Dynamic Programming and Related Leetcode Problems"
description: "."
pubDate: "Jan 14 2025"
heroImage: "/Fibonacci.png"
tags: ["Leetcode"]
---

# Dynamic Programming

Core concepts:

1. Subproblems _M_ that are overlapping/have duplicated parts
2. State transfer equation can be defined like *dp(_state_n_) = M(dp(_state_n-1_), dp(_state_n-2_))*. You need to know what is the state and what the options are when in this state to go to the next state.

A way to solve this kind of issue is to first draw out a recursion tree to visualize it. For example the classic Fibonacci sequence **f(n)=f(n-1)+f(n-2)** , the tree is like:

![image](/Fibonacci.png)

You can clearly see in this tree that there are a lot of subproblems that are calculated for more than onece when doing recursion. One way to simplify it is to use memoization to keep record of those value and doing a lookup before doing calculations to avoid multiple calculations for the same subproblem, this requries extra space. In this way, the time complexity can be reduced from _O(2^n)_ to _O(n)_ where n is the total number of subproblems.

We can use an array dp[] for the memoization, then initialize the base case _dp[0] = 0_, _dp[1] = 1_ , from bottom to up just keep calculating using _dp[i] = dp[i-1] + dp[i-2]_ in an iteration (i in [2:n]). Furthermore, to reduce the space complexity, we could just use two variabled to save the values of _dp[i-1]_ and _dp[i-2]_ and keep updating the two values when doing iteration.

In summary, the basic procedures to tackle such problem are as follows:

1. Define state, state must be the one with limited total number variable.
2. Define option list, which lead to state transfer.
3. Using _dp_ to define state transfer equation using mathematical induction.

Generally two common approach for iteration would be:

1. Top-down approach with recurrsion, remember to use an array `memo` to memorize along the way (`if memo[i] != special_value; return memo[i]`).
2. Bottom-up approach with iteration, this way is to build up the dp array from the base case.

To be noted that usually 2d dp table couples with bottom-up iteration, memoization array couples with top-down recurssion.

Some related Leetcode problems:

1.[Coin Change](https://leetcode.com/problems/coin-change/description/): In this case, the total amount _a_ so far is the state (_a_ must be less or equal than amount), the option _c_ is in the list of coin values _coins_, and the state transfer should be _dp[a] = min(dp[a-c]+1, dp[a])_ when the coin value is smaller or equal than _a_, which means by comparing the case of using the coin or not. Time complexity is _O(kn)_ where _k_ is the length of _coins_ and n is the amount, space complexity is _O(n)_.

2.[Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/description/): In this case the state is the current maximum length for this array item, the options are all the array items before this current item, so the state transfer should be _dp[i] = max(dp[i], dp[j] + 1)_ when _nums[j] <nums[i]_. The idea is similar to two pointers, the total time complexity is _O(n*n)_ , space complexity is _O(n)_ where n is the length of the array.

There's another method to reduce the time complexity to _O(n*logn)_ by instead of iterating through the whole list, we use a subsequence list _sub_ to store the result list, we keep replacing the maximum value that is larger then _nums[j]_ in _sub_ with _nums[j]_ by using **binary search**, in this way we only need to iterate through the whole array once while being able to maintain the result list.

3.[Russian Doll Envelopes](https://leetcode.com/problems/russian-doll-envelopes/description/): this is the case to display how we can decrease the dimensions of the problem by sorting and fixing one dimension.

4.[Distinct Subsequences](https://leetcode.com/problems/distinct-subsequences/): By analyzing the problem we could see the brute-force way is to list all the subsequences using backtrack and find the total number of subsequences which are equal to the target string. And by comparing the two string we will need two pointers. Why not minimize the subproblem, instead of comparing the whole string, we compare the substring, for the comparison of _rabbbit_ and _rabit_ there would be a lot of overlapping comparison of _r_ _ra_ _rab_ etc, which reminds of us to use dp. 

For _rabbbit_ and _rabit_ when i=j=0 we have two options (similar to backtrack), either we match s[0] and t[0] or not. So _dp(s[i], t[j]) = dp(s[i+1], t[j+1]) + d[(s[i+1], t[j]) when s[i] == t[j]_ otherwise _dp(s[i], t[j]) = dp(s[i+1], t[j])_. _dp(0,0) = dp(1,1) + dp(1, 0) = ..._. Finally we look at the base case, when _j == t.length_ which means we match all the charaters in t, we return 1. Else when we don't have enough characters in s to match t's rest, we return 0. To further optimize, coz we have a duplicate option _dp(s, i+1, t, j)_ we'll use a 2-d dp table to keep memory of dp[i][j] to decrease the time complexisty to _O(n*m)_. 

5.[Word Break](https://leetcode.com/problems/word-break/description/): Though it's not about getting a max/min value, but it's still about overlapping subproblems, we can use boolean dp array for memoization.

6.[Edit Distance](https://leetcode.com/problems/edit-distance/description/): Similar string related issue, we still use index i, j to iterate through the two strings from end to start, then dp[i][j] should be the smallest edit distance of word1[0:i] and word2[0:j], we move the index to the top to minimize the issue. 

7. [Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/description/): this problem is quite obvious to get the state transfer function and use dp to solve. (Could also use Dijkstra to solve it, but it's less efficient due to the use of PriorityQueue)

8. [Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/description/): using dp to solve this issue could reach _O(n*m)_ time complexity, which is better than other methods.


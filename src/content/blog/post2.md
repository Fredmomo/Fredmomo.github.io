---
title: "LeetCode Top Notes For Bookmarking"
description: "LeetCode top sharing notes that summarize common patterns with issue links to follow on."
pubDate: "Aug 15 2024"
heroImage: "/post_img.webp"
tags: ["Leetcode"]
---

1. [Two pointers](https://leetcode.com/discuss/study-guide/1688903/Solved-all-two-pointers-problems-in-100-days) 

	It includes merging, dividing, searching, sliding window and more. 
	
2. [Sliding Window Pattern](https://leetcode.com/discuss/interview-question/5622545/sliding-window-technique-patterns)

	It's particularly for sliding window, which includes four patterns:
	* Fixed window size k, in which you let right->(k, n) and do ops for arr[right-k] and arr[right] 
	* Dynamic Window size, in which you let left=0, right->(0, n), try to shrink the size by updating left pointer when condition met in a while loop while keeping right pointer moving
	* Caterpillar, same setting as dynamic, but you keep moving the left in a while loop until the condition met
	* expanding/shrinking window size based on conditions set to other data structure like the size of array or hashtable
3. 
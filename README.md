# Algorithm
algorithm demo from [https://github.com/xidui/algorithm-training](https://github.com/xidui/algorithm-training)

### Overview

* [Two Sum](#Two-Sum)
* [Add Two Numbers](#Add-Two-Numbers)
* [Longest Substring Without Repeating Characters](#Longest-Substring-Without Repeating-Characters)
* [Median of Two Sorted Arrays](#Median-of-Two-Sorted-Arrays)
* [ZigZag Conversion](#ZigZag Conversion)

Two Sum
---

Given an array of integers, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution.

Input: numbers={2, 7, 11, 15}, target=9
Output: index1=1, index2=2 


```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    var result = [];
    	for(var i = 0, len = nums.length; i < len; i++){
    		for(var j = i+1; j < len; j++){
    			if(target - nums[i] == nums[j]){
    				result.push(i+1);
    				result.push(j+1);
    				break;
    			}
    		}
    	}
    	return result;
};
```

16 / 16 test cases passed.

Status: Accepted

Runtime: 348 ms

Your runtime beats 39.62% of javascript submissions.

(from [https://leetcode.com/problems/two-sum/](https://leetcode.com/problems/two-sum/))

Add Two Numbers
---

You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
    var l3 = {},
        sum = 0,
        l3Bak = {},
        next1 = {},
        next2 = {};
    sum = l1.val + l2.val;
    l3 = new ListNode(sum % 10);
    sum = Math.floor(sum / 10);
    l3Bak = l3;
    next1 = l1.next;
    next2 = l2.next;
    while (next1 || next2 || sum !== 0) {
        sum = (next1 !== null ? next1.val : 0) + (next2 !== null ? next2.val : 0) + sum;
        l3Bak.next = new ListNode(sum % 10);
        sum = Math.floor(sum / 10);
        l3Bak = l3Bak.next;
        next1 = next1 ? next1.next : null;
        next2 = next2 ? next2.next : null;
    }

    return l3;
}
```
1555 / 1555 test cases passed.

Status: Accepted

Runtime: 296 ms

Your runtime beats 96.10% of javascript submissions.

(from [https://leetcode.com/problems/add-two-numbers/](https://leetcode.com/problems/add-two-numbers/))

Longest Substring Without Repeating Characters
---

Given a string, find the length of the longest substring without repeating characters. For example, the longest substring without repeating letters for "abcabcbb" is "abc", which the length is 3. For "bbbbb" the longest substring is "b", with the length of 1.

```js
var lengthOfLongestSubstring = function(s) {
    if (s === "") return 0;
    var res,
        current = 1,
        len = s.length,
        max = 1;

    for (var i = 1; i < len + 1; i++) {
        res = s.substr(i - current, current).indexOf(s.substr(i, 1));
        // console.log(str.indexOf());
        if (res > -1) {
            if (max < current) {
                max = current;
            }
            current -= res;

        } else {
            current++;
        }
    }

    return max

}
```
981 / 981 test cases passed.

Status: Accepted

Runtime: 232 ms

Your runtime beats 96.27% of javascript submissions.

(from [https://leetcode.com/problems/longest-substring-without-repeating-characters/](https://leetcode.com/problems/longest-substring-without-repeating-characters/))

Median of Two Sorted Arrays
---

There are two sorted arrays nums1 and nums2 of size m and n respectively. Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

```js
var findMedianSortedArrays = function(nums1, nums2) {
    var len1 = nums1.length,
        len2 = nums2.length,
        arr = [],
        iseven = !((len1 + len2) % 2),
        current1 = 0,
        current2 = 0,
        loop = Math.floor((len1 + len2) / 2) + 1;

    for (var i = 0; i < loop; i++) {
        if (current1 == len1) {
            arr.push(nums2[current2]);
            current2++;
            continue;
        }

        if (current2 == len2) {
            arr.push(nums1[current1]);
            current1++;
            continue;
        }

        if (nums1[current1] < nums2[current2]) {
            arr.push(nums1[current1]);
            current1++;
        } else {
            arr.push(nums2[current2]);
            current2++;
        }
    }
    return iseven ? (arr.pop() + arr.pop()) / 2 : arr.pop();
}
```
2079 / 2079 test cases passed.

Status: Accepted

Runtime: 300 ms

Your runtime beats 74.14% of javascript submissions.

(from [https://leetcode.com/problems/median-of-two-sorted-arrays/](https://leetcode.com/problems/median-of-two-sorted-arrays/))


ZigZag Conversion
---

The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility) 

    P   A   H   N
    A P L S I I G
    Y   I   R
And then read line by line: "PAHNAPLSIIGYIR"

```js
/**
 * @param {string} s
 * @param {number} numRows
 * @return {string}
 */
var convert = function(s, numRows) {
    var res = "",
        len = s.length; //总长度
    if (numRows == 1 || numRows == 0) return s;
    //外层循环判断第几行
    //内层循环判断行距
    for (var i = 0; i < numRows; i++) {
        var isUp = false;
        for (var j = i; j < len;) {
            res += s[j];
            if (i == 0) {
                j += 2 * (numRows - i - 1);
                continue;
            }
            if (i == numRows - 1) {
                j += 2 * i;
                continue;
            }
            if (isUp) {
                j += 2 * i;
                isUp = false;
            } else {
                j += 2 * (numRows - i - 1);
                isUp = true;
            }
        }
    }
    return res;
};
```
1158 / 1158 test cases passed.

Status: Accepted

Runtime: 188 ms

2079 / 2079 test cases passed.

Your runtime beats 91.00% of javascriptsubmissions.

(from [https://leetcode.com/problems/zigzag-conversion/](https://leetcode.com/problems/zigzag-conversion/))


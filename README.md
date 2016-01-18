# Algorithm
algorithm demo from [https://github.com/xidui/algorithm-training](https://github.com/xidui/algorithm-training)

##Two Sum
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

Run code 164 ms (from [https://leetcode.com/problems/two-sum/](https://leetcode.com/problems/two-sum/))

##Add Two Numbers
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
Run code 148 ms (from [https://leetcode.com/problems/add-two-numbers/](https://leetcode.com/problems/add-two-numbers/))

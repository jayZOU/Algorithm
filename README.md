# Algorithm
algorithm demo from https://github.com/xidui/algorithm-training

##Two Sum
Given an array of integers, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution.

Input: numbers={2, 7, 11, 15}, target=9
Output: index1=1, index2=2 

``` 
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

[78. Subsets](https://leetcode.com/problems/subsets/)

Given a set of distinct integers, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

Example:

Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]

## Solution

一个长度为n的数组的subset有 $2^n$ 个，因为对于数组中的每一个位置要么它属于subset，要么不属于subset

ps: 生成bitmask的简单方法：

```java
String bitmask = Integer.toBinaryString(i).substring(1);
```
**复杂度**
- 时间：$O(n \times 2^n)$
- 空间：$O(2^n)$

```java
class Solution {
    List<List<Integer>> res = new ArrayList<List<Integer>>();
    
    
    public List<List<Integer>> subsets(int[] nums) {
        
        create(nums, new boolean[nums.length], 0);
        return res;
    }
    
    public void create(int[] nums, boolean[] contains, int index) {
        
        if (nums.length == index) {
            List<Integer> cur = new ArrayList<>();
            for (int i=0; i<contains.length; i++){
                if (contains[i]) cur.add(nums[i]);
            }
            res.add(cur);
            return;
        }
        
        contains[index] = false;
        create(nums, contains, index + 1);
        contains[index] = true;
        create(nums, contains, index + 1);
    }
}

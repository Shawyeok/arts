## 137. Single Number II
Given a non-empty array of integers, every element appears three times except for one, which appears exactly once. Find that single one.

Note:

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

**Example 1:**
```
Input: [2,2,3,2]
Output: 3
```

**Example 2:**
```
Input: [0,1,0,1,0,1,99]
Output: 99
```

### Code
```java
class Solution {
  public int singleNumber(int[] nums) {
    int res = 0;
    for (int i = 0; i < 32; i++) {
      int x = 1 << i;
      int sum = 0;
      for (int j = 0; j < nums.length; j++) {
        if ((x & nums[j]) != 0) {
          sum++;
        }
      }
      res |= (sum % 3) << i;
    }

    return res;
  }
}
```

### Description
这道题由于缺乏经验，想了两三个小时都没有结果。

想过对数组求和然后对于3取模，但这个方案只适用于数值在(-3, 3)的情况，没什么意义。

以二进制的角度看数，对每一个bit位上面进行求和然后对3取模得到的二进制数就是结果，这个思路不错，但应该还有优化空间。

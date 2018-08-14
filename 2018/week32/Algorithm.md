## Two Sum
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

### Code
```
func twoSum(nums []int, target int) []int {
	table := make(map[int]int)
	for i, n := range nums {
		remain := target - n
		j, ok := table[remain]
		if ok {
			return []int{j, i}
		}
		table[n] = i
	}

	panic("Not found.")
}
```

### Description
首先想到的是两个for循环，不过这样复杂度为`O(n^2)`，肯定不是最优解。然后是想到加法的一些特性，例如：奇数+奇数=偶数、偶数+奇数=奇数等，不过因为这里只是一个加减的操作非常简单，通过判断整数的奇偶性反而会增加计算量，所以这个方法也不是一个好办法。最后还是看了官方提供的solution，通过引入一个映射表将复杂度降低到了`O(n)`，由于官方给的solution是用`java`语言写的，而我刚好在学习`golang`，所以用golang重写了一版。这里有一点好奇的是，为什么LeetCode对于算法的优劣判断完全是基于了时间复杂度而没有考虑所使用的空间复杂度呢？

### Links
- https://leetcode.com/problems/two-sum/description/
- https://golang.org/ref/spec#Index_expressions
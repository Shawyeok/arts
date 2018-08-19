## Minimum Size Subarray Sum
Given an array of n positive integers and a positive integer s, find the minimal length of a contiguous subarray of which the sum ≥ s. If there isn't one, return 0 instead.

**Example:**
```
Input: s = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: the subarray [4,3] has the minimal length under the problem constraint.
```

**Follow up:**

If you have figured out the `O(n)` solution, try coding another solution of which the time complexity is `O(n log n)`.

### Code
```golang
func minSubArrayLen(s int, nums []int) int {
	sum, j, mLen := 0, 0, len(nums)+1
	for i := range nums {
		sum += nums[i]

		for sum >= s {
			mLen = min(mLen, i-j+1)
      if mLen == 1 {
        return 1
      }
			sum -= nums[j]
			j++
		}
	}

	if mLen == len(nums)+1 {
		return 0
	}
  return mLen
}

func min(n int, m int) int {
	if n < m {
		return n
	}
	return m
}
```

### Description
**Go语言和Java/JavaScript语言的一些差异：**

不支持条件表达式，以及`nums[j++]`这种写法，只能拆成两行。

一开始想到的还是`土办法`，运行时间是96ms，通过在草稿上面演化模拟，想到了多记录一个坐标的方式，最后写出来的代码运行时间是12ms，然后看了提供的solution，代码简洁多了，并且运行时间也只有8ms，从最初的96ms到8ms，效率提升了12倍。

### Links
- https://golang.org/doc/faq#Does_Go_have_a_ternary_form

# [2905. 找出满足差值条件的下标 II](https://leetcode.cn/problems/find-indices-with-index-and-value-difference-ii)

[English Version](/solution/2900-2999/2905.Find%20Indices%20With%20Index%20and%20Value%20Difference%20II/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p>给你一个下标从 <strong>0</strong> 开始、长度为 <code>n</code> 的整数数组 <code>nums</code> ，以及整数 <code>indexDifference</code> 和整数 <code>valueDifference</code> 。</p>

<p>你的任务是从范围 <code>[0, n - 1]</code> 内找出&nbsp; <strong>2</strong> 个满足下述所有条件的下标 <code>i</code> 和 <code>j</code> ：</p>

<ul>
	<li><code>abs(i - j) &gt;= indexDifference</code> 且</li>
	<li><code>abs(nums[i] - nums[j]) &gt;= valueDifference</code></li>
</ul>

<p>返回整数数组 <code>answer</code>。如果存在满足题目要求的两个下标，则 <code>answer = [i, j]</code> ；否则，<code>answer = [-1, -1]</code> 。如果存在多组可供选择的下标对，只需要返回其中任意一组即可。</p>

<p><strong>注意：</strong><code>i</code> 和 <code>j</code> 可能 <strong>相等</strong> 。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums = [5,1,4,1], indexDifference = 2, valueDifference = 4
<strong>输出：</strong>[0,3]
<strong>解释：</strong>在示例中，可以选择 i = 0 和 j = 3 。
abs(0 - 3) &gt;= 2 且 abs(nums[0] - nums[3]) &gt;= 4 。
因此，[0,3] 是一个符合题目要求的答案。
[3,0] 也是符合题目要求的答案。
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums = [2,1], indexDifference = 0, valueDifference = 0
<strong>输出：</strong>[0,0]
<strong>解释：</strong>
在示例中，可以选择 i = 0 和 j = 0 。 
abs(0 - 0) &gt;= 0 且 abs(nums[0] - nums[0]) &gt;= 0 。 
因此，[0,0] 是一个符合题目要求的答案。 
[0,1]、[1,0] 和 [1,1] 也是符合题目要求的答案。 
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>nums = [1,2,3], indexDifference = 2, valueDifference = 4
<strong>输出：</strong>[-1,-1]
<strong>解释：</strong>在示例中，可以证明无法找出 2 个满足所有条件的下标。
因此，返回 [-1,-1] 。</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= n == nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= nums[i] &lt;= 10<sup>9</sup></code></li>
	<li><code>0 &lt;= indexDifference &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= valueDifference &lt;= 10<sup>9</sup></code></li>
</ul>

## 解法

<!-- 这里可写通用的实现逻辑 -->

## Solutions

**Solution 1: Two Pointers + Maintaining Maximum and Minimum Values**

We use two pointers $i$ and $j$ to maintain a sliding window with a gap of $indexDifference$, where $j$ and $i$ point to the left and right boundaries of the window, respectively. Initially, $i$ points to $indexDifference$, and $j` points to $0$.

We use $mi$ and $mx$ to maintain the indices of the minimum and maximum values to the left of pointer $j$.

When pointer $i$ moves to the right, we need to update $mi$ and $mx$. If $nums[j] \lt nums[mi]$, then $mi$ is updated to $j$; if $nums[j] \gt nums[mx]$, then $mx$ is updated to $j$. After updating $mi$ and $mx$, we can determine whether we have found a pair of indices that satisfy the condition. If $nums[i] - nums[mi] \ge valueDifference$, then we have found a pair of indices $[mi, i]$ that satisfy the condition; if $nums[mx] - nums[i] >= valueDifference$, then we have found a pair of indices $[mx, i]$ that satisfy the condition.

If pointer $i$ moves to the end of the array and we have not found a pair of indices that satisfy the condition, we return $[-1, -1]$.

The time complexity is $O(n)$, where $n$ is the length of the array. The space complexity is $O(1)$.

<!-- tabs:start -->

### **Python3**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```python
class Solution:
    def findIndices(
        self, nums: List[int], indexDifference: int, valueDifference: int
    ) -> List[int]:
        mi = mx = 0
        for i in range(indexDifference, len(nums)):
            j = i - indexDifference
            if nums[j] < nums[mi]:
                mi = j
            if nums[j] > nums[mx]:
                mx = j
            if nums[i] - nums[mi] >= valueDifference:
                return [mi, i]
            if nums[mx] - nums[i] >= valueDifference:
                return [mx, i]
        return [-1, -1]
```

### **Java**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```java
class Solution {
    public int[] findIndices(int[] nums, int indexDifference, int valueDifference) {
        int mi = 0;
        int mx = 0;
        for (int i = indexDifference; i < nums.length; ++i) {
            int j = i - indexDifference;
            if (nums[j] < nums[mi]) {
                mi = j;
            }
            if (nums[j] > nums[mx]) {
                mx = j;
            }
            if (nums[i] - nums[mi] >= valueDifference) {
                return new int[] {mi, i};
            }
            if (nums[mx] - nums[i] >= valueDifference) {
                return new int[] {mx, i};
            }
        }
        return new int[] {-1, -1};
    }
}
```

### **C++**

```cpp
class Solution {
public:
    vector<int> findIndices(vector<int>& nums, int indexDifference, int valueDifference) {
        int mi = 0, mx = 0;
        for (int i = indexDifference; i < nums.size(); ++i) {
            int j = i - indexDifference;
            if (nums[j] < nums[mi]) {
                mi = j;
            }
            if (nums[j] > nums[mx]) {
                mx = j;
            }
            if (nums[i] - nums[mi] >= valueDifference) {
                return {mi, i};
            }
            if (nums[mx] - nums[i] >= valueDifference) {
                return {mx, i};
            }
        }
        return {-1, -1};
    }
};
```

### **Go**

```go
func findIndices(nums []int, indexDifference int, valueDifference int) []int {
	mi, mx := 0, 0
	for i := indexDifference; i < len(nums); i++ {
		j := i - indexDifference
		if nums[j] < nums[mi] {
			mi = j
		}
		if nums[j] > nums[mx] {
			mx = j
		}
		if nums[i]-nums[mi] >= valueDifference {
			return []int{mi, i}
		}
		if nums[mx]-nums[i] >= valueDifference {
			return []int{mx, i}
		}
	}
	return []int{-1, -1}
}
```

### **TypeScript**

```ts
function findIndices(nums: number[], indexDifference: number, valueDifference: number): number[] {
    let [mi, mx] = [0, 0];
    for (let i = indexDifference; i < nums.length; ++i) {
        const j = i - indexDifference;
        if (nums[j] < nums[mi]) {
            mi = j;
        }
        if (nums[j] > nums[mx]) {
            mx = j;
        }
        if (nums[i] - nums[mi] >= valueDifference) {
            return [mi, i];
        }
        if (nums[mx] - nums[i] >= valueDifference) {
            return [mx, i];
        }
    }
    return [-1, -1];
}
```

### **...**

```

```

<!-- tabs:end -->
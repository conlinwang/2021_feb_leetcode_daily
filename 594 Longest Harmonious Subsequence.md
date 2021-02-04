# 594 Longest Harmonious Subsequence

We define a harmonious array as an array where the difference between its maximum value and its minimum value is **exactly** `1`.

Given an integer array `nums`, return *the length of its longest harmonious subsequence among all its possible subsequences*.

A **subsequence** of array is a sequence that can be derived from the array by deleting some or no elements without changing the order of the remaining elements.

**Example 1:**

```
Input: nums = [1,3,2,2,5,2,3,7]
Output: 5
Explanation: The longest harmonious subsequence is [3,2,2,2,3].

```

**Example 2:**

```
Input: nums = [1,2,3,4]
Output: 2

```

**Example 3:**

```
Input: nums = [1,1,1,1]
Output: 0

```

**Constraints:**

- `1 <= nums.length <= 2 * 104`
- `109 <= nums[i] <= 109`

python solution:

```python
class Solution:
    def findLHS(self, nums: List[int]) -> int:
        cnt = collections.Counter(nums)
        res = 0
        for key in cnt:
            if cnt[key + 1]:
                res = max(res, cnt[key + 1] + cnt[key])
        return res
```

Runtime: **312 ms**

Memory Usage: **16 MB**

cpp solution:

```cpp
class Solution {
public:
    int findLHS(vector<int>& nums) {
        unordered_map<int, int> cnt;
        int res = 0;
        for (auto i : nums)
            cnt[i]++;
        for (auto iter: cnt){
            if (cnt.count(iter.first-1) > 0)
                res = max(res, iter.second + cnt[iter.first-1]);
        }
        return res;
    }
};
```

Runtime: **60 ms**

Memory Usage: **39.9 MB**

T.C. O(N) or say 2N, 2 passes

S.C. O(N)
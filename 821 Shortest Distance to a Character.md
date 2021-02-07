# 821 Shortest Distance to a Character

Given a string `s` and a character `c` that occurs in `s`, return *an array of integers `answer` where* `answer.length == s.length` *and* `answer[i]` *is the shortest distance from* `s[i]` *to the character* `c` *in* `s`.

**Example 1:**

```
Input: s = "loveleetcode", c = "e"
Output: [3,2,1,0,1,0,0,1,2,2,1,0]

```

**Example 2:**

```
Input: s = "aaab", c = "b"
Output: [3,2,1,0]

```

**Constraints:**

- `1 <= s.length <= 104`
- `s[i]` and `c` are lowercase English letters.
- `c` occurs at least once in `s`.

python solution

```python
class Solution:
    def shortestToChar(self, s: str, c: str) -> List[int]:
        N = len(s)
        pre = N
        res = []
        for i, ch in enumerate(s):
            if ch == c:
                pre = i
                res.append(0)
            else:
                res.append(abs(i - pre))
        pre = -1
        for i in range(N-1, -1, -1):
            if s[i] == c:
                pre = i
            else:
                res[i] = min(res[i], abs(pre - i))
        return res
    # T.C. O(N); S.C. O(1) without counting the output
        
        target = set()
        for i, ch in enumerate(s):
            if ch == c:
                target.add(i)
        res = []
        for i, ch in enumerate(s):
            if ch == c:
                res.append(0)
            else:
                tmp = float('inf')
                for idx in target:
                    tmp = min(tmp, abs(i-idx))
                res.append(tmp)
        return res
    # T.C. O(N); S.C. O(N) without counting the output
```
# 524. Longest Word in Dictionary through Deleting

Given a string and a string dictionary, find the longest string in the dictionary that can be formed by deleting some characters of the given string. If there are more than one possible results, return the longest word with the smallest lexicographical order. If there is no possible result, return the empty string.

**Example 1:**

```
Input:
s = "abpcplea", d = ["ale","apple","monkey","plea"]

Output: 
"apple"

```

**Example 2:**

```
Input:
s = "abpcplea", d = ["a","b","c"]

Output: 
"a"

```

**Note:**

1. All the strings in the input will only contain lower-case letters.
2. The size of the dictionary won't exceed 1,000.
3. The length of all the strings in the input won't exceed 1,000.

python solution use duque

```python
class Solution:
    def findLongestWord(self, s: str, d: List[str]) -> str:
        if not s:
            return s
        res = ''
        for word in d:
            if word == s:
                return s
            W = deque(list(word))
            for i, ch in enumerate(s):
                if W and s[i] == W[0]:
                    W.popleft()
                if not W:
                    if len(res) < len(word) or \
                       (len(res) == len(word) and word < res):
                        res = word
                    break
        return res
```
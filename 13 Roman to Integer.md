# 13. Roman to Integer

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, `2` is written as `II` in Roman numeral, just two one's added together. `12` is written as `XII`, which is simply `X + II`. The number `27` is written as `XXVII`, which is `XX + V + II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`.
 Because the one is before the five we subtract it making four. The same
 principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9.
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90.
- `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer.

**Example 1:**

```
Input: s = "III"
Output: 3

```

**Example 2:**

```
Input: s = "IV"
Output: 4

```

**Example 3:**

```
Input: s = "IX"
Output: 9

```

**Example 4:**

```
Input: s = "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.

```

**Example 5:**

```
Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.

```

**Constraints:**

- `1 <= s.length <= 15`
- `s` contains only the characters `('I', 'V', 'X', 'L', 'C', 'D', 'M')`.
- It is **guaranteed** that `s` is a valid roman numeral in the range `[1, 3999]`.

python sol

sol (1)

```python
class Solution:
    def romanToInt(self, s: str) -> int:
	# T.C. O(N) S.C. O(N), forward thinking
        if not s:
            return 0
        
        s = collections.deque(list(s))
        res = 0
        lookup = {'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000}
        I_lookup = {'V': 4, 'X': 9}
        X_lookup = {'L': 40, 'C': 90}
        C_lookup = {'D': 400, 'M': 900}
        while s:
            cur = s.popleft()
            if not s or cur not in {'I', 'X', 'C'}:
                res += lookup[cur]
            else:
                if cur == 'I':
                    if s[0] in I_lookup:
                        cur = s.popleft()
                        res += I_lookup[cur]
                    else:
                        res += lookup[cur]
                elif cur == 'X':
                    if s[0] in X_lookup:
                        cur = s.popleft()
                        res += X_lookup[cur]
                    else:
                        res += lookup[cur]
                else:
                    if s[0] in C_lookup:
                        cur = s.popleft()
                        res += C_lookup[cur]
                    else:
                        res += lookup[cur]
        return res

```

sol (2)

```python
class Solution:
    def romanToInt(self, s: str) -> int:
	# T.C. O(N) S.C. O(1), backward thinking. I read the hint to get this
        if not s:
            return 0
        lookup = {'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000}
        cur_max, res = 0, 0
        for ch in s[::-1]:
            if lookup[ch] >= cur_max:
                cur_max = lookup[ch]
                res += lookup[ch]
            else:
                res -= lookup[ch]
        return res
```
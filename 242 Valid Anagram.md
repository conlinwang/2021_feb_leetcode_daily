# 242. Valid Anagram

Given two strings *s* and *t* , write a function to determine if *t* is an anagram of *s*.

**Example 1:**

```
Input: s = "anagram", t = "nagaram"
Output: true

```

**Example 2:**

```
Input: s = "rat", t = "car"
Output: false

```

**Note:**
You may assume the string contains only lowercase alphabets.

**Follow up:**
What if the inputs contain unicode characters? How would you adapt your solution to such case?

python solution

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        cnt = collections.Counter(s)
        for ch in t:
            if cnt[ch]:
                cnt[ch] -= 1
            else:
                return False
        return True
T.C. O(N)
S.C. S(N)
```

cpp solution

```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.size() != t.size()) return false;
        unordered_map<char, int> s_map, t_map;
        for (int i=0; i < s.size(); ++i){
            s_map[s[i]] ++;
            t_map[t[i]] ++;
        }
        return s_map == t_map;
    }
};
T.C. O(N)
S.C. S(N)
```

Happy Taiwan's Lunar New Year!!!
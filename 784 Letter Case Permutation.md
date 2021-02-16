# 784. Letter Case Permutation

Given a string S, we can transform every letter individually to be lowercase or uppercase to create another string.

Return *a list of all possible strings we could create*. You can return the output in **any order**.

**Example 1:**

```
Input: S = "a1b2"
Output: ["a1b2","a1B2","A1b2","A1B2"]

```

**Example 2:**

```
Input: S = "3z4"
Output: ["3z4","3Z4"]

```

**Example 3:**

```
Input: S = "12345"
Output: ["12345"]

```

**Example 4:**

```
Input: S = "0"
Output: ["0"]

```

**Constraints:**

- `S` will be a string with length between `1` and `12`.
- `S` will consist only of letters or digits.

python sol: DFS

```python
class Solution:
    def letterCasePermutation(self, S: str) -> List[str]:
        res = []
        N = len(S)
        def dfs(idx, cur):
            if idx == N:
                res.append(''.join(cur))
                return
            else:
                if S[idx].isdigit():
                    cur.append(S[idx])
                    dfs(idx+1, cur)
                    cur.pop()
                else:
                    cur.append(S[idx].upper())
                    dfs(idx+1, cur)
                    cur.pop()
                    cur.append(S[idx].lower())
                    dfs(idx+1, cur)
                    cur.pop()
                return 
        dfs(0, [])
        return res
```

BFS

```python
class Solution:
    def letterCasePermutation(self, S: str) -> List[str]:
        if S.isdigit():
            return [S]
        
        queue=collections.deque([])
        for i in range(len(S)):
            if S[i].isalpha():
                queue.append(i)

        visited={S}
        while queue:
            pos=queue.popleft()
            temp=[]
            for s in visited:
                if s[pos].isupper():
                    tempS=s[:pos]+s[pos].lower()+s[pos+1:]
                    if tempS not in visited:
                        temp.append(tempS)
                else:
                    tempS=s[:pos]+s[pos].upper()+s[pos+1:]
                    if tempS not in visited:
                        temp.append(tempS)
            for s in temp:
                visited.add(s)

        return list(visited)
```
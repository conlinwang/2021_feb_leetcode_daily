# 862. Shortest Subarray with Sum at Least K

Return the **length** of the shortest, non-empty, contiguous subarray of `A` with sum at least `K`.

If there is no non-empty subarray with sum at least `K`, return `-1`.

**Example 1:**

```
Input:A = [1], K = 1
Output:1

```

**Example 2:**

```
Input:A = [1,2], K = 4
Output:-1

```

**Example 3:**

```
Input:A = [2,-1,2], K = 3
Output:3

```

**Note:**

1. `1 <= A.length <= 50000`
2. `10 ^ 5 <= A[i] <= 10 ^ 5`
3. `1 <= K <= 10 ^ 9`

thinkings for solving this problem:

1. `1 <= A.length <= 50000`: this hint to me that the solution need to be O(N) or O(N log N) sort might be usable
2. at first I have no idea so always start with brute force solution and see what we can find to improve:

    ```python
    class Solution:
        def shortestSubarray(self, A: List[int], K: int) -> int:
            # brute force solution T.C. --> O(N^2); S.C. --> O(1)
            res = float('inf')
            N = len(A)
            for i in range(N):
                for j in range(i, N):
                    if sum(A[i : j+1]) >= K and j + 1 - i < res:
                        res = j + 1 - i
            if res == float('inf'): return -1
            return res

    ```

    the space complexity is O(1) looks goo, but time complexity is O(N^2) this is bad. So how can I improve?

    3. I see the summation there and I can use accumulated sum to help me

    ```python
    class Solution:
        def shortestSubarray(self, A: List[int], K: int) -> int:
            # accumulated sum method
            # T.C. O(N^2) S.C. O(N)
            acc = []
            cur, res = 0, float('inf')
            for i, a in enumerate(A):
                cur += a
                if cur >= K:
                    res = min(res, i + 1)
                for j in range(len(acc)-1, -1, -1):
                    if cur - acc[j] >= K:
                        res = min(res, i - j)
                        break
                acc.append(cur)
            if res == float('inf'): return -1        
            return res
    ```

    For each move in A, the inner for loop look back and see if there is possible subarray sum that is ≥ K. If YES, then bingo! 

    I fund the shortest subarray that can have subarray sum that is ≥ K, thus break the loop and move on. 

    If not, then it's ok still we move on and see the next element in A.

    One thing to notice is that IF, it is the subarray from the beginning that satisfy the condition I need to handle it separately with the if condition, since I didn't use padding.

    However, the time complexity is still O(N^2) for the inner for loop looking backward and the space complexity is now O(N), but it is better then the first one in average case.

    4. Now, if the accumulated sum can be a deque, then I only need to check the first element in the deque, while WITHOUT the first element in the deque the accumulated sum can still be ≥ K. then we won't need to keep the first element in the deque anymore. Use this idea we need a while loop to pop out the history accumulated sum and we discard the first one while WITHOUT the first element in the deque the accumulated sum can still satisfy the condition.

    5. However, since the accumulated sum might goes ups and down, we don't need to keep the non-increasing part in the deque. Therefore, we can use another while loop after to make sure the deque is a increasing deque.

    All these ideas comes with the last solution:

    ```python
    class Solution:
        def shortestSubarray(self, A: List[int], K: int) -> int:
            # T.C. O(N) S.C. O(N)
            acc = collections.deque([(0, -1)]) # use padding
            cur, res = 0, float('inf')
            for i, a in enumerate(A):
                cur += a    
                while acc and cur - acc[0][0] >= K:
                    res = min(res, i - acc[0][1])
                    acc.popleft()
                
                while acc and acc[-1][0] > cur:
                    acc.pop()
                acc.append((cur, i))
                
            if res == float('inf'): return -1
            return res
    ```
# 895. Maximum Frequency Stack (Hard)!

Implement `FreqStack`, a class which simulates the operation of a stack-like data structure.

`FreqStack` has two functions:

- `push(int x)`, which pushes an integer `x` onto the stack.
- `pop()`, which **removes** and returns the most frequent element in the stack.
    - If there is a tie for most frequent element, the element closest to the top of the stack is removed and returned.

**Example 1:**

```
Input: ["FreqStack","push","push","push","push","push","push","pop","pop","pop","pop"],
[[],[5],[7],[5],[7],[4],[5],[],[],[],[]]
Output: [null,null,null,null,null,null,null,5,7,5,4]
Explanation:
After making six .push operations, the stack is [5,7,5,7,4,5] from bottom to top.  Then:

pop() -> returns 5, as 5 is the most frequent.
The stack becomes [5,7,5,7,4].

pop() -> returns 7, as 5 and 7 is the most frequent, but 7 is closest to the top.
The stack becomes [5,7,5,4].

pop() -> returns 5.
The stack becomes [5,7,4].

pop() -> returns 4.
The stack becomes [5,7].

```

**Note:**

- Calls to `FreqStack.push(int x)` will be such that `0 <= x <= 10^9`.
- It is guaranteed that `FreqStack.pop()` won't be called if the stack has zero elements.
- The total number of `FreqStack.push` calls will not exceed `10000` in a single test case.
- The total number of `FreqStack.pop` calls will not exceed `10000` in a single test case.
- The total number of `FreqStack.push` and `FreqStack.pop` calls will not exceed `150000` across all test cases.

solution 1:

1. use priority queue to implement the max freq stack
    1. store [freq, num] in pq and map = {'num': [positions]}

    ```python
    class FreqStack:

        def __init__(self):
            self.h = []
            self.freq = collections.defaultdict(int)
            
        def push(self, x: int) -> None:
            N = len(self.h)
            self.freq[x] += 1
            heapq.heappush(self.h, (-self.freq[x], x, N))
            # print(self.freq)
            
        def pop(self) -> int:
            if not self.h:
                return
            
            res = [(heapq.heappop(self.h))]
            while self.h:
                tmp = heapq.heappop(self.h)
                if tmp[0] == res[-1][0]:
                    res.append(tmp)
                else:
                    heapq.heappush(self.h, tmp)
                    break
            if len(res) == 1:
                self.freq[res[0][1]] -= 1
                heapq.heappush(self.h, (float('inf'), 0, 0))
                return res[0][1]
            else:
                res_sort = sorted(res, key = lambda x : x[2])
                for r in res_sort[:-1]:
                    heapq.heappush(self.h, r)
                self.freq[res_sort[-1][1]] -= 1
                heapq.heappush(self.h, (float('inf'), 0, 0))
                return res_sort[-1][1]
    # Your FreqStack object will be instantiated and called as such:
    # obj = FreqStack()
    # obj.push(x)
    # param_2 = obj.pop()
    ```

    will time out QQ

    solution 2 use nested freq indexed stack

    ```python
    class FreqStack:

        def __init__(self):
            self.freqStack = []
            self.freq = collections.defaultdict(int)

        def push(self, x: int) -> None:
            self.freq[x] += 1
            if len(self.freqStack) < self.freq[x]:
                self.freqStack.append([x])
            else:
                self.freqStack[self.freq[x]-1].append(x)
                
        def pop(self) -> int:
            res = self.freqStack[-1].pop()
            if not self.freqStack[-1]:
                self.freqStack.pop()
            self.freq[res] -= 1
            return res
    # Your FreqStack object will be instantiated and called as such:
    # obj = FreqStack()
    # obj.push(x)
    # param_2 = obj.pop()
    ```

    I read someone's solution and understand there is nested freq indexed stack.

    leaned a new thing. A Good problem!!! it really challenged my thinkings

    worth to mark it down
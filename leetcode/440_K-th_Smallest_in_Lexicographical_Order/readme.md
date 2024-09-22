## 문제
Given two integers n and k, return the kth lexicographically smallest integer in the range [1, n].
 

## Example 1:
```
Input: n = 13, k = 2
Output: 10
Explanation:
The lexicographical order is [1, 10, 11, 12, 13, 2, 3, 4, 5, 6, 7, 8, 9],
so the second smallest number is 10.
```

## Example 2:
Input: n = 1, k = 1
Output: 1
 
## Constraints:
1 <= k <= n <= 109

# Solution
```
import java.util.*;
class Solution {
    public int findKthNumber(long n, long k) {
        long currentNumber = 1;
        long count = k-1;
        
        while (count > 0) {
            long steps = calculateSteps(currentNumber, n);
            if (steps <= count) {
                currentNumber++;
                count -= steps;
            } else {
                currentNumber *= 10;
                count--;
            }
        }

        /** Timeout occurred from test case 42
            
            while (count > 0) {
                if (currentNumber*10 <= n) {
                    currentNumber *= 10;

                } else if (currentNumber+1 > n){
                    long tmpNumber = currentNumber/10 + 1;
                    currentNumber = tmpNumber;

                } else if ((currentNumber+1)%10 == 0){
                    long tmpNumber = (currentNumber+1)/10;
                    while (tmpNumber % 10 == 0) {
                        tmpNumber /= 10;
                    }
                    currentNumber = tmpNumber;

                } else {
                    currentNumber++;
                }

                count--;
            }
        */

        return (int) currentNumber;
    }

    long calculateSteps(long current, long n) {
        long steps = 0;
        long first = current;
        long last = current;
        
        while (first <= n) {
            steps += Math.min(n+1, last+1) - first;
            first *= 10;
            last = last*10 + 9;
        }
        
        return steps;
    }
}
```

# 고려사항
### 1. String으로 값을 받아서 정렬 후 인덱스로 찾기

-> 메모리 초과

### 2. 숫자들을 트리 구조로 생각해서 찾기

-> 노드를 일일히 계산하기 때문에 찾아야하는 인덱스가 큰 경우 시간 초과

### 3. 2번 + 타겟이 되는 인덱스보다 작은 구간은 최대한 한 번에 계산

-> calculateSteps()

## Problem
Given a binary string s and a positive integer n, return true if the binary representation of all the integers in the range [1, n] are substrings of s, or false otherwise.

A substring is a contiguous sequence of characters within a string.

## Example1
>Input: s = "0110", n = 3    
Output: true

## Example2
>Input: s = "0110", n = 4    
Output: false

## Constraints
- 1 <= s.length <= 1000
- s[i] is either '0' or '1'.
- 1 <= n <= 10<sup>9</sup>

# Solution
```
import java.util.*;
class Solution {
    public boolean queryString(String s, int n) {
        if (n == 1) return s.contains("1");

        for (int i=2; i<=n; i++) {
            StringBuilder sb = new StringBuilder();
            int nBinaryInteger = i;

            while (nBinaryInteger != 1) {
                if (nBinaryInteger % 2 == 0) 
                    sb.append("0");
                else
                    sb.append("1");
                nBinaryInteger/=2;
            }
            sb.append("1");
            if (!s.contains(sb.reverse()))
                return false;
        }
        
        return true;
    }
}
```

# Reflection
- 시간복잡도가 O(n<sup>2</sup>)이라서 좀 비효율일 것 같았는데 생각보다 많이 안걸렸다.
- 다른 사람들은 `Integer.toBinaryString(int)`를 많이 사용했다.

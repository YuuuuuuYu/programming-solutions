## 문제
정수 4를 1, 2, 3의 합으로 나타내는 방법은 총 7가지가 있다. 

합을 나타낼 때는 수를 1개 이상 사용해야 한다.
- 1+1+1+1
- 1+1+2
- 1+2+1
- 2+1+1
- 2+2
- 1+3
- 3+1

정수 n이 주어졌을 때, n을 1, 2, 3의 합으로 나타내는 방법의 수를 구하는 프로그램을 작성하시오.

## 입력
첫째 줄에 테스트 케이스의 개수 T가 주어진다. 

각 테스트 케이스는 한 줄로 이루어져 있고, 정수 n이 주어진다. n은 양수이며 11보다 작다.

## 출력
각 테스트 케이스마다, n을 1, 2, 3의 합으로 나타내는 방법의 수를 출력한다.

## 예제 입력
```
3
4
7
10
```

## 예제 출력
```
7
44
274
```

# Solution
```
import java.io.*;
import java.util.*;

public class boj_9095 {
  public static void main(String[] args) throws Exception {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
      StringBuilder result = new StringBuilder();
      int T = Integer.parseInt(br.readLine());
      int count[] = new int[12];
      count[1] = 1;  // 1을 만드는 모든 경우의 수
      count[2] = 2;  // 2를 만드는 모든 경우의 수
      count[3] = 4;  // 3을 만드는 모든 경우의 수

      for (int i = 4; i <= 11; i++)
        count[i] = count[i-1] + count[i-2] + count[i-3];

      int n;
      for (int i = 0; i < T; i++) {
        n = Integer.parseInt(br.readLine());
        result.append(count[n]).append("\n");
      }

      System.out.println(result.toString());
  }
}
```

# 고려사항
- 1부터 4까지 나열하고 5를 만들어보니 13개가 나왔고 규칙이 보였음
- 점화식을 구체적으로 확인해보니 다음과 같음
  - f(x) = f(x-1) + f(x-2) + f(x-3), x>=4
  - f(x-1), 마지막에 1을 더하는 경우
  - f(x-2), 마지막에 2를 더하는 경우
  - f(x-3), 마지막에 3을 더하는 경우
  - 4부터 적용되는 이유는 1, 2, 3으로만 표현해야하기 때문

## 문제
2×n 크기의 직사각형을 1×2, 2×1 타일로 채우는 방법의 수를 구하는 프로그램을 작성하시오.

아래 그림은 2×5 크기의 직사각형을 채운 한 가지 방법의 예이다.
![그림 1](https://onlinejudgeimages.s3-ap-northeast-1.amazonaws.com/problem/11726/1.png)


## 입력
첫째 줄에 n이 주어진다. (1 ≤ n ≤ 1,000)

## 출력
첫째 줄에 2×n 크기의 직사각형을 채우는 방법의 수를 10,007로 나눈 나머지를 출력한다.

## 예제 입력
`9`

## 예제 출력
`55`

# Solution
```
import java.io.*;
import java.util.*;

public class boj_11726 {
  public static void main(String[] args) throws Exception {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
      int n = Integer.parseInt(br.readLine());
      int dp[] = new int[1001];
      dp[1] = 1;
      dp[2] = 2;

      for (int i = 3; i <= n; i++) {
        dp[i] = (dp[i-2]+dp[i-1]) % 10007;
      }
    
      System.out.println(dp[n]);
  }
}
```

# 고려사항
- 처음부터 DP인줄 알고 점화식을 써봤으나 케이스 하나를 지나쳐서 DFS로 전환
- 하지만 DFS라고 하기에는 너무 복잡해져서 다시 점화식을 써보니 DP가 맞았다

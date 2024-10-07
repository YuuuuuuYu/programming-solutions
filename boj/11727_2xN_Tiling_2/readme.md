## 문제
2×n 직사각형을 1×2, 2×1과 2×2 타일로 채우는 방법의 수를 구하는 프로그램을 작성하시오.

아래 그림은 2×17 직사각형을 채운 한가지 예이다.

![그림 1](https://onlinejudgeimages.s3-ap-northeast-1.amazonaws.com/upload/images/t2n2122.gif)

## 입력
첫째 줄에 n이 주어진다. (1 ≤ n ≤ 1,000)

## 출력
첫째 줄에 2×n 크기의 직사각형을 채우는 방법의 수를 10,007로 나눈 나머지를 출력한다.

## 예제 입력
`2`

## 예제 출력
`3`

# Solution
```
import java.io.*;

public class boj_11727 {
  public static void main(String[] args) throws Exception {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
      int n = Integer.parseInt(br.readLine());
      int dp[] = new int[1001];
      dp[0] = 1;
      dp[1] = 1;

      for (int i = 2; i <= n; i++)
        dp[i] = (2*dp[i-2]+dp[i-1]) % 10007;

      System.out.println(dp[n]);
  }
}
```

# 고려사항
- 기존 2x1, 1x2만 채우는 형식에서 2x2가 추가된 형태
- 따라서 마지막 타일 부분을 채우는 방법은
  - 1x2 2개로 채우기
  - 2x1 또는 2x2로 채우기

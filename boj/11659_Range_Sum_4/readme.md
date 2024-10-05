## 문제
수 N개가 주어졌을 때, i번째 수부터 j번째 수까지 합을 구하는 프로그램을 작성하시오.

## 입력
첫째 줄에 수의 개수 N과 합을 구해야 하는 횟수 M이 주어진다. 

둘째 줄에는 N개의 수가 주어진다. 

셋째 줄부터 M개의 줄에는 합을 구해야 하는 구간 i와 j가 주어진다.

수는 1,000보다 작거나 같은 자연수이다. 

## 출력
총 M개의 줄에 입력으로 주어진 i번째 수부터 j번째 수까지 합을 출력한다.

## 제한
- 1 ≤ N ≤ 100,000
- 1 ≤ M ≤ 100,000
- 1 ≤ i ≤ j ≤ N

## 예제 입력
```
5 3
5 4 3 2 1
1 3
2 4
5 5
```

## 예제 출력
```
12
9
1
```

# Solution
```
import java.io.*;
import java.util.*;

public class boj_11659 {
  public static void main(String[] args) throws Exception {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
      StringBuilder sb = new StringBuilder();
      StringTokenizer st = new StringTokenizer(br.readLine());
      int N = Integer.parseInt(st.nextToken());
      int M = Integer.parseInt(st.nextToken());

      int prefixSum[] = new int[100001];
      st = new StringTokenizer(br.readLine());

      for (int i = 1; i <= N; i++)
        prefixSum[i] = prefixSum[i-1]+Integer.parseInt(st.nextToken());

      for (int i = 0; i < M; i++) {
        st = new StringTokenizer(br.readLine());
        int start = Integer.parseInt(st.nextToken());
        int end = Integer.parseInt(st.nextToken());
        sb.append(prefixSum[end]-prefixSum[start-1]).append("\n");
      }

      System.out.println(sb);
  }
}
```

# 고려사항
- 누적합을 먼저 구한 후 해당 구간의 시작 끝부분만큼 계산하면 됨
- 시간을 더 줄이려고 했지만 비트 연산자 사용이 아닌 이상 모르겠다

## 문제
준규가 가지고 있는 동전은 총 N종류이고, 각각의 동전을 매우 많이 가지고 있다.

동전을 적절히 사용해서 그 가치의 합을 K로 만들려고 한다. 이때 필요한 동전 개수의 최솟값을 구하는 프로그램을 작성하시오.

## 입력
첫째 줄에 N과 K가 주어진다. (1 ≤ N ≤ 10, 1 ≤ K ≤ 100,000,000)

둘째 줄부터 N개의 줄에 동전의 가치 Ai가 오름차순으로 주어진다. 

(1 ≤ Ai ≤ 1,000,000, A1 = 1, i ≥ 2인 경우에 Ai는 Ai-1의 배수)

## 출력
첫째 줄에 K원을 만드는데 필요한 동전 개수의 최솟값을 출력한다.

## 예제 입력
```
10 4200
1
5
10
50
100
500
1000
5000
10000
50000
```

## 예제 출력
6

# Solution
```
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
  public static void main(String[] args) throws Exception {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
      StringTokenizer st = new StringTokenizer(br.readLine());
      int coinCnt = Integer.parseInt(st.nextToken());
      int target = Integer.parseInt(st.nextToken());
      int calcCnt = 0;
      
      int coin[] = new int[coinCnt];
      for (int i = 0; i < coinCnt; i++) {
        coin[i] = Integer.parseInt(br.readLine());
      }

      for (int coinSize = coin.length-1; target > 0; coinSize--) {
        int checkCoinCnt = target/coin[coinSize];
        calcCnt += checkCoinCnt;
        target -= checkCoinCnt*coin[coinSize];
      }
      
      System.out.println(calcCnt);
  }
}
```

# 고려사항
- 큰 동전부터 계산해서 나눌 수 있을만큼 나누고 해당 개수만큼 카운팅
- 타겟보다 큰 동전의 경우 checkCoinCnt가 0이기 때문에 따로 조건문이 필요 없음


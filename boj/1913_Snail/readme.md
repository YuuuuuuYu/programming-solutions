## 문제
홀수인 자연수 N이 주어지면, 다음과 같이 1부터 N2까지의 자연수를 달팽이 모양으로 N×N의 표에 채울 수 있다.    
|  |  |  |
|---|---|---|
| 9 | 2 | 3 |
| 8 | 1 | 4 |
| 7 | 6 | 5 |

|  |  |  |  |  |
|----|----|----|----|----|
| 25 | 10 | 11 | 12 | 13 |
| 24 | 9  | 2  | 3  | 14 |
| 23 | 8  | 1  | 4  | 15 |
| 22 | 7  | 6  | 5  | 16 |
| 21 | 20 | 19 | 18 | 17 |

N이 주어졌을 때, 이러한 표를 출력하는 프로그램을 작성하시오.    
또한 N2 이하의 자연수가 하나 주어졌을 때, 그 좌표도 함께 출력하시오.    
예를 들어 N=5인 경우 6의 좌표는 (4,3)이다.

## 입력
첫째 줄에 홀수인 자연수 N(3 ≤ N ≤ 999)이 주어진다.    
둘째 줄에는 위치를 찾고자 하는 N2 이하의 자연수가 하나 주어진다.

## 출력
N개의 줄에 걸쳐 표를 출력한다.    
각 줄에 N개의 자연수를 한 칸씩 띄어서 출력하면 되며, 자릿수를 맞출 필요가 없다.    
N+1번째 줄에는 입력받은 자연수의 좌표를 나타내는 두 정수를 한 칸 띄어서 출력한다.

## 예제 입력
```
7
35
```

## 예제 출력
```
49 26 27 28 29 30 31
48 25 10 11 12 13 32
47 24 9 2 3 14 33
46 23 8 1 4 15 34
45 22 7 6 5 16 35
44 21 20 19 18 17 36
43 42 41 40 39 38 37
5 7
```

# Solution
```
import java.io.*;
import java.util.*;

public class boj_1913 {
  public static void main(String[] args) throws Exception {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
      StringBuilder sb = new StringBuilder();
      int N = Integer.parseInt(br.readLine());
      int snail[][] = new int[N+1][N+1];
      int init_X = (N+1)/2;
      int init_Y = (N+1)/2;
      snail[init_X][init_Y] = 1;
    
      int target = Integer.parseInt(br.readLine());
      int target_X = init_X, target_Y = init_Y;
      int number = 2;  // 1은 초기화했으니 2부터 시작
      int moving = 0;
      int offset = 0;
      int step = 0;

      /**
      n(이동하는 방향의 단계?)이 주어졌을 때, 규칙은 다음과 같다.
          홀수 => (n+1)/2
          짝수 => n/2

          N=5일 때, 방향은 (위-우측-아래-좌측-위-우측-아래-좌측-위) 총 9번이다.
          마지막 9번째 방향일 때, 이동 횟수는 5번이지만 이동 횟수는 (N-1)을 넘을 수 없다.
              
                |    n    |   이동 횟수
          n%4=1 | 1, 5, 9 |  1, 3, 4
          n%4=2 | 2, 4    |  1, 3
          n%4=3 | 3, 6    |  2, 4
          n%4=0 | 4, 8    |  2, 4

      **/
      while (moving < N*N) {
        offset = step%2 == 0 ? step/2 : (step+1)/2;
        for (int i=0; i<offset; i++) {
          int direction = step%4;
          switch(direction) {
            case 1:  // 위
              init_X--;
              break;
            case 2:  // 우측
              init_Y++;
              break;
            case 3:  // 아래
              init_X++;
              break;
            default: // 좌측
              init_Y--;
              break;
          }

          snail[init_X][init_Y] = number++;
          if (target == snail[init_X][init_Y]) {
            target_X = init_X;
            target_Y = init_Y;
          }
          
          moving++;
          if (number > N*N) break;
        }
        
        step++;
        if (number > N*N) break;
      }

      for (int i = 1; i <= N; i++) {
        for (int j = 1; j <= N; j++) {
          sb.append(snail[i][j]).append(" ");
        }
        sb.append("\n");
      }

      sb.append(target_X).append(" ").append(target_Y);
      System.out.println(sb);
  }
}
```

# 고려사항
- 움직인 걸음 수`moving` 값으로 계산했는데 배열의 원소를 순차적으로 증가하는 값`number`을 넣는게 맞는 것 같다.
- 타겟 좌표가 1일때, 초기화를 했어야했는데 그 부분이 미흡했다.
- 초반엔 DP로 계산하려고 했으나, 생각해보니 N*N이 될 때까지 좌표를 규칙에 맞게 계산하면 되는 것이었다.

![그림 1](https://raw.githubusercontent.com/YuuuuuuYu/programming-solutions/refs/heads/main/boj/1913_Snail/image.png)

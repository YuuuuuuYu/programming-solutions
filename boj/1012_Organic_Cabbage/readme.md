## 문제
차세대 영농인 한나는 강원도 고랭지에서 유기농 배추를 재배하기로 하였다. 농약을 쓰지 않고 배추를 재배하려면 배추를 해충으로부터 보호하는 것이 중요하기 때문에, 한나는 해충 방지에 효과적인 배추흰지렁이를 구입하기로 결심한다. 이 지렁이는 배추근처에 서식하며 해충을 잡아 먹음으로써 배추를 보호한다. 특히, 어떤 배추에 배추흰지렁이가 한 마리라도 살고 있으면 이 지렁이는 인접한 다른 배추로 이동할 수 있어, 그 배추들 역시 해충으로부터 보호받을 수 있다. 한 배추의 상하좌우 네 방향에 다른 배추가 위치한 경우에 서로 인접해있는 것이다.

한나가 배추를 재배하는 땅은 고르지 못해서 배추를 군데군데 심어 놓았다. 배추들이 모여있는 곳에는 배추흰지렁이가 한 마리만 있으면 되므로 서로 인접해있는 배추들이 몇 군데에 퍼져있는지 조사하면 총 몇 마리의 지렁이가 필요한지 알 수 있다. 예를 들어 배추밭이 아래와 같이 구성되어 있으면 최소 5마리의 배추흰지렁이가 필요하다. 0은 배추가 심어져 있지 않은 땅이고, 1은 배추가 심어져 있는 땅을 나타낸다.
|1|1|0|0|0|0|0|0|0|0|
|---|---|---|---|---|---|---|---|---|---|
|0|1|0|0|0|0|0|0|0|0|
|0|0|0|0|1|0|0|0|0|0|
|0|0|0|0|1|0|0|0|0|0|
|0|0|1|1|0|0|0|1|1|1|
|0|0|0|0|1|0|0|1|1|1|


## 입력
입력의 첫 줄에는 테스트 케이스의 개수 T가 주어진다. 그 다음 줄부터 각각의 테스트 케이스에 대해   
첫째 줄에는 배추를 심은 배추밭의 가로길이 M(1 ≤ M ≤ 50)과 세로길이 N(1 ≤ N ≤ 50),  
그리고 배추가 심어져 있는 위치의 개수 K(1 ≤ K ≤ 2500)이 주어진다.     
그 다음 K줄에는 배추의 위치 X(0 ≤ X ≤ M-1), Y(0 ≤ Y ≤ N-1)가 주어진다.  
두 배추의 위치가 같은 경우는 없다.  

## 출력
각 테스트 케이스에 대해 필요한 최소의 배추흰지렁이 마리 수를 출력한다.

## 예제 입력
```
2
10 8 17
0 0
1 0
1 1
4 2
4 3
4 5
2 4
3 4
7 4
8 4
9 4
7 5
8 5
9 5
7 6
8 6
9 6
10 10 1
5 5
```

## 예제 출력
```
5
1
```

# Solution
```
import java.io.*;
import java.util.*;

public class boj_1012 {
  static StringTokenizer st;
  static int M, N, K;
  static int field[][];
  static int dx[] = { -1, 1, 0, 0 };
  static int dy[] = { 0, 0, -1, 1 };

  public static void main(String[] args) throws Exception {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    StringBuilder sb = new StringBuilder();
    int T = Integer.parseInt(br.readLine());

    for (int i = 0; i < T; i++) {
      st = new StringTokenizer(br.readLine());
      M = Integer.parseInt(st.nextToken());
      N = Integer.parseInt(st.nextToken());
      K = Integer.parseInt(st.nextToken());
      field = new int[M][N];
      for (int j = 0; j < K; j++) {
        st = new StringTokenizer(br.readLine());
        field[Integer.parseInt(st.nextToken())][Integer.parseInt(st.nextToken())] = 1;
      }

      int worms = 0;
      for (int j = 0; j < M; j++) {
        for (int k = 0; k < N; k++) {
          if (field[j][k] == 1) {
            dfs(j, k);
            worms++;
          }
        }
      }
      sb.append(worms).append("\n");
    }

    System.out.println(sb);
  }

  /**
   * 시작 지점부터 인접한 배추에 지렁이가 다녀감
   * 지렁이가 다녀간 곳은 0으로 처리
  */
  static void dfs(int y, int x) {
    field[y][x] = 0;
    
    for (int i = 0; i < 4; i++) {
      int nx = x + dx[i];
      int ny = y + dy[i];
      if (0 <= nx && nx < field[0].length && 0 <= ny && ny < field.length && field[ny][nx] == 1) {
        dfs(ny, nx);
      }
    }
    return;
  }
}
```

# 고려사항
- 상하좌우로 인접하기만 하면 그 구역에 지렁이 1마리로 충분함
- 따라서 배추가 있는 곳을 돌때, 인접한 배추들을 0으로 처리한다면  
  다음 루프 때 패스해서 인접 구역을 카운트할 수 있음

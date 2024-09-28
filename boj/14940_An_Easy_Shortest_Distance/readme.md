## 문제
지도가 주어지면 모든 지점에 대해서 목표지점까지의 거리를 구하여라.

문제를 쉽게 만들기 위해 오직 가로와 세로로만 움직일 수 있다고 하자.

## 입력
지도의 크기 n과 m이 주어진다. n은 세로의 크기, m은 가로의 크기다.(2 ≤ n ≤ 1000, 2 ≤ m ≤ 1000)

다음 n개의 줄에 m개의 숫자가 주어진다. 

0은 갈 수 없는 땅이고 1은 갈 수 있는 땅, 2는 목표지점이다. 입력에서 2는 단 한개이다.

## 출력
각 지점에서 목표지점까지의 거리를 출력한다. 

원래 갈 수 없는 땅인 위치는 0을 출력하고, 원래 갈 수 있는 땅인 부분 중에서 도달할 수 없는 위치는 -1을 출력한다.

## 예제 입력
```
15 15
2 1 1 1 1 1 1 1 1 1 1 1 1 1 1
1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
1 1 1 1 1 1 1 1 1 1 0 0 0 0 1
1 1 1 1 1 1 1 1 1 1 0 1 1 1 1
1 1 1 1 1 1 1 1 1 1 0 1 0 0 0
1 1 1 1 1 1 1 1 1 1 0 1 1 1 1
```

## 예제 출력
```
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15
2 3 4 5 6 7 8 9 10 11 12 13 14 15 16
3 4 5 6 7 8 9 10 11 12 13 14 15 16 17
4 5 6 7 8 9 10 11 12 13 14 15 16 17 18
5 6 7 8 9 10 11 12 13 14 15 16 17 18 19
6 7 8 9 10 11 12 13 14 15 16 17 18 19 20
7 8 9 10 11 12 13 14 15 16 17 18 19 20 21
8 9 10 11 12 13 14 15 16 17 18 19 20 21 22
9 10 11 12 13 14 15 16 17 18 19 20 21 22 23
10 11 12 13 14 15 16 17 18 19 20 21 22 23 24
11 12 13 14 15 16 17 18 19 20 0 0 0 0 25
12 13 14 15 16 17 18 19 20 21 0 29 28 27 26
13 14 15 16 17 18 19 20 21 22 0 30 0 0 0
14 15 16 17 18 19 20 21 22 23 0 31 32 33 34
```

# Solution
```
import java.io.*;
import java.util.*;

public class boj_14940 {  
    // 이동할 방향: 상, 하, 좌, 우
    static int[] dx = {-1, 1, 0, 0};
    static int[] dy = {0, 0, -1, 1};
    
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        StringBuilder result = new StringBuilder();
        int startX = -1, startY = -1;
        
        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());
        int map[][] = new int[n][m];
        int distance[][] = new int[n][m];
        
        for (int i = 0; i < n; i++) {
            st = new StringTokenizer(br.readLine());
            
            for (int j = 0; j < m; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
                distance[i][j] = -1;
                
                if (map[i][j] == 2) {
                    startX = i;
                    startY = j;
                }
            }
        }

        if (startX != -1 && startY != -1)
            bfs(n, m, map, distance, startX, startY);
        
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (map[i][j] == 0)
                    result.append("0 ");
                else
                    result.append(distance[i][j]).append(" ");
            }
            result.append("\n");
        }

        System.out.println(result.toString());
    }

    static void bfs(int n, int m, int[][] map, int[][] distance, int startX, int startY) {
        Queue<int[]> queue = new LinkedList<>();
        queue.offer(new int[]{startX, startY});
        distance[startX][startY] = 0; // 시작 지점의 거리는 0

        while(!queue.isEmpty()) {
            int[] current = queue.poll();
            int x = current[0];
            int y = current[1];

            for(int dir = 0; dir < 4; dir++) {
                int nx = x+dx[dir];
                int ny = y+dy[dir];

                if(nx >= 0 && nx < n && ny >= 0 && ny < m) {
                    if(map[nx][ny] != 0 && distance[nx][ny] == -1) {
                        distance[nx][ny] = distance[x][y]+1;
                        queue.offer(new int[]{nx, ny});
                    }
                }
            }
        }
    }
}
```

# 고려사항
- 각 좌표에서 타겟 좌표까지 계산하는 것보다 

  타겟 좌표에서 나머지 좌표로 거리 계산하는 것이 좋음

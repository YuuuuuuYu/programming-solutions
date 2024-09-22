## 문제
폴리오미노란 크기가 1×1인 정사각형을 여러 개 이어서 붙인 도형이며, 다음과 같은 조건을 만족해야 한다.

정사각형은 서로 겹치면 안 된다.

도형은 모두 연결되어 있어야 한다.

정사각형의 변끼리 연결되어 있어야 한다. 즉, 꼭짓점과 꼭짓점만 맞닿아 있으면 안 된다.

정사각형 4개를 이어 붙인 폴리오미노는 테트로미노라고 하며, 다음과 같은 5가지가 있다.

`ㅡ ㅁ ㄴ ㄹ ㅜ 패턴`

아름이는 크기가 N×M인 종이 위에 테트로미노 하나를 놓으려고 한다. 

종이는 1×1 크기의 칸으로 나누어져 있으며, 각각의 칸에는 정수가 하나 쓰여 있다.

테트로미노 하나를 적절히 놓아서 테트로미노가 놓인 칸에 쓰여 있는 수들의 합을 최대로 하는 프로그램을 작성하시오.

테트로미노는 반드시 한 정사각형이 정확히 하나의 칸을 포함하도록 놓아야 하며, 회전이나 대칭을 시켜도 된다.

## 입력
첫째 줄에 종이의 세로 크기 N과 가로 크기 M이 주어진다. (4 ≤ N, M ≤ 500)

둘째 줄부터 N개의 줄에 종이에 쓰여 있는 수가 주어진다. 

i번째 줄의 j번째 수는 위에서부터 i번째 칸, 왼쪽에서부터 j번째 칸에 쓰여 있는 수이다. 

입력으로 주어지는 수는 1,000을 넘지 않는 자연수이다.

## 출력
첫째 줄에 테트로미노가 놓인 칸에 쓰인 수들의 합의 최댓값을 출력한다.

## 예제 입력
```
5 5
1 2 3 4 5
5 4 3 2 1
2 3 4 5 6
6 5 4 3 2
1 2 1 2 1
```

## 예제 출력
`19`

# Solution
```
import java.io.*;
import java.util.*;

public class Main {  
    static int maxSum = 0;
    static int n, m;
    static int[][] tetromino;
    static int max = 0;
    static boolean[][] visited;

    // 이동할 방향: 상, 하, 좌, 우
    static int[] dx = {-1, 1, 0, 0};
    static int[] dy = {0, 0, -1, 1};

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        tetromino = new int[n][m];

        for (int i = 0; i < n; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < m; j++) {
                tetromino[i][j] = Integer.parseInt(st.nextToken());
                max = Math.max(max, tetromino[i][j]);
            }
        }
        visited = new boolean[n][m];

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                visited[i][j] = true;
                dfs(i, j, 1, tetromino[i][j]);
                visited[i][j] = false;
            }
        }

        System.out.println(maxSum);
    }

    static void dfs(int x, int y, int count, int sum) {
        // (현재 값 + 남은 값에서의 max)가 maxSum보다 작거나 같으면 중지
        if (sum + max*(4-count) <= maxSum) {
            return;
        }

        if (count == 4) {
            maxSum = Math.max(maxSum, sum);
            return;
        }

        for(int dir = 0; dir < 4; dir++) {
            int nx = x+dx[dir];
            int ny = y+dy[dir];

            if(0 <= nx && nx < n && 0 <= ny && ny < m && !visited[nx][ny]) {  
                // ㅜ 패턴
                if (count == 2) {    
                    visited[nx][ny] = true;
                    dfs(x, y, count+1, sum+tetromino[nx][ny]);
                    visited[nx][ny] = false;
                }

                // ㅡ ㅁ ㄴ ㄹ 패턴
                visited[nx][ny] = true;
                dfs(nx, ny, count+1, sum+tetromino[nx][ny]);
                visited[nx][ny] = false;
            }
        }
    }
}
```

# 고려사항
- x, y 좌표를 if문에서 바로 체크하지 말고 미리 계산 후에 계산한 값을 체크하기 `nx`, `ny`
- ㅜ 패턴의 경우 2번째에 돌때 다음 위치의 값은 합산하되

  위치는 현위치에서 다시 계산하면 ㅜ 패턴으로 계산 가능 `if count = 2`
- 남은 계산을 했을 때, `maxSum`보다 작거나 같은 경우는 계산 생략 
- 자주 참조하는 값은 `static`으로 두는게 좋을 것 같다

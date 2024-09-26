## 문제
신종 바이러스인 웜 바이러스는 네트워크를 통해 전파된다. 

한 컴퓨터가 웜 바이러스에 걸리면 그 컴퓨터와 네트워크 상에서 연결되어 있는 모든 컴퓨터는 웜 바이러스에 걸리게 된다.

예를 들어 7대의 컴퓨터가 <그림 1>과 같이 네트워크 상에서 연결되어 있다고 하자. 

1번 컴퓨터가 웜 바이러스에 걸리면 웜 바이러스는 2번과 5번 컴퓨터를 거쳐 3번과 6번 컴퓨터까지 전파되어 

2, 3, 5, 6 네 대의 컴퓨터는 웜 바이러스에 걸리게 된다. 

하지만 4번과 7번 컴퓨터는 1번 컴퓨터와 네트워크상에서 연결되어 있지 않기 때문에 영향을 받지 않는다.

![그림 1](https://onlinejudgeimages.s3-ap-northeast-1.amazonaws.com/upload/images/zmMEZZ8ioN6rhCdHmcIT4a7.png)

어느 날 1번 컴퓨터가 웜 바이러스에 걸렸다. 

컴퓨터의 수와 네트워크 상에서 서로 연결되어 있는 정보가 주어질 때, 

1번 컴퓨터를 통해 웜 바이러스에 걸리게 되는 컴퓨터의 수를 출력하는 프로그램을 작성하시오.

## 입력
첫째 줄에는 컴퓨터의 수가 주어진다. 

컴퓨터의 수는 100 이하인 양의 정수이고 각 컴퓨터에는 1번 부터 차례대로 번호가 매겨진다. 

둘째 줄에는 네트워크 상에서 직접 연결되어 있는 컴퓨터 쌍의 수가 주어진다. 

이어서 그 수만큼 한 줄에 한 쌍씩 네트워크 상에서 직접 연결되어 있는 컴퓨터의 번호 쌍이 주어진다.

## 출력
1번 컴퓨터가 웜 바이러스에 걸렸을 때, 1번 컴퓨터를 통해 웜 바이러스에 걸리게 되는 컴퓨터의 수를 첫째 줄에 출력한다.

## 예제 입력
```
7
6
1 2
2 3
1 5
5 2
5 6
4 7
```

## 예제 출력
`4`

# Solution
```
import java.io.*;
import java.util.*;

public class Main {
  static Node computer[];
  static boolean warmComputer[];
  
  static class Node {
    int key;
    List<Node> linkNode;
    
    Node(int key) {
      this.key = key;
      linkNode = new ArrayList<>();
    }
  }
  
  public static void main(String[] args) throws Exception {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
      int computerCnt = Integer.parseInt(br.readLine());
      computer = new Node[computerCnt+1];
      warmComputer = new boolean[computerCnt+1];

      for (int i = 1; i < computer.length; i++)
        computer[i] = new Node(i);
    
      int linkCnt = Integer.parseInt(br.readLine());
      StringTokenizer st;

      int com1, com2;
      for (int i = 0; i < linkCnt; i++) {
        st = new StringTokenizer(br.readLine());
        com1 = Integer.parseInt(st.nextToken());
        com2 = Integer.parseInt(st.nextToken());

        computer[com1].linkNode.add(computer[com2]);
        computer[com2].linkNode.add(computer[com1]);
      }

      dfs(1);

      int result = 0;
      for (int i = 2; i < warmComputer.length; i++) {
        if (warmComputer[i]) result++;
      }

      System.out.println(result);
  }

  static void dfs(int key) {
    warmComputer[key] = true;

    for (Node nextNode : computer[key].linkNode) {
      if (!warmComputer[nextNode.key])
        dfs(nextNode.key);
    }
  }
}
```

# 고려사항
- 방향이 정해져있지 않기 때문에 `linkNode`가 양방향으로 추가되어야함

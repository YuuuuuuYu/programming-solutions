## 문제
김진영이 듣도 못한 사람의 명단과, 보도 못한 사람의 명단이 주어질 때, 듣도 보도 못한 사람의 명단을 구하는 프로그램을 작성하시오.

## 입력
첫째 줄에 듣도 못한 사람의 수 N, 보도 못한 사람의 수 M이 주어진다. 

이어서 둘째 줄부터 N개의 줄에 걸쳐 듣도 못한 사람의 이름과, N+2째 줄부터 보도 못한 사람의 이름이 순서대로 주어진다. 

이름은 띄어쓰기 없이 알파벳 소문자로만 이루어지며, 그 길이는 20 이하이다. N, M은 500,000 이하의 자연수이다.

듣도 못한 사람의 명단에는 중복되는 이름이 없으며, 보도 못한 사람의 명단도 마찬가지이다.

## 출력
듣보잡의 수와 그 명단을 사전순으로 출력한다.

## 예제 입력
```
3 4
ohhenrie
charlie
baesangwook
obama
baesangwook
ohhenrie
clinton
```

## 예제 출력
```
2
baesangwook
ohhenrie
```

# Solution
```
import java.io.*;
import java.util.*;

public class Main {
  public static void main(String[] args) {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
      List<String> people = new ArrayList<>();

      try {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int input1 = Integer.parseInt(st.nextToken());
            int input2 = Integer.parseInt(st.nextToken());
            Set<String> unheard = new HashSet<>();
            int cnt = 0;

            while(input1-- > 0) {
              String name = br.readLine();
              unheard.add(name);
            }
            
            while(input2-- > 0) {
              String name = br.readLine();
              if (unheard.contains(name)) {
                people.add(name);
                cnt++;
              }   
            }

            Collections.sort(people);
            StringBuilder result = new StringBuilder();
            result.append(cnt).append("\n");
        
            for (String person: people) {
              result.append(person).append("\n");
            }

            System.out.println(result.toString());
      } catch(IOException e) {}
  }
}
```

# 고려사항
- Set을 사용하지 않고 StringBuilder에 바로 넣어서 하려했지만 sort를 해야하는 문제가 있음
- 모든 입력을 String 배열에 넣고 sort 후에 중복되는 부분 찾는 것도 좋은 방법

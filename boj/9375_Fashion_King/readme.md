## 문제
해빈이는 패션에 매우 민감해서 한번 입었던 옷들의 조합을 절대 다시 입지 않는다. 

예를 들어 오늘 해빈이가 안경, 코트, 상의, 신발을 입었다면, 

다음날은 바지를 추가로 입거나 안경대신 렌즈를 착용하거나 해야한다. 

해빈이가 가진 의상들이 주어졌을때 과연 해빈이는 알몸이 아닌 상태로 며칠동안 밖에 돌아다닐 수 있을까?

## 입력
첫째 줄에 테스트 케이스가 주어진다. 테스트 케이스는 최대 100이다.

각 테스트 케이스의 첫째 줄에는 해빈이가 가진 의상의 수 n(0 ≤ n ≤ 30)이 주어진다.

다음 n개에는 해빈이가 가진 의상의 이름과 의상의 종류가 공백으로 구분되어 주어진다. 같은 종류의 의상은 하나만 입을 수 있다.

모든 문자열은 1이상 20이하의 알파벳 소문자로 이루어져있으며 같은 이름을 가진 의상은 존재하지 않는다.

## 출력
각 테스트 케이스에 대해 해빈이가 알몸이 아닌 상태로 의상을 입을 수 있는 경우를 출력하시오.

## 예제 입력
```
2
3
hat headgear
sunglasses eyewear
turban headgear
3
mask face
sunglasses face
makeup face
```

## 예제 출력
```
5
3
```

## 힌트
첫 번째 테스트 케이스는 headgear에 해당하는 의상이 hat, turban이며

eyewear에 해당하는 의상이 sunglasses이므로

(hat), (turban), (sunglasses), (hat, sunglasses), (turban, sunglasses)로 총 5가지 이다.

# Solution
```
import java.io.*;
import java.util.*;

public class boj_9375 {
  public static void main(String[] args) throws Exception {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
      StringBuilder result = new StringBuilder();
      int testcase = Integer.parseInt(br.readLine());
      
      for (int i = 0; i < testcase; i++) {
        Map<String, Integer> costume = new HashMap<>();
        int n = Integer.parseInt(br.readLine());
        
        for (int j = 0; j < n; j++) {
          StringTokenizer st = new StringTokenizer(br.readLine());
          st.nextToken();  // 의상명은 생략
          String type = st.nextToken();

          costume.put(type, costume.getOrDefault(type, 0)+1);
        }

        // 각 의상 종류 개수+1을 곱함, ex1) hat, turban, 입지 않는 경우
        int combinations = 1;
        for (int count : costume.values()) {
            combinations *= count+1;
        }

        // 알몸인 경우는 없음
        combinations--;
        result.append(combinations).append("\n");
      }

      System.out.println(result);
  }
}
```

# 고려사항
- 의상명이 중요하지 않을거 같았음
- 입지 않는 경우도 하나의 경우로 바로 생각을 했다면 더 수월하게 풀었을 것

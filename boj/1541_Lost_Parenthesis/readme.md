## 문제
세준이는 양수와 +, -, 그리고 괄호를 가지고 식을 만들었다. 그리고 나서 세준이는 괄호를 모두 지웠다.

그리고 나서 세준이는 괄호를 적절히 쳐서 이 식의 값을 최소로 만들려고 한다.

괄호를 적절히 쳐서 이 식의 값을 최소로 만드는 프로그램을 작성하시오.

## 입력
첫째 줄에 식이 주어진다. 식은 ‘0’~‘9’, ‘+’, 그리고 ‘-’만으로 이루어져 있고, 가장 처음과 마지막 문자는 숫자이다. 

그리고 연속해서 두 개 이상의 연산자가 나타나지 않고, 5자리보다 많이 연속되는 숫자는 없다. 수는 0으로 시작할 수 있다. 

입력으로 주어지는 식의 길이는 50보다 작거나 같다.

## 출력
첫째 줄에 정답을 출력한다.

## 예제 입력
```
55-50+40
```

## 예제 출력
`-35`

# Solution
```
import java.io.*;
import java.util.*;

public class boj_1541 {
  public static void main(String[] args) throws Exception {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    String calculation[] = br.readLine().split("-");
    StringTokenizer st;
    int PNFlag = 1;
    int result = 0;
    
    for (int i=0; i<calculation.length; i++) {
      st = new StringTokenizer(calculation[i], "+");
      int sum = 0;
      while (st.hasMoreTokens()) {
        sum += Integer.parseInt(st.nextToken());
      }
      
      result += PNFlag*sum;
      PNFlag = -1;
    }

    System.out.println(result);
  }
}
```

# 후기
- `-`가 올 때, 최대한 값이 큰 상태에서 빼줘야한다.
- 첫 번째 숫자는 무조건 양수이므로, 그 뒤에 `-` 연산자가 있는 부분만 처리해주면 될 것 같다.

## 문제
비어있는 공집합 S가 주어졌을 때, 아래 연산을 수행하는 프로그램을 작성하시오.
- add x: S에 x를 추가한다. (1 ≤ x ≤ 20) S에 x가 이미 있는 경우에는 연산을 무시한다.
- remove x: S에서 x를 제거한다. (1 ≤ x ≤ 20) S에 x가 없는 경우에는 연산을 무시한다.
- check x: S에 x가 있으면 1을, 없으면 0을 출력한다. (1 ≤ x ≤ 20)
- toggle x: S에 x가 있으면 x를 제거하고, 없으면 x를 추가한다. (1 ≤ x ≤ 20)
- all: S를 {1, 2, ..., 20} 으로 바꾼다.
- empty: S를 공집합으로 바꾼다.

## 입력
첫째 줄에 수행해야 하는 연산의 수 M (1 ≤ M ≤ 3,000,000)이 주어진다.

둘째 줄부터 M개의 줄에 수행해야 하는 연산이 한 줄에 하나씩 주어진다.

## 출력
check 연산이 주어질때마다, 결과를 출력한다.

## 예제 입력
```
26
add 1
add 2
check 1
check 2
check 3
remove 2
check 1
check 2
toggle 3
check 1
check 2
check 3
check 4
all
check 10
check 20
toggle 10
remove 20
check 10
check 20
empty
check 1
toggle 1
check 1
toggle 1
check 1
```

## 예제 출력
```
1
1
0
1
0
1
0
1
0
1
1
0
0
0
1
0
```

# Solution
```
import java.io.*;
import java.util.*;

public class Main {
  public static void main(String[] args) {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
      boolean resultArray[] = new boolean[21];

      try {
        int cnt = Integer.parseInt(br.readLine());

        StringBuilder sb = new StringBuilder();
        while(cnt-->0) {
          String input = br.readLine();
          char command = input.charAt(0);
          switch(command) {
              case 'a':
                  if (input.charAt(1) == 'd') {
                      resultArray[toIntSecondArg(input, 4)] = true;
                  } else if (input.charAt(1) == 'l') {
                      Arrays.fill(resultArray, true);
                  }
                  break;
              case 'r':
                  resultArray[toIntSecondArg(input, 7)] = false;
                  break;
              case 'c':
                  sb.append(resultArray[toIntSecondArg(input, 6)] ? "1\n" : "0\n");
                  break;
              case 't':
                  if(resultArray[toIntSecondArg(input, 7)]) {
                      resultArray[toIntSecondArg(input, 7)] = false;
                  } else {
                      resultArray[toIntSecondArg(input, 7)] = true;
                  }
                  break;
              case 'e':
                  resultArray = new boolean[21];
                  break;
          }
        }

        System.out.print(sb.toString());
      } catch (IOException e) {}
  }

  static int toIntSecondArg(String str, int startIdx) {
    return Integer.parseInt(str.substring(startIdx, str.length()));
  }
}
```

# 고려사항
- x의 범위가 1~20 이고, 존재 유무만 체크하기 때문에 boolean 사용
- System print를 최대한 줄이기 위해 StringBuilder 사용
- 연산에 대한 분기를 시킬 때, char 타입으로 분기

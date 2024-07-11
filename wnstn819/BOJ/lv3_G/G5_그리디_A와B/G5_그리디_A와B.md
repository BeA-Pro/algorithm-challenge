## 🔗 문제 링크
[A와B]
https://www.acmicpc.net/problem/12904

## 💻 코드
```java
package 그리디.G5_12904_A와B;

import java.io.*;
import java.util.*;

public class Main {
    public static int N,M;
    public static void main(String[] args) throws IOException {
        //BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedReader br = new BufferedReader(new FileReader("src/input.txt"));
        StringTokenizer st = new StringTokenizer(br.readLine());
        StringBuilder s = new StringBuilder();
        StringBuilder t = new StringBuilder();

        s.append(st.nextToken());
        t.append(br.readLine());

        while(s.length() < t.length()){

            if(t.charAt(t.length()-1) == 'A'){
                t.deleteCharAt(t.length()-1);
            }else{
                t.deleteCharAt(t.length()-1);
                t.reverse();
            }
        }

        if(s.toString().contentEquals(t.toString())){
            System.out.println(1);
        }else{
            System.out.println(0);
        }





    }

}



```

## 📝 해설

S -> T로 바꾸려고 하면

뒤에 A가 오는 경우와 B가 오는 경우 2가지를 최대 1000자리까지 진행해야하므로 시간초과가 날 것으로 예상

T -> S로 바꾸는 것이 해결하기에 적합함
제일 뒷자리가 A일 경우에는 A만 제거
B일 경우에는 B를 제거하고 뒤집으면 되기 때문에 O(T의 길이)로 시간 초과가 나지 않는다.

문자열을 다룰 때 해당 인덱스를 제거하거나 뒤집는 경우에 Stringbuilder를 사용하면 간편하기 때문에 StringBuilder를 사용


요약하자면 StringBuilder를 사용하고 T -> S로 문제를 해결하면 된다.

그리디 문제라서 조금 더 복잡할 줄 알았는데 생각보다 간단했음.


## 📌 결과


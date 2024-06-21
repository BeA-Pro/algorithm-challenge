## 🔗 문제 링크
[메뉴리뉴얼](https://school.programmers.co.kr/learn/courses/30/lessons/72411)

## 💻 코드
```java
import java.util.*;
class Solution {
    Map<String, Integer> map = new HashMap<>();

    // 사람들이 시킨 메뉴들을 조합하여 가능한 모든 코스 메뉴를 만들기
    void cal(String s, StringBuilder sb,int cur_idx, Map<String, Boolean> visit){
        if(sb.length() >= 2 && !visit.containsKey(sb.toString())){
            String temp = sb.toString();
            visit.put(temp,true);
            if(map.containsKey(temp)){
                map.put(temp, map.get(temp) + 1);
            }else{
                map.put(temp,1);
            }
        }
        if(cur_idx == s.length()) return;
        
        sb.append(s.charAt(cur_idx));
        cal(s,sb,cur_idx+1,visit);

        sb.deleteCharAt(sb.length() - 1);
        cal(s,sb,cur_idx+1,visit);
    }
    
    
    public String[] solution(String[] orders, int[] course) {
        String[] answer = {};
       
        for(int i=0;i<orders.length;i++){
          // 중복된 값 방지
            Map<String, Boolean > visit = new HashMap<>();
            // 코스 메뉴는 사전 순이어야 하므로 시킨 메뉴를 사전 순으로 정렬
            char[] charArray = orders[i].toCharArray();
            Arrays.sort(charArray);
            cal(new String(charArray),new StringBuilder(),0, visit);
        }

        
        ArrayList<String> list = new ArrayList<>();
         for(int number : course){
            ArrayList<String> temp = new ArrayList<>();
            int cnt = 0;
            for (Map.Entry<String, Integer> entry : map.entrySet()) {
               
                if(entry.getKey().length() == number){
                    if(entry.getValue() == 1) continue;
                    if(entry.getValue() > cnt){
                        cnt = entry.getValue();
                        temp.clear();
                        temp.add(entry.getKey());
                    }else if(entry.getValue() == cnt) temp.add(entry.getKey());
                }
            }

            for(String s : temp){
                list.add(s);
            }
        }

        Collections.sort(list);
        answer = new String[list.size()];
        list.toArray(answer);
        return answer;
    }
}
```

## 📝 해설
이 문제는 로직 자체는 간단하지만 해당 언어의 구조체를 잘 활용해야 쉽게 풀 수 있는 문제이다.

`orders`의 길이는 20 이하이고 `orders`의 각 원소는 크기가 10 이하이다.
따라서 한 손님이 만들 수 있는 코스 요리의 경우의 수는 10! = 3,628,800이고 모든 손님의 수는 20명이므로 위 조건에서 만들 수 있는 모든 코스 요리 수를 시간복잡도 O(10!*20)에 계산 할 수 있다.  

로직은 다음과 같다.
  1. `orders` 배열을 돌면서 손님이 주문한 단품메뉴 조합에서 나올 수 있는 모든 경우를 찾아내고 그 수를 `map`(key : 가능한 코스 요리, value 주문 수)에 누적한다.(중복 허용X)
  2. `course`를 돌면서 `map` 중에서 `key`의 길이(코스 메뉴 길이)가 자신과 같은 값을 찾는다.
  3. 그들 중 `value`의 값(주문 된 횟수)이 1이 넘으며 가장 큰 값이면 `list`에 추가한다.
  4. `list`를 사전 순으로 정렬하여 리턴한다.

문제를 풀면서 `StringBuilder`나 `HashMap` 등 다양한 구조체를 사용해본 경험이 없어서 많이 어려웠다.
많이 연습하고 공부해야겠다.
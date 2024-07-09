## 🔗 문제 링크
[Dividing the Gold](https://www.acmicpc.net/problem/5954)

## 💻 코드
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class G3_DividingtheGold{
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        int [] coins = new int [n];

        int total = 0;
        int mod = 1000000;
        for(int i=0;i<n;i++){
            coins[i] = Integer.parseInt(br.readLine());
            total+=coins[i];
        }

        int max_sum = total/2;
        int[] count = new int [max_sum + 1];
        boolean[] dp = new boolean[max_sum + 1];
        count[0] = 1;
        dp[0] = true;
        for(int coin : coins){
            for(int i = max_sum; i>=coin; i--){
                if(dp[i-coin]) {
                    dp[i] = true;
                    count[i] = (count[i] + count[i - coin]) % mod;
                }
            }
        }

        int sum = 0;
        for(int i = max_sum; i>=0;i--) {
            if (dp[i]) {
                sum = i;
                break;
            }
        }

        System.out.println(total - sum*2);
        System.out.println(count[sum]);

    }
}

```

## 📝 해설

다이나믹 프로그래밍을 이용하여 차가 최소가 되도록 분할하는 문제입니다.
N의 최대 크기가 250이고 V[i]의 최댓값이 2500이므로 250*2500은 충분히 배열로 선언 할 수 있는 크기입니다.

```java
int max_sum = total/2;
int[] count = new int [max_sum + 1];
boolean[] dp = new boolean[max_sum + 1];
```
`max_sum`은 분할 할 경우 나올 수 있는 최댓값입니다.(total이 홀수일 경우는 최댓값 - 1);
`count[i]`는 분할하여 i가 나오는 경우의 수를 저장합니다.

```java
for(int coin : coins){
    for(int i = max_sum; i>=coin; i--){
        if(dp[i-coin]) {
            dp[i] = true;
            count[i] = (count[i] + count[i - coin]) % mod;
        }
    }
}
```
동전 하나를 집고 나올 수 있는 최댓값에서 부터 역순으로 순회하며 `coin` 하나를 이용하여 만들 수 있는 분할 값을 찾습니다. (정방향으로 순회 할 경우 한 동전이 중복되어 누적되므로 주의해야 합니다.)
만약 `i-coin`으로 분할 될 수 있다면 이는 즉 `coin`을 더한 `i`로도 분할 가능하다는 이야기 입니다.
이렇게 모든 `coin`에 대해 반복문을 돌면 `count[i]`에는 `coin`들을 둘로 나누어 나올 수 있는 분할 값(i)과 그 수(count[i])가 저장되게 됩니다.
`dp[i]`를 선언한 이유는 count[i]가 1000000인 경우 `mod`로 나누면 0이 되는데, count[i]가 1000000이 나올 수 없는 경우와 구분 짓기 위해서입니다.



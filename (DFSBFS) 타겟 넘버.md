# (DFS/BFS) 타겟 넘버

###### 문제 설명

n개의 음이 아닌 정수가 있습니다. 이 수를 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다. 예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.

```
-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3
```

사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
- 각 숫자는 1 이상 50 이하인 자연수입니다.
- 타겟 넘버는 1 이상 1000 이하인 자연수입니다.

##### 입출력 예

| numbers         | target | return |
| --------------- | ------ | ------ |
| [1, 1, 1, 1, 1] | 3      | 5      |



### 코드1

```java
import java.util.*;
class Solution {
    public int solution(int[] numbers, int target) {
        int answer = 0;
        Queue<Integer> que = new LinkedList<>();
        que.offer(0);
        for (int i = 0; i < numbers.length; i++) {
            for (int j = 0; j < Math.pow(2,i); j++) {
                int num = que.poll();
                que.offer(num + numbers[i]);
                que.offer(num - numbers[i]);
            }
        }
        while (!que.isEmpty()) {
            if (que.poll() == target) {
               answer++; 
            }
        }
        return answer;
    }
}
```

- queue를 이용한 BFS
- i(깊이)가 증가할 때마다 2의 배수로 너비가 증가함
- 깊이가 numbers.length인 모든 경우를 queue에 저장하고, target과 일치하는 값을 찾음



### 코드2

~~~java
class Solution {
    public int solution(int[] numbers, int target) {
        int answer = 0;
        answer = dfs(numbers, 0, 0, target);
        return answer;
    }
    int dfs(int[] numbers, int n, int sum, int target) {
        if(n == numbers.length) {
            if(sum == target) {
                return 1;
            }
            return 0;
        }
        return dfs(numbers, n + 1, sum + numbers[n], target) + dfs(numbers, n + 1, sum - numbers[n], target);
    }
}
~~~

- DFS / 재귀를 이용
- 깊이가 n 인( n == numbers.length) 값이 target이면 1을 리턴, 아니면 0리턴
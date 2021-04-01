# (정렬) H-Index

###### 문제 설명

H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다. 위키백과[1](https://programmers.co.kr/learn/courses/30/lessons/42747#fn1)에 따르면, H-Index는 다음과 같이 구합니다.

어떤 과학자가 발표한 논문 `n`편 중, `h`번 이상 인용된 논문이 `h`편 이상이고 나머지 논문이 h번 이하 인용되었다면 `h`의 최댓값이 이 과학자의 H-Index입니다.

어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
- 논문별 인용 횟수는 0회 이상 10,000회 이하입니다.

##### 입출력 예

| citations       | return |
| --------------- | ------ |
| [3, 0, 6, 1, 5] | 3      |

##### 입출력 예 설명

이 과학자가 발표한 논문의 수는 5편이고, 그중 3편의 논문은 3회 이상 인용되었습니다. 그리고 나머지 2편의 논문은 3회 이하 인용되었기 때문에 이 과학자의 H-Index는 3입니다.



### 코드

~~~java
import java.util.*;
class Solution {
    public int solution(int[] citations) {
        int answer = 0;
        int n = citations.length;
        Integer[] arr = Arrays.stream(citations).boxed().toArray(Integer[]::new);
        Arrays.sort(arr, Collections.reverseOrder());
        for (int i = 0 ; i < n ; i++){
            if((i+1)>=arr[i]){
                return arr[i];
            }
        }
        
        return 0;
    }
}
~~~

1. int 형 배열 citations를 내림차순으로 정렬해야 함

2. 일반적으로 int형 배열은 Collections.reverseOrder()를 사용할 수 없기 때문에 Integer형으로 변환하여 정렬해야 함

3. 기존의 citations 배열을 Integer형 배열으로 박싱하여 arr에 저장하여 정렬함

4. (i+1) >= arr[i]  

   - (i+1)개 이상의 논문이 arr[i]번 이상 인용된 경우

   - 예를 들어 {3,0,6,1,5} 인 경우, {6,5,3,1,0} 으로 정렬되고
   - (1)개 이상의 논문이 arr[0] (6번) 이상 인용 X
   - (2)개 이상의 논문이 arr[1] (5번) 이상 인용 X
   - (3)개 이상의 논문이 arr[2] (3번) 이상 인용 O

   - 따라서 (i+1) >= arr[i]  이 성립함
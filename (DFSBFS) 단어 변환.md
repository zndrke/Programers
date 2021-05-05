# (DFS/BFS) 단어 변환

###### 문제 설명

두 개의 단어 begin, target과 단어의 집합 words가 있습니다. 아래와 같은 규칙을 이용하여 begin에서 target으로 변환하는 가장 짧은 변환 과정을 찾으려고 합니다.

```
1. 한 번에 한 개의 알파벳만 바꿀 수 있습니다.
2. words에 있는 단어로만 변환할 수 있습니다.
```

예를 들어 begin이 "hit", target가 "cog", words가 ["hot","dot","dog","lot","log","cog"]라면 "hit" -> "hot" -> "dot" -> "dog" -> "cog"와 같이 4단계를 거쳐 변환할 수 있습니다.

두 개의 단어 begin, target과 단어의 집합 words가 매개변수로 주어질 때, 최소 몇 단계의 과정을 거쳐 begin을 target으로 변환할 수 있는지 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 각 단어는 알파벳 소문자로만 이루어져 있습니다.
- 각 단어의 길이는 3 이상 10 이하이며 모든 단어의 길이는 같습니다.
- words에는 3개 이상 50개 이하의 단어가 있으며 중복되는 단어는 없습니다.
- begin과 target은 같지 않습니다.
- 변환할 수 없는 경우에는 0를 return 합니다.

##### 입출력 예

| begin | target | words                                      | return |
| ----- | ------ | ------------------------------------------ | ------ |
| "hit" | "cog"  | ["hot", "dot", "dog", "lot", "log", "cog"] | 4      |
| "hit" | "cog"  | ["hot", "dot", "dog", "lot", "log"]        | 0      |



### 코드

~~~java
import java.util.*;
class Solution {
    class Word{
        int depth;
        String wrd;
        
        public Word(String wrd, int depth) {
            this.wrd = wrd;
            this.depth = depth;
        }
    }
    boolean canChangeWord(String w1, String w2) {
        int count = w1.length() - 1;
        for(int i = 0; i < w1.length(); i++) {
            if (w1.charAt(i) == w2.charAt(i)) {
                count--;
            }
        }
        if (count == 0) {
            return true;
        }
        else {
            return false;
        }
    }
    public int solution(String begin, String target, String[] words) {
        int answer = 0;
        Queue<Word> que = new LinkedList<>();
        que.offer(new Word(begin,0));
        
        while (!que.isEmpty()) {
            Word str = que.poll();
            for (int i = 0; i < words.length; i++) {
                if (str.wrd.equals(target)) {
                    return str.depth;
                }
                if ( str.depth > words.length) {
                    return 0;
                }
                if (canChangeWord(str.wrd, words[i])) {
                    Word W = new Word(words[i], str.depth + 1);
                    que.offer(W);
                }
            }
        }
        return 0;
    }
}
~~~

- 단어는 한번에 하나의 알파벳만 바꿀 수 있다. 따라서 몇 번 바꾸면 target 단어와 일치하는지 세기 위하여 BFS 알고리즘을 사용한다.



1. Word 클래스
   - BFS의 depth는 한번 변환을 거쳤을 때 만들 수 있는 단어를 의미
   - wrd는 저장된 단어를 의미
   - Word 클래스의 객체는 단어와 깊이를 함께 가짐



2. canChangeWord 메소드
   - 알파벳이 (length-1) 개 만큼 같다는 것은 한번 변환으로 만들 수 있음 을 나타냄
   - 따라서, 두 알파벳이 (length-1)개 일치하면 true 아니면 false 를 리턴



3. solution 메소드
   - BFS이기 때문에 큐를 사용함
   - 큐가 비게되는 것은 변환할 수 있는 단어가 없기 때문에 0을 리턴함
   - words의 길이를 초과하는 것도 변환이 불가능 함을 의미하므로 0을 리턴
   - target과 일치하는 단어가 나오면 그 단어의 depth를 리턴하면 됨
   - canChangeWord가 true이면 큐에 저장하면서 depth를 증가함


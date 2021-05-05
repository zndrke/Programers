# (DFS/BFS) 네트워크

###### 문제 설명

네트워크란 컴퓨터 상호 간에 정보를 교환할 수 있도록 연결된 형태를 의미합니다. 예를 들어, 컴퓨터 A와 컴퓨터 B가 직접적으로 연결되어있고, 컴퓨터 B와 컴퓨터 C가 직접적으로 연결되어 있을 때 컴퓨터 A와 컴퓨터 C도 간접적으로 연결되어 정보를 교환할 수 있습니다. 따라서 컴퓨터 A, B, C는 모두 같은 네트워크 상에 있다고 할 수 있습니다.

컴퓨터의 개수 n, 연결에 대한 정보가 담긴 2차원 배열 computers가 매개변수로 주어질 때, 네트워크의 개수를 return 하도록 solution 함수를 작성하시오.

##### 제한사항

- 컴퓨터의 개수 n은 1 이상 200 이하인 자연수입니다.
- 각 컴퓨터는 0부터 `n-1`인 정수로 표현합니다.
- i번 컴퓨터와 j번 컴퓨터가 연결되어 있으면 computers[i][j]를 1로 표현합니다.
- computer[i][i]는 항상 1입니다.

##### 입출력 예

| n    | computers                         | return |
| ---- | --------------------------------- | ------ |
| 3    | [[1, 1, 0], [1, 1, 0], [0, 0, 1]] | 2      |
| 3    | [[1, 1, 0], [1, 1, 1], [0, 1, 1]] | 1      |

##### 입출력 예 설명

예제 #1
아래와 같이 2개의 네트워크가 있습니다.
![image0.png](https://grepp-programmers.s3.amazonaws.com/files/ybm/5b61d6ca97/cc1e7816-b6d7-4649-98e0-e95ea2007fd7.png)

예제 #2
아래와 같이 1개의 네트워크가 있습니다.
![image1.png](https://grepp-programmers.s3.amazonaws.com/files/ybm/7554746da2/edb61632-59f4-4799-9154-de9ca98c9e55.png)



### 코드

```java
class Solution {
    boolean[] dfs(int[][] computers, int i, boolean[] visited) {
        visited[i] = true;
        
        for (int j = 0; j < computers.length; j++){
            if (i != j && computers[i][j] == 1 && visited[j] != true) {
                visited = dfs(computers, j, visited);
            }
        }
        return visited;
    }
    
    public int solution(int n, int[][] computers) {
        int answer = 0;
        boolean[] visited = new boolean[n];
        
        for (int i = 0; i < n; i++){
            if(visited[i] != true){
                visited = dfs(computers,i,visited);
                answer++;
            }
        }
        return answer;
    }
}
```

- visited가 true가 아닌 노드에서, 연결된 모든 노드를 방문하여 visited를 true로 만들고, answer을 증가함



1. 첫번째 for문(solution 메소드 안에)에서 모든 노드를 방문하면서 visited가 false인 노드를 dfs에 넣고 answer을 증가함

2. dfs 메소드에서는 

   1. 자신이 아닌 노드(i != j)
   2. 간선이 연결되어 있는 (computers[i][j]== 1)
   3. 아직 방문하지 않은 노드 (visited[i] != true)

   인 노드가 있으면 dfs를 다시 호출하여 방문함

   - 따라서, 간선이 연결된 모든 노드를 방문하게 되고 
   - 간선이 연결되지 않은 노드는 방문하지 않게 됨
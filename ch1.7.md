# Graph


## 遍历
### 无向图

#### DFS + visited (techdose)

### 有向图
#### DFS + visited (techdose，同无向图）

```java 
public class Solution {
    void countComponents(int n, int[][] edges) {
        Map<Integer, List<Integer>> graph = new HashMap<>();
        boolean[] visited = new boolean[n];
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                dfs(graph, i, visited);//visit all 
            }
        }
    }

    void dfs(Map<Integer, List<Integer>> graph, int curr, boolean[] visited) {
        visited[curr] = true;
        System.out.println(curr);
        for (int next : graph.get(curr)) {
            if (!visited[next]) {
                dfs(graph, next, visited);
            }
        }
    }
}

```

## 找环

### 无向图
#### DFS + visited + parent

```java
public class Solution {
    public boolean hasCycle(int n, int[][] edges) {
        List<List<Integer>> graph = new ArrayList<>();
        boolean[] visited = new boolean[n];
        return (dfs(graph, -1, 0, visited);
    }

    //return true if it is cyclic
    private boolean dfs(List<List<Integer>> graph, int parent, int current, boolean[] visited) {
        boolean res = false;
        visited[current] = true;
        for(int next : graph.get(current)) {
            if(next==parent) continue;//看见来时的路，莫回头
            if(visited[next]) return true;//find a cycle
            res = res || dfs(graph, current, next, visited);
            if(res) return true;//early stop
        }
        return res;
    }
}

```

#### DFS + color (techdose)
```java
//待加
```



### 有向图
#### DFS + visited (techdose)

```java
//
```
#### DFS + color 0/1/2

```java
public class Solution {
    public boolean hasCycle(int n, int[][] edges) {
        List<List<Integer>> graph = new ArrayList<>();
        return dfs(graph, 0, new int[n]);
    }

    private boolean dfs(List<List<Integer>> graph, int current, int[] color) {
        color[current] = 1;
        for (int next : graph.get(current)) {
            if (color[next] == 1) {
                return true;
            } else if (color[next] == 2) {
                //do nothing
            } else {
                boolean c = dfs(graph, next, color);
                if (c) return true;//early stop
            }
        }
        color[current] = 2;
        return false;
    }
}

```



## 拓扑排序
### 只针对DAG
#### BFS
```java

```

#### DFS

```java


```
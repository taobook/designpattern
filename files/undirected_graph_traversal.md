# Undirected Graph Traversal 
DFS + visited (td)
### Solution:

```java 
package tt.lab.algorithm.graph;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

class GraphTraversalDFS {
    public static void main(String[] args) {
        // Test cases
        System.out.println(new GraphTraversalDFS().countComponents(5, new int[][]{{0, 1}, {1, 2}, {3, 4}})); // Output: 2
        System.out.println(new GraphTraversalDFS().countComponents(5, new int[][]{{0, 1}, {1, 2}, {2, 3}, {3, 4}})); // Output: 1
    }

    public int countComponents(int n, int[][] edges) {
        int res = 0;
        Map<Integer, List<Integer>> graph = new HashMap<>();

        // Initialize the graph
        for (int i = 0; i < n; i++) {
            graph.put(i, new ArrayList<>());
        }

        // Add edges to the graph (undirected)
        for (int[] edge : edges) {
            graph.get(edge[0]).add(edge[1]);
            graph.get(edge[1]).add(edge[0]);
        }

        boolean[] visited = new boolean[n];

        // Visit each node and perform DFS if not visited
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                dfs(graph, i, visited);
                res++; // Increment the component count for each new DFS
            }
        }
        return res;
    }

    private void dfs(Map<Integer, List<Integer>> graph, int curr, boolean[] visited) {
        visited[curr] = true; // Mark current node as visited
        System.out.println(curr); // Optional: to visualize node visits

        // Visit all connected neighbors
        for (int next : graph.get(curr)) {
            if (!visited[next]) {
                dfs(graph, next, visited);
            }
        }
    }
}

```

The above implementation of Depth-First Search (DFS) to count the connected components in an undirected graph is correct and well-structured. It builds the graph using an adjacency list, and then it performs DFS to traverse each connected component, incrementing the result counter when a new component is discovered.

To summarize:

*   **Input**: The number of nodes (`n`) and a list of edges (`edges`).
*   **Output**: The number of connected components in the graph.
*   **Method**:
  *   Create an adjacency list to represent the graph.
  *   Use DFS to explore each unvisited node, marking all reachable nodes as visited.
  *   Count how many times a new DFS traversal is initiated (each time it signifies a new connected component).

### Example Outputs:

For `countComponents(5, new int[][]{{0, 1}, {1, 2}, {3, 4}})`:

*   The nodes form two separate components: `{0, 1, 2}` and `{3, 4}`, so the output is `2`.

For `countComponents(5, new int[][]{{0, 1}, {1, 2}, {2, 3}, {3, 4}})`:

*   All nodes are part of a single connected component, so the output is `1`.

### Performance:

*   **Time Complexity**: `O(n + e)`, where `n` is the number of nodes and `e` is the number of edges. This is because we need to visit each node and edge exactly once in the worst case.
*   **Space Complexity**: `O(n + e)` for storing the adjacency list and the `visited` array.



### Solution

```java
package tt.lab.algorithm.graph;

import java.util.ArrayList;
import java.util.List;

public class DetectDirectCycleColor {
    public static void main(String[] args) {
        // Test cases
        System.out.println(new DetectDirectCycleColor().hasCycle(5, new int[][]{{0, 1}, {0, 2}, {0, 3}, {1, 4}})); // false
        System.out.println(new DetectDirectCycleColor().hasCycle(5, new int[][]{{0, 1}, {1, 2}, {2, 3}, {3, 1}, {1, 4}})); // true
        System.out.println(new DetectDirectCycleColor().hasCycle(6, new int[][]{{0, 1}, {1, 2}, {2, 3}, {1, 3}, {1, 4}, {0, 4}, {4, 5}})); // false
    }

    public boolean hasCycle(int n, int[][] edges) {
        // Handle edge case for an empty graph
        if (n == 0) return false;

        // Initialize the graph as an adjacency list
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            graph.add(new ArrayList<>());
        }

        // Add edges to the graph
        for (int[] edge : edges) {
            graph.get(edge[0]).add(edge[1]);
        }

        // Initialize the color array to mark visitation states
        int[] color = new int[n];

        // Run DFS from each node that hasn't been fully processed yet
        for (int i = 0; i < n; i++) {
            if (color[i] == 0) {  // Only start DFS from unvisited nodes
                if (dfs(graph, i, color)) {
                    return true;  // If a cycle is found, return true
                }
            }
        }

        // If no cycle is found, return false
        return false;
    }

    // DFS method that returns true if a cycle is detected
    private boolean dfs(List<List<Integer>> graph, int node, int[] color) {
        color[node] = 1;  // Mark the current node as being visited

        // Explore all neighbors
        for (int neighbor : graph.get(node)) {
            if (color[neighbor] == 1) {
                // A cycle is detected if we revisit a node that is still being processed
                return true;
            }
            if (color[neighbor] == 0) {
                // Continue DFS if the node is unvisited
                if (dfs(graph, neighbor, color)) {
                    return true;  // If a cycle is detected in recursion, propagate it
                }
            }
        }

        // Mark the current node as fully processed
        color[node] = 2;
        return false;  // No cycle detected
    }
}

```

The above implementation for detecting cycles in a directed graph using DFS with a color marking system is well-structured and effective. Below, I will provide an overview of the code, some suggestions for improvement, and discuss the time and space complexity of the implementation.

### Overview of the Code

1.  **Graph Representation:**
    *   The graph is represented as an adjacency list using a `List<List<Integer>>`. This is an efficient way to store graphs, especially when dealing with sparse graphs.
2.  **Color Marking System:**
    *   The `color` array is used to track the state of each node:
        *   `0`: Node has not been visited.
        *   `1`: Node is currently being visited (part of the current DFS path).
        *   `2`: Node and all its descendants have been fully processed.
3.  **DFS Logic:**
    *   The `dfs` method explores each node. If it encounters a node that is currently being visited (`color[next] == 1`), it indicates a cycle.
    *   Nodes are marked as fully processed (`color[current] = 2`) once all their neighbors have been explored.


### Time and Space Complexity

*   **Time Complexity:**
    *   The time complexity of this algorithm is **O(V + E)**, where `V` is the number of vertices and `E` is the number of edges. Each vertex and edge is visited at most once.
*   **Space Complexity:**
    *   The space complexity is **O(V)** due to the `color` array and the recursion stack in the DFS.

### Conclusion

The latest implementation effectively detects cycles in a directed graph. 
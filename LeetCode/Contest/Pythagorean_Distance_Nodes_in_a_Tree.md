# Pythagorean Distance Nodes in a Tree

##  Problem Statement

You are given an integer `n` representing the number of nodes in a tree, numbered from `0` to `n-1`.

You are also given:
- A list `edges` of `n-1` undirected edges forming a tree
- Three distinct nodes `x`, `y`, and `z`

For any node `u` in the tree:
- `dx` = distance from `u` to `x`
- `dy` = distance from `u` to `y`
- `dz` = distance from `u` to `z`

A node `u` is called **special** if the three distances form a **Pythagorean Triplet**, i.e.:

```
a² + b² = c²
```

(after sorting the three distances)

Your task is to return the **number of special nodes**.

---

##  Input Format

- Integer `n` — number of nodes  
- 2D array `edges` of size `n-1`, where each edge is `[u, v]`  
- Integers `x`, `y`, `z` — the given nodes  

---

##  Output Format

- An integer representing the count of special nodes

---

##  Concepts Used

- Tree traversal
- Breadth First Search (BFS)
- Distance calculation in trees
- Pythagorean triplet validation
- Integer overflow handling

---

##  Key Insight

In a tree, the shortest distance from a node to another node can be computed using **BFS**.

Instead of calculating distances from every node (which would be inefficient), we:
- Run **BFS from node `x`**
- Run **BFS from node `y`**
- Run **BFS from node `z`**

This gives us the distance of **every node** from `x`, `y`, and `z` in just `O(n)` time.

---

##  Approach

1. Build an adjacency list from the given edges
2. Perform BFS from `x`, `y`, and `z` to get distance arrays
3. For each node `u`:
   - collect `{dx[u], dy[u], dz[u]}`
   - sort the three distances
   - check if `a² + b² == c²` (use `long long` to avoid overflow)
4. Count all such nodes

---

## 🧪 Example

### Input
```
n = 4
edges = [[0,1], [0,2], [0,3]]
x = 1, y = 2, z = 3

```
### Output
```
3
```


---

##  Dry Run

Tree structure:
```
          1
          |
          0
        /   \
       2     3

```

Distances for each node:

| Node | Distances (x, y, z) | Sorted | Special |
|-----|--------------------|--------|---------|
| 0   | 1, 1, 1            | 1,1,1  | ❌ No   |
| 1   | 0, 2, 2            | 0,2,2  | ✅ Yes  |
| 2   | 2, 0, 2            | 0,2,2  | ✅ Yes  |
| 3   | 2, 2, 0            | 0,2,2  | ✅ Yes  |

Total special nodes = **3**

---

##  C++ Code

```cpp
class Solution {
public:
    int specialNodes(
        int n,
        vector<vector<int>>& edges,
        int x,
        int y,
        int z
    ) {
        // Build adjacency list
        vector<vector<int>> adj(n);
        for (auto &e : edges) {
            adj[e[0]].push_back(e[1]);
            adj[e[1]].push_back(e[0]);
        }

        // BFS to compute distances from a source
        auto bfs = [&](int src) {
            vector<int> dist(n, -1);
            queue<int> q;
            q.push(src);
            dist[src] = 0;

            while (!q.empty()) {
                int u = q.front();
                q.pop();
                for (int v : adj[u]) {
                    if (dist[v] == -1) {
                        dist[v] = dist[u] + 1;
                        q.push(v);
                    }
                }
            }
            return dist;
        };

        // Distance arrays
        vector<int> dx = bfs(x);
        vector<int> dy = bfs(y);
        vector<int> dz = bfs(z);

        int count = 0;

        // Check each node
        for (int i = 0; i < n; i++) {
            vector<int> d = {dx[i], dy[i], dz[i]};
            sort(d.begin(), d.end());

            long long a = d[0], b = d[1], c = d[2];
            if (a * a + b * b == c * c) {
                count++;
            }
        }

        return count;
    }
};
```

### Complexity Analysis

Time Complexity: O(n)

Space Complexity: O(n)

### Takeaway

In trees, BFS is the fastest way to compute distances

Minimize BFS runs — here, only 3 are needed

Always use long long when squaring integers

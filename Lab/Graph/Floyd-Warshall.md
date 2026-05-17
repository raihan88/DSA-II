# Floyd-Warshall Algorithm

## Problem Description

Floyd-Warshall Algorithm is an all-pairs shortest path algorithm used to find the shortest distance between every pair of vertices in a weighted graph.

Unlike:

* BFS, which finds shortest path in unweighted graphs
* Dijkstra, which finds shortest path from one source
* Bellman-Ford, which also works from one source

Floyd-Warshall computes the shortest distance between all possible pairs of nodes.

The algorithm works for:

* Directed graphs
* Undirected graphs
* Graphs with negative edge weights

However, the graph must not contain a negative weight cycle.

In this implementation, the graph is represented using an adjacency matrix.

---

## Theory and Solution Intuition

The Floyd-Warshall Algorithm is based on **Dynamic Programming**.

The main idea is:

* Initially, the adjacency matrix contains direct edge distances.
* Then, every vertex is considered as an intermediate node (called `via` node).
* The algorithm checks whether passing through the intermediate node gives a shorter path.

Suppose we want to calculate the shortest path from node `i` to node `j`.

There are two possibilities:

* Use the current known shortest path
* Go through another intermediate node `via`

The update formula becomes:

dist[i][j] = \min(dist[i][j],\ dist[i][via] + dist[via][j])

If traveling through the intermediate node reduces the path cost, the distance is updated.

---

## Example Graph

Consider the following graph:

```text id="4sytrr"
        3
    0 ------> 1
    |         |
   5|         |1
    |         |
    v         v
    2 ------> 3
         2
```

Initial adjacency matrix:

```text id="7fh9l9"
      0    1    2    3

0     0    3    5   INF
1   INF    0  INF    1
2   INF  INF    0    2
3   INF  INF  INF    0
```

After applying Floyd-Warshall:

* Distance from `0 → 3` becomes `4`

because:

```text id="jlwmn3"
0 → 1 → 3 = 3 + 1 = 4
```

which is smaller than infinity.

---

## Step-by-Step Working Procedure

Initially:

* The adjacency matrix stores direct edge weights.
* If there is no direct edge between two nodes, distance is set to infinity (`1e8`).

The algorithm then performs three nested loops.

The outermost loop selects the intermediate node:

```cpp id="8y2dyk"
for(int via = 0; via < n; via++)
```

The next two loops traverse every pair of nodes `(i, j)`.

For every pair:

* Check whether the path through `via` is shorter.
* Update the distance if necessary.

This process continues until every node has been considered as an intermediate node.

---

## Floyd-Warshall Algorithm Code

```cpp id="6nqt35"
#include<bits/stdc++.h>
using namespace std;

void floydWarshall(vector<vector<int>> &dist){

    int n = dist.size();

    for(int via = 0; via < n; via++){

        for(int i = 0; i < n; i++){

            for(int j = 0; j < n; j++){

                // Avoid infinity overflow
                if(dist[i][via] != 1e8 &&
                   dist[via][j] != 1e8){

                    dist[i][j] = min(
                        dist[i][j],
                        dist[i][via] + dist[via][j]
                    );
                }
            }
        }
    }
}

int main(){

    int n;

    cout<<"Enter number of nodes: ";

    cin>>n;

    vector<vector<int>>dist(n, vector<int>(n));

    cout<<"Enter adjacency matrix:"<<endl;
    cout<<"Use 100000000 for INF"<<endl;

    for(int i = 0; i < n; i++){

        for(int j = 0; j < n; j++){

            cin>>dist[i][j];
        }
    }

    floydWarshall(dist);

    cout<<"Shortest Distance Matrix:"<<endl;

    for(int i = 0; i < n; i++){

        for(int j = 0; j < n; j++){

            if(dist[i][j] == 1e8)
                cout<<"INF ";
            else
                cout<<dist[i][j]<<" ";
        }

        cout<<endl;
    }
}
```

---

## Code Explanation

The graph is represented using a 2D adjacency matrix:

```cpp id="d06lj6"
vector<vector<int>> dist;
```

Each cell:

```text id="4s89kh"
dist[i][j]
```

stores the shortest known distance from node `i` to node `j`.

Initially:

* Direct edge weights are stored
* Unreachable paths are assigned `1e8`

The main update step is:

```cpp id="cslkhz"
dist[i][j] = min(
    dist[i][j],
    dist[i][via] + dist[via][j]
);
```

This checks whether using the intermediate node produces a shorter path.

The condition:

```cpp id="sp14bq"
if(dist[i][via] != 1e8 &&
   dist[via][j] != 1e8)
```

prevents overflow caused by adding infinity values.

---

## Dynamic Programming Concept

Floyd-Warshall follows Dynamic Programming because:

* Solutions of smaller subproblems are reused
* Shortest paths are gradually improved

At every stage:

* The algorithm decides whether including a new intermediate node improves the answer.

---

## Time Complexity

The time complexity of Floyd-Warshall Algorithm is:

```text id="0gphm2"
O(V³)
```

Where:

* `V` = Number of vertices

This complexity comes from the three nested loops.

---

## Space Complexity

The space complexity is:

```text id="h9ttn5"
O(V²)
```

because the adjacency matrix stores distances for every pair of vertices.

---

## Advantages of Floyd-Warshall Algorithm

Floyd-Warshall Algorithm:

* Finds shortest path between all pairs of nodes
* Handles negative edge weights
* Is simple and elegant to implement

---

## Limitations of Floyd-Warshall Algorithm

The algorithm:

* Is slower for large graphs because of cubic complexity
* Cannot work correctly if a negative weight cycle exists

---

## Applications of Floyd-Warshall Algorithm

Floyd-Warshall Algorithm is commonly used in:

* Network routing systems
* City road distance systems
* Graph analysis
* Dynamic programming problems
* Finding transitive closure
* Competitive programming problems involving all-pairs shortest paths

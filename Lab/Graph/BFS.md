# Breadth First Search (BFS)

## Problem Description

Breadth First Search (BFS) is a graph traversal algorithm used to visit all reachable vertices of a graph level by level. Starting from a source node, BFS first visits all adjacent nodes, then moves to the next level of neighbors. This algorithm is widely used in shortest path problems for unweighted graphs, network traversal, social network analysis, and many other applications in computer science.

In this program, an undirected graph is represented using an adjacency list. The algorithm starts traversal from node `0` and visits every connected node using the BFS technique.

---

## Theory and Solution Intuition

A graph consists of vertices (nodes) and edges (connections between nodes). During traversal, one important challenge is ensuring that the same node is not visited multiple times. BFS solves this problem using two important data structures:

1. A **queue** to maintain the order of traversal.
2. A **visited array** to track already visited nodes.

The main idea of BFS is very similar to spreading waves. Suppose we start from node `0`. First, node `0` is visited. Then all nodes directly connected to `0` are visited. After that, the neighbors of those nodes are explored. In this way, traversal happens level by level.

The queue follows the **First In First Out (FIFO)** principle. The first inserted node is processed first. This property ensures that nodes closer to the source are visited earlier.

For example, consider the following graph:

```text
        0
      /   \
     1     2
    / \     \
   3   4     5
```

Starting BFS from node `0` produces the traversal:

```text
0 1 2 3 4 5
```

The traversal order occurs because:

* Node `0` is visited first.
* Its neighbors `1` and `2` are inserted into the queue.
* Then `1` is processed before `2`.
* After that, neighbors of `1` are explored, followed by neighbors of `2`.

---

## Step-by-Step Working Procedure

Initially, the graph is created using an adjacency list. Each edge is inserted in both directions because the graph is undirected.

A visited array is initialized with `false` values. This means no node has been visited yet.

The source node `0` is marked as visited and inserted into the queue.

The algorithm repeatedly performs the following operations:

* Remove the front node from the queue.
* Print the node.
* Traverse all adjacent nodes of that node.
* If an adjacent node is not visited:

  * Mark it as visited.
  * Push it into the queue.

The process continues until the queue becomes empty.

---

## BFS Code

```cpp
#include<bits/stdc++.h>
using namespace std;

int main(){
    unordered_map<int, vector<int>>adj;
    int n, e;
    
    cout<<"Please Enter number of nodes and edges"<<endl;

    cin>>n>>e;
    
    int u,v;

    // Input edges
    for(int i = 0; i < e; i++){
        cout<<"Enter edges: ";
        cin>>u>>v;

        // Undirected graph
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    vector<bool>visited(n,false);
    queue<int>q;

    // Source node = 0
    visited[0] = true;
    q.push(0);

    while(!q.empty()){

        int u = q.front();
        q.pop();

        cout<<u<<" ";

        // Traverse adjacent nodes
        for(int v: adj[u]){

            if(visited[v]==false){

                visited[v] = true;
                q.push(v);
            }
        }
    }
}
```

---

## Code Explanation

The adjacency list is declared using:

```cpp
unordered_map<int, vector<int>> adj;
```

Here, every node stores a list of its neighboring vertices.

The visited array:

```cpp
vector<bool> visited(n, false);
```

keeps track of visited nodes to avoid repeated traversal.

The queue:

```cpp
queue<int> q;
```

is responsible for maintaining BFS order.

The source node `0` is visited first:

```cpp
visited[0] = true;
q.push(0);
```

Inside the loop:

```cpp
while(!q.empty())
```

the front node is removed and processed.

Adjacent nodes are explored using:

```cpp
for(int v: adj[u])
```

If a node is not visited, it is marked visited and pushed into the queue.

---

## Time Complexity

The time complexity of BFS is:

```text
O(V + E)
```

Where:

* `V` = Number of vertices
* `E` = Number of edges

Each node is visited once, and every edge is traversed once.

---

## Space Complexity

The space complexity is:

```text
O(V + E)
```

because:

* The adjacency list stores all edges.
* The visited array stores all vertices.
* The queue may contain multiple vertices during traversal.

---

## Applications of BFS

Breadth First Search is commonly used in:

* Shortest path in unweighted graphs
* Social networking systems
* Web crawling
* Broadcasting in networks
* Finding connected components
* Level order traversal in trees

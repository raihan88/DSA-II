# Bellman-Ford Algorithm

## Problem Description

Bellman-Ford Algorithm is a shortest path algorithm used to find the minimum distance from a single source node to all other nodes in a weighted graph. Unlike Dijkstra’s Algorithm, Bellman-Ford can handle graphs containing negative edge weights.

Another important feature of this algorithm is that it can detect a **negative weight cycle** in the graph. A negative cycle is a cycle whose total edge weight becomes negative. If such a cycle exists, the shortest path is not well-defined because the path cost can decrease infinitely.

In this program, the graph is represented using an edge list. Each edge contains:

* Source node `u`
* Destination node `v`
* Edge weight `w`

The algorithm calculates the shortest distance from the source node to every other node.

---

## Theory and Solution Intuition

The Bellman-Ford Algorithm works using a technique called **edge relaxation**.

The main idea is simple:

* Initially, all distances are considered infinity.
* The source node distance is set to `0`.
* Then every edge is relaxed repeatedly.

Relaxation means:

* If a shorter path is found through an edge, update the distance.

For a graph with `V` vertices:

* The algorithm relaxes all edges exactly `V-1` times.

Why `V-1` times?

Because the longest possible shortest path between two vertices can contain at most `V-1` edges.

After performing `V-1` iterations, the algorithm performs one additional iteration:

* If any distance can still be reduced, then a negative weight cycle exists.

---

## Example Graph

Consider the following graph:

```text id="8qk7s7"
        4
    0 ------> 1
    |         |
    |         | -2
    |         v
    |-------> 2
         5
```

Edges:

* `0 → 1` weight `4`
* `1 → 2` weight `-2`
* `0 → 2` weight `5`

Starting from source node `0`:

* Distance to `1` = 4
* Distance to `2` = 2

because:

```text id="rfcb2t"
0 → 1 → 2 = 4 + (-2) = 2
```

which is smaller than the direct path cost `5`.

---

## Step-by-Step Working Procedure

First, all distances are initialized to infinity.

The source node distance is assigned `0`.

Then the algorithm performs the following operation `V-1` times:

* Traverse every edge
* Check whether a shorter path exists
* Update the distance if necessary

The relaxation condition is:

```text id="1sotj7"
distance[u] + w < distance[v]
```

If this condition becomes true:

* A shorter path is found
* Update `distance[v]`

After completing `V-1` iterations, all edges are checked once more.

If any distance still decreases, then the graph contains a negative weight cycle.

---

## Bellman-Ford Algorithm Code

```cpp id="1wh5px"
#include<bits/stdc++.h>
using namespace std;

vector<int> bellmanFord(int V,
                        vector<vector<int>>& edges,
                        int src){

    vector<int>distance(V, 1e8);

    distance[src] = 0;

    // Relax all edges V-1 times
    for(int i = 0; i < V-1; i++){

        for(auto edge : edges){

            int u = edge[0];
            int v = edge[1];
            int w = edge[2];

            if(distance[u] != 1e8 &&
               distance[u] + w < distance[v]){

                distance[v] = distance[u] + w;
            }
        }
    }

    // Negative cycle detection
    for(auto edge : edges){

        int u = edge[0];
        int v = edge[1];
        int w = edge[2];

        if(distance[u] != 1e8 &&
           distance[u] + w < distance[v]){

            return {-1};
        }
    }

    return distance;
}

int main(){

    int V, E;

    cout<<"Please Enter number of vertices and edges"<<endl;

    cin>>V>>E;

    vector<vector<int>>edges;

    int u, v, w;

    // Input edges
    for(int i = 0; i < E; i++){

        cout<<"Enter edge (u v w): ";

        cin>>u>>v>>w;

        edges.push_back({u,v,w});
    }

    int src;

    cout<<"Enter source node: ";

    cin>>src;

    vector<int>ans = bellmanFord(V, edges, src);

    // Negative cycle exists
    if(ans.size() == 1 && ans[0] == -1){

        cout<<"Negative Weight Cycle Detected"<<endl;
    }
    else{

        cout<<"Shortest Distances:"<<endl;

        for(int d : ans){
            cout<<d<<" ";
        }
    }
}
```

---

## Code Explanation

The graph is stored using an edge list:

```cpp id="v5zq6n"
vector<vector<int>> edges;
```

Each edge contains:

```text id="o9e21x"
{u, v, w}
```

where:

* `u` = source node
* `v` = destination node
* `w` = edge weight

The distance array:

```cpp id="7m3h4w"
vector<int> distance(V, 1e8);
```

stores the shortest known distance from the source node.

The core relaxation condition is:

```cpp id="4fpk7j"
if(distance[u] != 1e8 &&
   distance[u] + w < distance[v])
```

If a shorter path is found:

* Update the destination node distance

The outer loop runs `V-1` times because the maximum number of edges in a shortest path is `V-1`.

Finally, the algorithm checks for negative cycles by trying one more relaxation.

---

## Relaxation Concept

Relaxation is the heart of Bellman-Ford Algorithm.

Suppose:

* Current shortest distance to node `2` = 10
* Another path gives distance = 6

Then:

```text id="grlg50"
distance[2] = 6
```

This update process is called relaxation.

---

## Negative Weight Cycle

Consider the following cycle:

```text id="8mjlwm"
0 → 1 → 2 → 0
```

If the total cycle weight becomes negative, then every traversal reduces path cost further.

In such cases:

* The shortest path is undefined
* Bellman-Ford detects this situation

---

## Time Complexity

The time complexity of Bellman-Ford Algorithm is:

```text id="0js1d9"
O(V × E)
```

Where:

* `V` = Number of vertices
* `E` = Number of edges

The algorithm traverses all edges `V-1` times.

---

## Space Complexity

The space complexity is:

```text id="9py9w5"
O(V + E)
```

because:

* The edge list stores all edges
* The distance array stores distances for all vertices

---

## Advantages of Bellman-Ford Algorithm

Bellman-Ford Algorithm:

* Works with negative edge weights
* Detects negative cycles
* Is simpler conceptually than some advanced shortest path algorithms

---

## Limitations of Bellman-Ford Algorithm

The algorithm is slower than Dijkstra’s Algorithm because:

* Every edge is processed multiple times

Therefore, when all weights are non-negative, Dijkstra’s Algorithm is usually preferred.

---

## Applications of Bellman-Ford Algorithm

Bellman-Ford Algorithm is used in:

* Network routing protocols
* Currency exchange systems
* Graphs containing negative weights
* Detecting arbitrage opportunities
* Competitive programming shortest path problems

# Dijkstra’s Algorithm

## Problem Description

Dijkstra’s Algorithm is a greedy graph algorithm used to find the shortest distance from a single source node to all other nodes in a weighted graph where all edge weights are non-negative.

In this program, the graph is represented using an adjacency list. Each edge contains two values:

* The neighboring node
* The weight of the edge

The algorithm starts from source node `0` and calculates the minimum distance from node `0` to every other node in the graph.

---

## Theory and Solution Intuition

In many real-life problems, graphs contain weighted edges. For example:

* Roads between cities may have distances
* Network cables may have transmission costs
* Flights may have ticket prices

In such cases, simple BFS cannot guarantee the shortest path because BFS only works correctly when all edges have equal weight.

Dijkstra’s Algorithm solves this problem by always selecting the node with the currently smallest known distance. This greedy decision gradually builds the shortest path tree.

The algorithm mainly uses:

1. An adjacency list for graph representation
2. A distance array
3. A priority queue (Min Heap)

The distance array stores the shortest known distance from the source to every node.

Initially:

* Distance of source node = `0`
* Distance of all other nodes = `∞` (infinity)

The priority queue always gives the node with the minimum distance value.

---

## Example Graph

Consider the following weighted graph:

```text id="nq5v89"
        4
    0 ------ 1
    |        |
  1 |        | 2
    |        |
    2 ------ 3
        5
```

Starting from node `0`:

* Distance to `0` = 0
* Distance to `2` = 1
* Distance to `1` = 4
* Distance to `3` = 6

Shortest distance array:

```text id="zjlwmn"
0 4 1 6
```

---

## Step-by-Step Working Procedure

First, the graph is created using an adjacency list where each node stores:

* Neighbor node
* Edge weight

A distance array is initialized with `INT_MAX`, which represents infinity.

The source node `0` is assigned distance `0`.

A min heap priority queue is used so that the node with the smallest distance is processed first.

The algorithm repeatedly performs the following operations:

* Extract the node with minimum distance from the priority queue.
* Traverse all adjacent nodes.
* Calculate new possible distance:

```text id="4kw5z7"
new_distance = current_distance + edge_weight
```

* If the new distance is smaller than the previously stored distance:

  * Update the distance
  * Insert the updated node into the priority queue

This process continues until the priority queue becomes empty.

---

## Dijkstra’s Algorithm Code

```cpp id="d9d8t6"
#include<bits/stdc++.h>
using namespace std;

int main(){

    unordered_map<int, vector<pair<int,int>>>adj;

    int n, e;

    cout<<"Please Enter number of nodes and edges"<<endl;

    cin>>n>>e;

    int u,v,w;

    // Input edges
    for(int i = 0; i < e; i++){

        cout<<"Enter edge (u v w): ";
        cin>>u>>v>>w;

        // Undirected weighted graph
        adj[u].push_back({v,w});
        adj[v].push_back({u,w});
    }

    // Min Heap
    priority_queue<
        pair<int,int>,
        vector<pair<int,int>>,
        greater<pair<int,int>>
    > pq;

    vector<int>distance(n,INT_MAX);

    // Source node = 0
    distance[0] = 0;

    pq.push({0,0});

    while(!pq.empty()){

        int d = pq.top().first;
        int node = pq.top().second;

        pq.pop();

        cout<<node<<" ";

        // Traverse neighbours
        for(auto vec:adj[node]){

            int neighbour = vec.first;
            int wt = vec.second;

            // Relaxation
            if(d + wt < distance[neighbour]){

                distance[neighbour] = d + wt;

                pq.push({d + wt, neighbour});
            }
        }
    }

    // Print shortest distances
    for(int a:distance){
        cout<<a<<" ";
    }
}
```

---

## Code Explanation

The adjacency list is declared as:

```cpp id="5b0r8t"
unordered_map<int, vector<pair<int,int>>> adj;
```

Each pair stores:

* Neighbor node
* Edge weight

The priority queue:

```cpp id="2ry36x"
priority_queue<
    pair<int,int>,
    vector<pair<int,int>>,
    greater<pair<int,int>>
> pq;
```

works as a min heap.

Each element inside the queue stores:

```text id="o2bnr5"
(distance, node)
```

The distance array:

```cpp id="n41t05"
vector<int> distance(n, INT_MAX);
```

stores the minimum known distance from the source.

The relaxation step is the core of Dijkstra’s Algorithm:

```cpp id="z2wr9t"
if(d + wt < distance[neighbour])
```

If a shorter path is found:

* Update the distance
* Push the updated value into the priority queue

---

## Relaxation Concept

Relaxation means improving the shortest known distance of a node.

Suppose:

* Current distance to node `2` = 10
* Another path gives distance = 6

Then the algorithm updates:

```text id="xnkgs8"
distance[2] = 6
```

This process continues until no better path exists.

---

## Time Complexity

The time complexity of Dijkstra’s Algorithm using a priority queue is:

```text id="4fbkkm"
O((V + E) log V)
```

Where:

* `V` = Number of vertices
* `E` = Number of edges

The logarithmic factor comes from heap operations.

---

## Space Complexity

The space complexity is:

```text id="n1xfz9"
O(V + E)
```

because:

* The adjacency list stores all edges
* The distance array stores all vertices
* The priority queue may contain multiple entries

---

## Limitations of Dijkstra’s Algorithm

Dijkstra’s Algorithm works correctly only when all edge weights are non-negative.

If the graph contains negative edge weights, the algorithm may produce incorrect results. In such cases, Bellman-Ford Algorithm is used instead.

---

## Applications of Dijkstra’s Algorithm

Dijkstra’s Algorithm is widely used in:

* GPS and navigation systems
* Network routing protocols
* Flight scheduling systems
* Robot path planning
* Communication networks
* Shortest path problems in competitive programming

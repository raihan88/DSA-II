# Kruskal’s Algorithm

## Problem Description

Kruskal’s Algorithm is a greedy graph algorithm used to find the **Minimum Spanning Tree (MST)** of a connected weighted graph.

A Minimum Spanning Tree is a subset of graph edges that:

* Connects all vertices
* Contains no cycle
* Has the minimum possible total edge weight

The algorithm works by repeatedly selecting the smallest weighted edge that does not create a cycle.

In this implementation:

* The graph is represented using an edge list
* Disjoint Set Union (DSU) is used for cycle detection

The final output of the algorithm is the minimum total cost of the spanning tree.

---

## Theory and Solution Intuition

Suppose a graph contains many weighted edges. Our goal is to connect all nodes with minimum total cost.

Kruskal’s Algorithm follows a greedy strategy:

* Always choose the smallest available edge
* Avoid edges that form cycles

To efficiently detect cycles, the algorithm uses the **Disjoint Set Union (DSU)** data structure.

DSU mainly supports two operations:

### Find Operation

The `find()` function determines the parent (representative) of a node.

If two nodes have the same parent, they belong to the same connected component.

### Union Operation

The `Union()` function merges two separate components into one.

This helps connect nodes while avoiding cycles.

---

## Example Graph

Consider the following weighted graph:

```text id="dhh5o7"
        4
    0 ------ 1
    | \      |
  6 |  \5    | 2
    |   \    |
    2 ------ 3
         3
```

Edges:

* `(1,3) = 2`
* `(2,3) = 3`
* `(0,1) = 4`
* `(0,3) = 5`
* `(0,2) = 6`

Kruskal’s Algorithm sorts edges by weight:

```text id="c8bkp9"
2, 3, 4, 5, 6
```

Selected MST edges:

* `(1,3)`
* `(2,3)`
* `(0,1)`

Total MST cost:

```text id="uzg4g4"
2 + 3 + 4 = 9
```

---

## Step-by-Step Working Procedure

Initially:

* Every node is its own parent
* All edges are sorted according to weight

The algorithm then processes edges one by one.

For every edge:

* Check whether the two nodes belong to different components
* If they belong to different sets:

  * Add the edge to the MST
  * Perform union operation
* Otherwise:

  * Ignore the edge because it forms a cycle

The process continues until all vertices become connected.

---

## Kruskal’s Algorithm Code

```cpp id="tk7y9u"
#include<bits/stdc++.h>
using namespace std;

int find(int node, vector<int>&parent){

    if(node == parent[node])
        return node;

    return parent[node] = find(parent[node], parent);
}

void Union(int X, int Y, vector<int>&parent){

    int par_x = find(X, parent);
    int par_y = find(Y, parent);

    if(par_x != par_y){

        parent[par_y] = par_x;
    }
}

bool compare(vector<int>&a, vector<int>&b){

    return a[2] < b[2];
}

int kruskalsMST(int V, vector<vector<int>> &edges){

    // Sort edges according to weight
    sort(edges.begin(), edges.end(), compare);

    vector<int>parent(V);

    // Initially every node is its own parent
    for(int i = 0; i < V; i++){

        parent[i] = i;
    }

    int sum = 0;

    for(auto edge : edges){

        int u = edge[0];
        int v = edge[1];
        int w = edge[2];

        // Check cycle
        if(find(u, parent) != find(v, parent)){

            sum += w;

            Union(u, v, parent);
        }
    }

    return sum;
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

    int ans = kruskalsMST(V, edges);

    cout<<"Minimum Spanning Tree Cost = "<<ans<<endl;
}
```

---

## Code Explanation

The graph is stored using an edge list:

```cpp id="1ax7gr"
vector<vector<int>> edges;
```

Each edge contains:

```text id="10yep3"
{u, v, w}
```

where:

* `u` = source node
* `v` = destination node
* `w` = edge weight

The sorting step:

```cpp id="6wv4yx"
sort(edges.begin(), edges.end(), compare);
```

arranges edges in ascending order of weight.

The `find()` function identifies the representative parent of a node.

The statement:

```cpp id="5y56my"
return parent[node] = find(parent[node], parent);
```

performs **Path Compression**, which optimizes DSU operations.

The `Union()` function merges two separate components.

The condition:

```cpp id="h1m95z"
if(find(u, parent) != find(v, parent))
```

ensures that adding the edge does not create a cycle.

---

## Greedy Strategy

Kruskal’s Algorithm follows a greedy approach because:

* It always selects the smallest valid edge first
* This locally optimal choice eventually produces the globally optimal MST

---

## Disjoint Set Union (DSU)

DSU helps efficiently manage connected components.

Initially:

```text id="mcnr6g"
0 1 2 3
```

Each node belongs to a separate set.

After union operations:

* Multiple nodes share the same parent
* This indicates connectivity

DSU greatly improves cycle detection efficiency.

---

## Time Complexity

The time complexity of Kruskal’s Algorithm is:

```text id="v5gmb4"
O(E log E)
```

Where:

* `E` = Number of edges

The dominant operation is sorting the edges.

DSU operations are nearly constant time due to path compression.

---

## Space Complexity

The space complexity is:

```text id="4oq2k9"
O(V + E)
```

because:

* The edge list stores all edges
* The parent array stores all vertices

---

## Advantages of Kruskal’s Algorithm

Kruskal’s Algorithm:

* Is simple and efficient
* Works well for sparse graphs
* Efficiently detects cycles using DSU

---

## Limitations of Kruskal’s Algorithm

The algorithm:

* Requires edge sorting
* Becomes less efficient for dense graphs compared to Prim’s Algorithm

---

## Applications of Kruskal’s Algorithm

Kruskal’s Algorithm is widely used in:

* Network design
* Road construction planning
* Electrical wiring systems
* Water pipeline optimization
* Minimum cost infrastructure problems
* Competitive programming MST problems

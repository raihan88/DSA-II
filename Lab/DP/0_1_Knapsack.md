### 0/1 Knapsack

### Problem Description

You are given a set of items.
Each item has:

* a **weight**
* a **value**

You also have a bag (knapsack) with a fixed **capacity**.

Your task:
Pick items so that:

* the **total weight does not exceed the capacity**
* the **total value is maximized**

Constraint:
You can either **take an item or skip it**. You cannot take it partially.


### Core Idea (Take / Skip)

At every item, make a decision:

* **Skip** → move to next item, capacity unchanged
* **Take** → add value, reduce capacity (only if weight allows)

Return the **maximum** of these two choices.


### ASCII Decision Diagram

```
knapsack(i, cap)
│
├── Skip item i
│   → knapsack(i+1, cap)
│
└── Take item i (if weight[i] <= cap)
    → value[i] + knapsack(i+1, cap - weight[i])
```


### Task

Write the recursive knapsack function using this take/skip idea.

Then convert that recursive solution into **Dynamic Programming** by applying the 3 simple steps. 

### Complete the Following Code

```cpp
#include<bits/stdc++.h>
using namespace std;

struct Item {
    int weight;
    int value;
};

vector<Item> item;

// Write your recursive function here
int knapsack(int i, int cap){
    // Base case

    // Skip case

    // Take case (if possible)

    // Return max of take and skip
}

int main(){
    int n, capacity;
    cin >> n >> capacity;

    item.resize(n);

    for(int i = 0; i < n; i++){
        cin >> item[i].weight >> item[i].value;
    }

    cout << knapsack(0, capacity) << endl;

    return 0;
}
```


### Sample Input

```
4 5
2 3
1 2
3 4
2 2
```

### Explanation

* 4 items, capacity = 5
* (weight, value):

  * (2,3)
  * (1,2)
  * (3,4)
  * (2,2)

Best selection:

* item 1 (2,3)
* item 2 (1,2)
* item 3 (3,4) → exceeds capacity if all taken
  Try combinations → best value = 7

### Sample Output

```
7
```


### Final Instruction

1. Complete the recursive function.
2. Run the code and verify with the sample input.
3. Convert it into **DP (memoization)**.
4. Run again and compare performance.
5. Show both outputs to the instructor.
## Rod Cutting

### Problem Description

You are given a rod of length **N**.

You also have an array `price[]`, where:

- `price[i]` = value of a piece of length **i**

Your task:

Cut the rod into pieces so that:

- the **total length remains N**
- the **total price is maximized**

Constraint:

- You can cut the rod **multiple times**
- You can use the **same length piece again and again**

Important note:

- `price[0] = 0` → cutting length 0 gives no value (just a dummy case)
- We will start from **length = 1**

### Core Idea (Take / Skip)

At every length `i`, you decide:

- **Skip** → do not cut length `i`, move to next length
- **Take** → cut a piece of length `i` and stay at `i` (because you can reuse it)

Return the **maximum** of these two choices.

### ASCII Decision Diagram

```
RC(i, len)
│
├── Skip length i
│   → RC(i+1, len)
│
└── Take length i (if i <= len)
    → price[i] + RC(i, len - i)
```

### Task

Write the recursive rod cutting function using this take/skip idea.

Then convert that recursive solution into **Dynamic Programming** by applying the 3 simple steps.

### Complete the Following Code

```cpp
#include<bits/stdc++.h>
using namespace std;

vector<int> price;
int n;

// Write your recursive function here
int RC(int i, int len){
    // Base case

    // Skip case

    // Take case (if possible)

    // Return max of take and skip
}

int main(){
    int len;
    cin >> n >> len;

    price.resize(n+1);

    for(int i = 0; i <= n; i++){
        cin >> price[i];
    }

    cout << RC(1, len) << endl;

    return 0;
}
```

### Sample Input

```
5 5
0 2 5 7 8 10
```

### Explanation

- Rod length = 5
- price array:

  - price[1] = 2
  - price[2] = 5
  - price[3] = 7
  - price[4] = 8
  - price[5] = 10

Try different cuts:

- 5 → 10
- 2 + 3 → 5 + 7 = 12 ✅ (best)
- 1 + 4 → 2 + 8 = 10
- 1 + 1 + 3 → 2 + 2 + 7 = 11

Best value = **12**

### Sample Output

```
12
```

### Final Instruction

1. Complete the recursive function.
2. Run the code with the sample input.
3. Convert it into **DP (memoization)**.
4. Run again and observe the speed improvement.
5. Show both versions to the instructor.

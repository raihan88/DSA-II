# 💼 Counting Sort (Non-Comparison Sorting Algorithm)

## 🎯 Problem Understanding

We are given:

* An **unsorted array of integers**
* Elements are assumed to be within a **known small range**

### Goal:

👉 Sort the array in **ascending order** using Counting Sort



# 🪜 Core Steps of Counting Sort

We will use the example:

```plaintext
Input Array: [4, 2, 2, 8, 3, 3, 1]
```


## 🔹 Step 1: Count Frequency of Each Element

**Idea:**

* Create a frequency array `count[]`
* Index represents the number, value represents its frequency


### 🔸 Output of Step 1

```plaintext
Count Array (Frequency):

Index:   0 1 2 3 4 5 6 7 8
Count:   0 1 2 2 1 0 0 0 1
```

---

### 🔸 Code for Step 1

```cpp
// Find max using for-each loop
int maxVal = arr[0];   // assume first element is max

for (int x : arr) {
    if (x > maxVal) {
        maxVal = x;    // update max
    }
}

// Initialize count array
vector<int> count(maxVal + 1, 0);

// Count frequency
for (int x : arr) {
    count[x]++;
}
```


## 🔹 Step 2: Compute Prefix Sum (Cumulative Count)

**Idea:**

* Convert `count[]` into **cumulative count array**
* This tells the **final position** of each element

👉 Better name: **Position Array**


### 🔸 Output of Step 2

```plaintext
Position Array (Prefix Sum):

Index:   0 1 2 3 4 5 6 7 8
Count:   0 1 3 5 6 6 6 6 7
```


### 🔸 Code for Step 2

```cpp
// Convert to prefix sum (position array)
for (int i = 1; i <= maxVal; i++) {
    count[i] += count[i - 1];
}
```


## 🔹 Step 3: Build Output Array (Right to Left Traversal)

**Idea:**

* Traverse original array from **right to left** (important for stability)
* Use position array to place elements correctly
* Decrease count after placing


### 🔸 Output of Step 3

```plaintext
Sorted Output Array:

[1, 2, 2, 3, 3, 4, 8]
```


### 🔸 Code for Step 3

```cpp
vector<int> output(arr.size());

// Traverse from right to maintain stability
for (int i = arr.size() - 1; i >= 0; i--) {
    int val = arr[i];

    // Find correct position
    int pos = count[val] - 1;

    output[pos] = val;

    // Decrease count
    count[val]--;
}
```


# ✅ Complete C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {

    vector<int> arr = {4, 2, 2, 8, 3, 3, 1};

    int n = arr.size();

    // Step 1: Find max value
    int maxVal = *max_element(arr.begin(), arr.end());

    // Step 2: Frequency array
    vector<int> count(maxVal + 1, 0);

    for (int x : arr) {
        count[x]++;
    }

    // Step 3: Prefix sum (position array)
    for (int i = 1; i <= maxVal; i++) {
        count[i] += count[i - 1];
    }

    // Step 4: Build output array
    vector<int> output(n);

    for (int i = n - 1; i >= 0; i--) {
        int val = arr[i];
        int pos = count[val] - 1;

        output[pos] = val;
        count[val]--;
    }

    // Print result
    cout << "Sorted Array: ";
    for (int x : output)
        cout << x << " ";

    return 0;
}
```


# ⏱ Time Complexity

```plaintext
O(n + k)
```

Where:

* `n` = number of elements
* `k` = range of input (max value)


# 📌 Key Observations

* Works best when range (`k`) is **small**
* Stable sorting algorithm (due to right-to-left traversal)
* No comparisons needed (unlike Merge/Quick Sort)

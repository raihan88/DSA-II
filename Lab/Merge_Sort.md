# 💼 Merge Sort (Divide & Conquer Algorithm)

## 🎯 Problem Understanding

We are given an **unsorted array**.

### Goal:

👉 Sort the array in **ascending order** using **Merge Sort**

![merge_sort](/images/merge_sort.png)

# 🪜 Core Steps of Merge Sort

## 🔹 Step 1: Divide

**Idea:**

- Recursively split the array into two halves
- Continue dividing until each subarray contains only **one element**

**Key Point:**
Division is done using indices (`left`, `right`, `mid`)

### 🔸 Divide Function Code

```cpp
void mergeSort(vector<int>& arr, int left, int right) {

    // Base case: single element
    if (left >= right)
        return;

    int mid = (left + right) / 2;

    // Divide left half
    mergeSort(arr, left, mid);

    // Divide right half
    mergeSort(arr, mid + 1, right);

    // Merge step will combine them
    merge(arr, left, mid, right);
}
```

## 🔹 Step 2: Merge

**Idea:**

- Combine two **sorted subarrays**
- Compare elements from both sides
- Place the smaller element into a temporary array
- Copy back to original array

**Key Point:**
This is where the **actual sorting happens**

### 🔸 Merge Function Code

```cpp
void merge(vector<int>& arr, int left, int mid, int right) {

    vector<int> temp;   // Temporary array

    int i = left;       // Pointer for left subarray
    int j = mid + 1;    // Pointer for right subarray

    // Compare and merge
    while (i <= mid && j <= right) {
        if (arr[i] <= arr[j]) {
            temp.push_back(arr[i]);
            i++;
        } else {
            temp.push_back(arr[j]);
            j++;
        }
    }

    // Copy remaining elements of left subarray
    while (i <= mid) {
        temp.push_back(arr[i]);
        i++;
    }

    // Copy remaining elements of right subarray
    while (j <= right) {
        temp.push_back(arr[j]);
        j++;
    }

    // Copy sorted elements back to original array
    for (int k = left; k <= right; k++) {
        arr[k] = temp[k - left];
    }
}
```

# ✅ Complete C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

// Merge two sorted halves
void merge(vector<int>& arr, int left, int mid, int right) {

    vector<int> temp;

    int i = left;
    int j = mid + 1;

    // Merge both parts
    while (i <= mid && j <= right) {
        if (arr[i] <= arr[j]) {
            temp.push_back(arr[i]);
            i++;
        } else {
            temp.push_back(arr[j]);
            j++;
        }
    }

    // Remaining elements
    while (i <= mid) {
        temp.push_back(arr[i]);
        i++;
    }

    while (j <= right) {
        temp.push_back(arr[j]);
        j++;
    }

    // Copy back
    for (int k = left; k <= right; k++) {
        arr[k] = temp[k - left];
    }
}

// Recursive divide function
void mergeSort(vector<int>& arr, int left, int right) {

    // Base condition
    if (left >= right)
        return;

    int mid = (left + right) / 2;

    // Divide
    mergeSort(arr, left, mid);
    mergeSort(arr, mid + 1, right);

    // Merge
    merge(arr, left, mid, right);
}

int main() {

    vector<int> arr = {5, 2, 4, 7, 1, 3, 2, 6};

    mergeSort(arr, 0, arr.size() - 1);

    cout << "Sorted Array: ";
    for (int x : arr)
        cout << x << " ";

    return 0;
}
```

# ⏱ Time Complexity

```
O(n log n)
```

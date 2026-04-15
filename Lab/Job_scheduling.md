# 💼 Job Scheduling (Greedy Algorithm)


## 🎯 Problem Understanding

Each job has:

* An **ID**
* A **Deadline**
* A **Profit**
* Each job takes **exactly 1 unit of time**

### Goal:

👉 Schedule jobs in a way that **maximizes total profit**
👉 No two jobs can run at the same time
👉 A job must be completed **on or before its deadline**


## 🧠 Greedy Strategy (Why it Works)

We will follow this logic:

1. **Sort jobs in descending order of profit**
2. Pick the most profitable job first
3. Try to schedule it at its deadline
4. If that slot is already occupied, check previous slots
5. Continue until all jobs are considered

This works because:

> Taking the highest profit first gives us the best chance to maximize total profit.


# 🪜 Step-by-Step Implementation

---

## 🔹 Step 1: Define the Job Structure

We need to store:

* Job ID
* Deadline
* Profit

```cpp
struct Job {
    int id;
    int deadline;
    int profit;
};
```


## 🔹 Step 2: Sort Jobs by Profit (Descending)

We need a comparator function:

```cpp
bool compare(Job a, Job b) {
    return a.profit > b.profit;
}
```

This ensures highest profit jobs come first.



## 🔹 Step 3: Main Scheduling Logic

### Idea:

* Find maximum deadline
* Create a slot array (to track free/occupied time slots)
* Iterate through sorted jobs
* Try to place each job in the latest possible free slot

---

# ✅ Complete C++ Code

```cpp
#include <bits/stdc++.h>

using namespace std;

struct Job {
    int id;
    int deadline;
    int profit;
};

// Comparator function to sort jobs by profit (descending)
bool compare(Job a, Job b) {
    return a.profit > b.profit;
}

void jobScheduling(vector<Job>& jobs) {

    // Step 1: Sort jobs by decreasing profit
    sort(jobs.begin(), jobs.end(), compare);

    // Step 2: Find maximum deadline
    int maxDeadline = 0;
    for (auto job : jobs) {
        maxDeadline = max(maxDeadline, job.deadline);
    }

    // Step 3: Create slot array (initialize with -1 meaning empty)
    vector<int> slot(maxDeadline + 1, -1);

    int totalProfit = 0;

    // Step 4: Try to schedule each job
    for (auto job : jobs) {

        // Check from deadline down to 1
        for (int t = job.deadline; t > 0; t--) {

            if (slot[t] == -1) {   // If slot is free
                slot[t] = job.id;  // Assign job
                totalProfit += job.profit;
                break;             // Move to next job
            }
        }
    }

    // Step 5: Print scheduled jobs
    cout << "Scheduled Jobs: ";
    for (int i = 1; i <= maxDeadline; i++) {
        if (slot[i] != -1)
            cout << slot[i] << " ";
    }

    cout << "\nTotal Profit: " << totalProfit << endl;
}

int main() {

    vector<Job> jobs = {
        {1, 2, 100},
        {2, 1, 19},
        {3, 2, 27},
        {4, 1, 25},
        {5, 3, 15}
    };

    jobScheduling(jobs);

    return 0;
}
```

---

# 📊 Example Walkthrough (Active Learning)

Given Jobs:

| Job | Deadline | Profit |
| --- | -------- | ------ |
| 1   | 2        | 100    |
| 2   | 1        | 19     |
| 3   | 2        | 27     |
| 4   | 1        | 25     |
| 5   | 3        | 15     |



### 🔹 Step 1: Sort by Profit

Order becomes:

```
Job 1 (100)
Job 3 (27)
Job 4 (25)
Job 2 (19)
Job 5 (15)
```

---

### 🔹 Step 2: Scheduling

* Job 1 → Slot 2 (Free) ✅
* Job 3 → Slot 2 (Occupied) → Try Slot 1 (Free) ✅
* Job 4 → Slot 1 (Occupied) ❌
* Job 2 → Slot 1 (Occupied) ❌
* Job 5 → Slot 3 (Free) ✅

---

### ✅ Final Schedule:

```
Slot 1 → Job 3
Slot 2 → Job 1
Slot 3 → Job 5
```

### 💰 Total Profit = 100 + 27 + 15 = 142

---

# ⏱ Time Complexity Analysis

1. Sorting:

   ```
   O(n log n)
   ```

2. Scheduling (worst case nested loop):

   ```
   O(n × maxDeadline)
   ```

Overall:

```
O(n log n + n × d)
```
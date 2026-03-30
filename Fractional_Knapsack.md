# 💰 Fractional Knapsack (Greedy Algorithm)

# 🔗 Connection with Job Scheduling

| Job Scheduling                | Fractional Knapsack               |
| ----------------------------- | --------------------------------- |
| Sort by **profit**            | Sort by **profit/weight ratio**   |
| Pick highest profit first     | Pick highest ratio first          |
| Try to fit into deadline slot | Try to fit into knapsack capacity |
| If full → move backward       | If full → take fraction           |

👉 Same greedy philosophy:

> Make the best local choice first.

But here’s the twist:

* In Job Scheduling → you either take a job or not.
* In Fractional Knapsack → you can take a **fraction** of an item.

---

# 🎯 Problem Definition

Each item has:

* `id`
* `weight`
* `profit`

We are given:

* `capacity` of knapsack

Goal:
👉 Maximize total profit.


# 🪜 Step-by-Step Strategy

### Step 1: Compute profit per unit weight

$ratio = \frac{profit}{weight}$


### Step 2: Sort items in descending order of ratio

Highest value per unit weight first.


### Step 3: Take items greedily

* If full item fits → take it.
* If not → take fractional part.
* Stop when capacity becomes 0.

---

# 🧠 Important Observation (Compare with Job Scheduling)

In Job Scheduling:

```cpp
return a.profit > b.profit;
```

In Knapsack:

```cpp
return a.ratio > b.ratio;
```

See the pattern? Only the sorting criteria changed.

---

# 🏗 Step 1: Define the Structure

```cpp
struct Item {
    // Think what variables should be here
};
```


# 🧮 Step 2: Compute Ratio

👉 Where should we compute ratio?

* Inside struct?
* Inside main?
* Before sorting?

Example implementation:

```cpp
for (auto &item : items) {
    item.ratio = item.profit / item.weight;
}
```


# 🔽 Step 3: Sorting (You Fill the Blank)

Relate it to previous comparator.

```cpp
bool compare(Item a, Item b) {
    // You should fill this
    return ____________________;
}
```

Hint:

> We sorted by profit in Job Scheduling.
> What should we sort by here?

# ✅ Complete Implementation (With Some Parts Intentionally Left)

```cpp
#include <bits/stdc++.h>

using namespace std;

struct Item {
    // Fill it yourself
};

bool compare(Item a, Item b) {
    // TODO: Sort in descending order of ratio
    return ____________________;
}

void fractionalKnapsack(vector<Item>& items, double capacity) {

    // Step 1: Compute ratio
    for (auto &item : items) {
        item.ratio = item.profit / item.weight;
    }

    // Step 2: Sort items
    sort(items.begin(), items.end(), compare);

    double totalProfit = 0.0;

    cout << "Selected Items:\n";

    // Step 3: Take items greedily
    for (auto item : items) {

        if (capacity >= item.weight) {

            // Take full item
            capacity -= item.weight;
            totalProfit += item.profit;

            cout << "Item " << item.id << " (Full)\n";
        }
        else {
            // Take fractional part
            totalProfit += capacity * item.ratio;

            cout << "Item " << item.id 
                 << " (Fractional, Weight taken = "
                 << capacity << ")\n";

            capacity = 0;
            break;   // Knapsack is full
        }
    }

    cout << "Total Profit: " << totalProfit << endl;
}

int main() {

    vector<Item> items = {
        {1, 10, 60, 0},
        {2, 20, 100, 0},
        {3, 30, 120, 0}
    };

    double capacity = 50.0;

    fractionalKnapsack(items, capacity);

    return 0;
}
```

# 📊 Example Walkthrough (Active Learning)

### Items:

| ID | Weight | Profit | Ratio |
| -- | ------ | ------ | ----- |
| 1  | 10     | 60     | 6     |
| 2  | 20     | 100    | 5     |
| 3  | 30     | 120    | 4     |

Capacity = 50

---

### Step 1: Sort by ratio (Descending)

Order:

```text
Item 1 (6)
Item 2 (5)
Item 3 (4)
```

---

### Step 2: Take Items

* Take Item 1 → remaining capacity = 40
* Take Item 2 → remaining capacity = 20
* Remaining capacity = 20  
Take 20 units from Item 3  
Profit added = 20 × ratio (20 × 4 = 80)

Total Profit:

$60 + 100 + 80 = 240$



# ⏱ Time Complexity (Compare with Job Scheduling)

| Step              | Complexity |
| ----------------- | ---------- |
| Ratio calculation | O(n)       |
| Sorting           | O(n log n) |
| Selection         | O(n)       |

Overall:

```
O(n log n)
```

Same dominant complexity as Job Scheduling.

---

# 🎓 Deep Conceptual Comparison

| Feature            | Job Scheduling | Fractional Knapsack |
| ------------------ | -------------- | ------------------- |
| Greedy Choice      | Highest profit | Highest ratio       |
| Can split item?    | ❌ No           | ✅ Yes               |
| Nature             | Discrete       | Continuous          |
| Optimal by Greedy? | Yes            | Yes                 |

## Problem Statement

In the **Fractional Knapsack** problem, we are given a set of items. Each item has:

* a **weight**, and
* a **profit (value)**.

**Assumptions:**

* We are allowed to take **fractions of an item**.
* The knapsack has a **fixed capacity (W)**.

**Objective:**
Select items (possibly fractionally) such that the **total profit is maximized** without exceeding the capacity.



 Example 

| Item | Weight | Profit |
| ---- | ------ | ------ |
| I1   | 30     | 120    |
| I2   | 10     | 60     |
| I3   | 20     | 100    |

Knapsack Capacity, **W = 50**


## Step-by-Step Greedy Solution

**Step 1:** Compute **profit per unit weight (P/W)** for each item and sort in descending order based on the P/W ratio.

$P/W = \frac{\text{Profit}}{\text{Weight}}$


**Sorted Items (by P/W descending):**

| Item | Weight | Profit | P/W |
| ---- | ------ | ------ | --- |
| I2   | 10     | 60     | 6   |
| I3   | 20     | 100    | 5   |
| I1   | 30     | 120    | 4   |


**Step 2:** Initialize remaining capacity.

Remaining Capacity = **50**


**Step 3:** Take items in sorted order. Take the whole item if possible; otherwise, take the maximum possible fraction of the next item.

* I2 (weight = 10) → take full → remaining capacity = 40, profit = 60
* I3 (weight = 20) → take full → remaining capacity = 20, profit = 100
* I1 (weight = 30) → cannot take full → take fraction = 20/30

Fraction taken = **2/3**

Profit from I1 = 120 × (2/3) = **80**


**Final Selection:**

| Item | Taken       | Profit |
| ---- | ----------- | ------ |
| I2   | Full        | 60     |
| I3   | Full        | 100    |
| I1   | 2/3 portion | 80     |



**Total Profit:**
= 60 + 100 + 80 = **240**

**Final Answer:**

Optimal Selection: I2 + I3 + (2/3 of I1)
Maximum Profit: **240**

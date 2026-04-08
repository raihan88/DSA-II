## Problem Statement

In the **Job Scheduling with Deadlines** problem, we are given a set of jobs. Each job has:

* a **deadline** (the latest time slot by which it must be completed), and
* a **profit** (earned only if the job is completed within its deadline).

**Assumptions:**

* Each job takes **exactly one unit of time**.
* Only **one job can be scheduled in a single time slot**.

**Objective:**
Schedule jobs in such a way that the **total profit is maximized**.


### Example

Consider the following set of jobs:

| Job | Deadline | Profit |
| --- | -------- | ------ |
| J1  | 2        | 100    |
| J2  | 1        | 19     |
| J3  | 2        | 27     |
| J4  | 1        | 25     |
| J5  | 3        | 15     |



## Step-by-Step Greedy Solution


 **Step 1:** Sort Jobs by Profit in descending order. We prioritize jobs with higher profit.

**Sorted Jobs:**

| Job | Deadline | Profit |
| --- | -------- | ------ |
| J1  | 2        | 100    |
| J3  | 2        | 27     |
| J4  | 1        | 25     |
| J2  | 1        | 19     |
| J5  | 3        | 15     |


**Step 2:** Find the maximum deadline among all jobs. 

Here, Max deadline = **3**

Create time slots from **1 to 3**:

| Slot 1 | Slot 2 | Slot 3 |
| ------ | ------ | ------ |
| Empty  | Empty  | Empty  |

**Step 3:** Schedule each job at its deadline. If that slot is already occupied, assign it to the nearest previous available slot. If no such slot exists, discard the job.

* J1 (deadline = 2) → place in **Slot 2**
* J3 (deadline = 2) → Slot 2 occupied → place in **Slot 1**
* J4 (deadline = 1) → Slot 1 occupied → **discard**
* J2 (deadline = 1) → Slot 1 occupied → **discard**
* J5 (deadline = 3) → place in **Slot 3**


| Slot 1 | Slot 2 | Slot 3 |
| ------ | ------ | ------ |
| J3     | J1     | J5     |


**Total Profit:**
= 27 + 100 + 15 = **142**


**Final Answer:**

Optimal Job Sequence: J3 → J1 → J5
Maximum Profit:142

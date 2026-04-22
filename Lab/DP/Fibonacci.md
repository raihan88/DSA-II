### Lab Instruction Note (Dynamic Programming – Fibonacci)

Run the given recursive Fibonacci code with **n = 45**.

```cpp
#include<bits/stdc++.h>
#include<chrono>
using namespace std;
using namespace std::chrono;

int fib(int n){
    if(n==0 || n==1) return n;
    return fib(n-1) + fib(n-2);
}

int main(){
    int n = 45;

    auto start = high_resolution_clock::now();
    cout << fib(n) << endl;
    auto end = high_resolution_clock::now();

    auto duration = duration_cast<milliseconds>(end - start);
    cout << "Time: " << duration.count() << " ms" << endl;
}
```

Observe the output and measure the execution time.

Now answer this question:
**Is this Dynamic Programming?**


### Task

Convert the given recursive code into Dynamic Programming using the following three steps:

1. **Create a storage structure**
Declare a DP array of size (n+1) and initialize all values to a marker (e.g., -1) to indicate “not computed yet”.

2. **Avoid recomputation**
Before solving any subproblem, check if the answer is already stored in the DP array. If it is, return that value immediately.

3. **Store the result**
After computing a value, save it in the DP array before returning it.


### Final Instruction

Convert the recursive code into DP using these steps.

```cpp
#include<bits/stdc++.h>
#include<chrono>
using namespace std;
using namespace std::chrono;

// Step 1: declare dp array (size can be 1000 to avoid complicacy.)

int fib(int n){
    if(n==0 || n==1) return n;

    // Step 2: check if already computed

    // Step 3: compute and store before returning
    return fib(n-1) + fib(n-2);
}

int main(){
    int n = 45;

    // initialize dp array with -1

    auto start = high_resolution_clock::now();
    cout << fib(n) << endl;
    auto end = high_resolution_clock::now();

    auto duration = duration_cast<milliseconds>(end - start);
    cout << "Time: " << duration.count() << " ms" << endl;
}
```

Update the above code and run it again with **n = 45**.

Observe the execution time.

Show both outputs (recursive vs DP) to the instructor and explain the difference.
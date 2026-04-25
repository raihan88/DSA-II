## Longest Common Subsequence (LCS)

### Introduction

A *subsequence* of a string is a sequence that can be formed by deleting zero or more characters from the original string without changing the relative order of the remaining characters. The characters do not need to be contiguous.

For example, consider the string **“abcde”**. Valid subsequences include “a”, “ace”, “abd”, and even the empty sequence. However, “aec” is not a valid subsequence because it does not preserve the original order.



### Problem statement

The *Longest Common Subsequence (LCS)* problem asks us to find the longest subsequence that is common to two given strings.

For example:
s1 = “abcde”
s2 = “ace”

The common subsequences are “a”, “c”, “e”, “ac”, “ae”, and “ace”. Among them, **“ace”** is the longest. Therefore, the LCS length is 3.



## Solution

### Intuition behind the solution

The problem can be understood by thinking about how we compare the strings step by step.

Suppose we are looking at the first characters of both strings. There are two possible situations.

If the characters match, for example ‘a’ in both strings “abcde” and “ace”, then this character must be part of the LCS. This is because including it will always give a better (longer) subsequence than ignoring it. So we include this character and move forward in both strings.

If the characters do not match, for example ‘b’ (from “abcde”) and ‘c’ (from “ace”), then we are unsure which character to include. In this case, we try both possibilities. One possibility is that we skip ‘b’ from the first string and try to match the rest. The other possibility is that we skip ‘c’ from the second string. We take the maximum result from these two choices.

For example:
Comparing “bcde” and “ce”

* If we skip ‘b’, we compare “cde” and “ce”
* If we skip ‘c’, we compare “bcde” and “e”

This branching naturally leads to a recursive solution.


### Recursion tree

We define:
LCS(s1, s2) working on remaining strings

Example with “abcde” and “ace”:

```
                         (abcde, ace)
                          a == a
                              |
                        1 + (bcde, ce)
                              |
                      (bcde, ce)  b != c
                       /                 \
              (cde, ce)              (bcde, e)
               c == c                  b != e
                 |                    /       \
           1 + (de, e)          (cde, e)   (bcde, "")
                |                c != e        φ
          (de, e) d != e        /     \
           /      \        (de, e)    (cde, "")
      (e, e)    (de, "")      |          φ
       e==e        φ        ...
        |
   1 + ("", "") 
        |
        φ
```

Here, **φ (phi)** represents the base case where one of the strings becomes empty. In that case, the LCS length is 0.

This tree shows overlapping subproblems such as (de, e), which are solved multiple times.



### Recursive code

```cpp
int LCS(int i, int j, string &s1, string &s2) {
    if (i == s1.length() || j == s2.length())
        return 0;

    if (s1[i] == s2[j])
        return 1 + LCS(i + 1, j + 1, s1, s2);

    return max(LCS(i + 1, j, s1, s2),
               LCS(i, j + 1, s1, s2));
}
```

Initial call:

```cpp
LCS(0, 0, s1, s2);
```


### Converting recursion into memoization

We optimize the recursive solution using memoization in three simple steps:

* Create a 2D array `dp` initialized with -1 to store results of subproblems
* Before solving a state (i, j), check if `dp[i][j]` is already computed
* Store the computed result in `dp[i][j]` before returning

```cpp
int dp[1001][1001];

int LCS(int i, int j, string &s1, string &s2) {
    if (i == s1.length() || j == s2.length())
        return 0;

    if (dp[i][j] != -1)
        return dp[i][j];

    if (s1[i] == s2[j])
        return dp[i][j] = 1 + LCS(i + 1, j + 1, s1, s2);

    return dp[i][j] = max(LCS(i + 1, j, s1, s2),
                          LCS(i, j + 1, s1, s2));
}
```


### Tabulation (bottom-up method)

In the tabular method, we build the solution from smaller subproblems.

Here, we define:
`
dp[i][j] = LCS length of first i characters of s1 and first j characters of s2`

So, we shift the meaning slightly compared to recursion.

**Base cases:**
`if i = 0, then dp[i][j] = 0 (empty first string)`

`if j = 0, then dp[i][j] = 0 (empty second string)`

**Transition:**

If characters match:
`dp[i][j] = 1 + dp[i-1][j-1]`

If not:
`dp[i][j] = max(dp[i-1][j], dp[i][j-1])`


### Filling the full table

s1 = “abcde”
s2 = “ace”

```
      0  a  c  e
   -------------
0 |  0  0  0  0
a |  0  1  1  1
b |  0  1  1  1
c |  0  1  2  2
d |  0  1  2  2
e |  0  1  2  3
```

We start from (0,0) and fill row by row.

For example:
At (1,1): ‘a’ == ‘a’ → 1 + dp[0][0] = 1
At (3,2): ‘c’ == ‘c’ → 1 + dp[2][1] = 2
At (5,3): ‘e’ == ‘e’ → 1 + dp[4][2] = 3

Final answer: dp[5][3] = 3


### Tabulation code

```cpp
int LCS(string s1, string s2) {
    int n = s1.length();
    int m = s2.length();

    vector<vector<int>> dp(n + 1, vector<int>(m + 1, 0));

    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            if (s1[i - 1] == s2[j - 1])
                dp[i][j] = 1 + dp[i - 1][j - 1];
            else
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
        }
    }

    return dp[n][m];
}
```


### Conclusion

The LCS problem demonstrates how a complex problem can be broken into smaller overlapping subproblems. The recursive solution provides insight into the structure, memoization improves efficiency by avoiding recomputation, and tabulation offers a systematic bottom-up approach. The final time complexity is O(n × m), which is efficient for most practical applications.

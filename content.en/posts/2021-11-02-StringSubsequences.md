---
title: 'Problem: String Subsequences'
tags:
  - cp
  - dp
  - strings
---
Cho chuỗi `s1` có độ dài `3`, `s2` có độ dài `<=1e5`. Tìm số `s2.subsequence(s1)`.

<!--more-->

*Submit [tại đây](https://www.hackerrank.com/test/5k8aftrdekm/questions/gdbs88p9h9n)*

**Hướng dẫn**
  - Gọi kết quả cần tìm là dp[3][n], chính là số subsequence s1(0, 3) xuất hiện trong chuỗi s2(0, n).

**Code**

- Độ phưc tạp **O(3 * n)**

```cpp
#include <bits/stdc++.h>

using namespace std;
#define int long long


/*
 * Complete the 'getSubsequenceCount' function below.
 *
 * The function is expected to return a LONG_INTEGER.
 * The function accepts following parameters:
 *  1. STRING s1
 *  2. STRING s2
 */

int getSubsequenceCount(string a, string b) {
    int n = b.length();
    vector<vector<int>> dp(3, vector<int>(n, 0));
    dp[0][0] = (b[0] == a[0]);
    for(int i = 1; i < n; i++){
        dp[0][i] = dp[0][i - 1] + (b[i] == a[0]);
    }
    for(int i = 1; i < 3; i++){
        for(int j = 1; j < n; j++){
            if(b[j] != a[i]) dp[i][j] = dp[i][j - 1];
            else dp[i][j] = dp[i][j - 1] + dp[i - 1][j - 1];
        }
    }
    return dp[2][n - 1];
}

signed main()
{
    ofstream fout(getenv("OUTPUT_PATH"));

    string s1;
    getline(cin, s1);

    string s2;
    getline(cin, s2);

    long result = getSubsequenceCount(s1, s2);

    fout << result << "\n";

    fout.close();

    return 0;
}
```

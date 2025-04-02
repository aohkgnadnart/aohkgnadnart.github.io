---
title: 'Problem: Atomic Energy'
tags:
  - cp
  - dp
  - math
  - dirichlet
---
Cho mảng `a` gồm `n` số nguyên dương. `q` truy vấn, mỗi truy vấn cho một số `k`. 
Yêu cầu tính `f(k)` biết nếu `k <= n` thì `f(k) = a[n]`, ngược lại `f(k) = min(f(x) + f(k - x))`, `x` thuộc `[1, k)`.

**Ràng buộc**
```
n <= 100
1 <= a[i] <= 1e9
q <= 1e5
1 <= k <= 1e9
```
**Input**

```
4 5
2 3 5 7
2
3
5
6
8
```

**Output**

```
3
5
8
10
13
```

<!--more-->

*Submit [tại đây](https://open.kattis.com/problems/atomicenergy)*

**Hướng dẫn**


**Code**

- Độ phưc tạp **O(n^4 + q)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long

signed main(){
    FILE *pFile = fopen("input.txt", "r");
    if(pFile != nullptr) freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(false);cin.tie(nullptr);
    int n, q;
    cin >> n >> q;
    int a[n + 1];
    int m = 1;
    for(int i = 1; i <= n; i++){
        cin >> a[i];
        if(a[i] * m < a[m] * i) m = i;
    }
    int sz = 2e6;
    vector<int> dp(sz, 1e18);
    dp[0] = 0;
    for(int i = 1; i <= n; i++){
        dp[i] = a[i];
    }
    for(int i = n + 1; i < sz; i++){
        for(int j = 1; j <= n; j++){
            dp[i] = min(dp[i], dp[i - j] + dp[j]);
        }
    }
    while(q--){
        int k;
        cin >> k;
        if(k < sz) cout << dp[k] << "\n";
        else{
            k -= 1e6;
            int r = k % m + 1e6;
            cout << dp[r] + k / m * a[m] << '\n';
        }
    }
}
```

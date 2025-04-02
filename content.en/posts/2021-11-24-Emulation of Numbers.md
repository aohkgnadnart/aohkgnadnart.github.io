---
title: 'Problem: Emulation of Numbers'
tags:
  - cp
  - dp
---
Cho số x và mảng n phần tử. Hỏi có bao nhiêu cách tạo nên x từ các phần tử của mảng. Biết mỗi phần tử trong mảng có thể sử dụng nhiều lần.

**Ràng buộc**

```
1 ≤ X ≤ 1000000
2 ≤ N ≤ 9
```

**Input**

```
6
3
2 7 3
```

**Output**

```
2
```

<!--more-->

*Submit [tại đây](https://oj.vnoi.info/problem/icpc21_beta_e)*

**Hướng dẫn**

- classic

**Code**

- Độ phưc tạp **O(X * n)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
int dp[(int)1e6 + 1];
signed main(){
    // freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(0);cin.tie(0);
    int x;
    cin >> x;
    int n;
    cin >> n;
    set<int> se;
    for(int i = 0; i < n; i++){
        int u;
        cin >> u;
        se.insert(u);

    }
    n = se.size();
    int a[n];
    int cnt = 0;
    for(auto val: se){
        a[cnt++] = val;
    }
    dp[0] = 1;
    for(auto val: a){
        for(int i = 1; i <= x; i++){
            if(i < val) continue;
            dp[i] += dp[i - val];
        }
    }
    cout << dp[x];
}
```

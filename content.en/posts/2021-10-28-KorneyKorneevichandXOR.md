---
title: 'Problem: Korney Korneevich and XOR'
tags:
  - cp
  - dp
  - binary search
  - brute force
---

Cho mảng a gồm n `(n <= 1e6)` số nguyên `(0 <= a[i] <= 5000)`. Xuất ra tất cả giá trị xor của tất cả mảng con(subsequence) tăng dần trong mảng.

**Ràng buộc**

```
1≤n≤1e6
0≤ai≤5000
```

**Input**

```
4
4 2 2 4
```

**Output**

```
4
0 2 4 6 
```

<!--more-->

*Submit [tại đây](https://codeforces.com/contest/1582/problem/F2)*

**Hướng dẫn 1**

  - Khởi tạo `vector<int> ind[5001]` trong đó `vector<int> ind[x]` là tất cả vị trí mà giá trị `x` xuất hiện trong mảng.
  - Khởi tạo `vector<int> dp(max_value, 1e9)` trong đó `dp[x]` là chỉ số vị trí nhỏ nhất tạo nên giá trị `xor` là `x`. 
  - 2 vòng `for` lòng: vòng `for` ngoài `i` từ `[0, max_value]`, vòng `for` trong `j` từ `[0, max_xor]`. Để tính `dp[i^j]`

**Code**

- Độ phức tạp **O(n + max_value * max_xor * logn)** trong đó `max_xor = (1 << 13)`, `max_value = 5000`

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
const int MAX_XOR = (1 << 13);
const int N = 5000;
vector<int> ind[N + 1];
vector<int> dp(MAX_XOR, 1e9);
signed main(){
    // freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(0);cin.tie(0);
    int n;
    cin >> n;
    for(int i = 0; i < n; i++){
        int x;
        cin >> x;
        ind[x].push_back(i);
    }
    dp[0] = -1;
    for(int i = 0; i <= N; i++){
        for(int j = 0; j < MAX_XOR; j++){
            if(dp[j] == (int)1e9) continue;
            auto it = upper_bound(ind[i].begin(), ind[i].end(), dp[j]);
            if(it == ind[i].end()) continue;
            dp[j^i] = min(dp[j^i], *it);
        }
    }
    int k = 0;
    for(int i = 0; i < MAX_XOR; i++){
        if(dp[i] < 1e9) k++;
    }
    cout << k << "\n";
    for(int i = 0; i < MAX_XOR; i++){
        if(dp[i] < 1e9) cout << i << " ";
    }
}
```

**Hướng dẫn 2**

  - Pending

**Code**

- Độ phức tạp **O(n + max_value * max_xor)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
using ll = long long;
const int MAX_XOR = (1 << 13);
const int MAX_VALUE = 5000;
vector<vector<int>> a(MAX_VALUE + 1, vector<int>(1, 0));
vector<int> r(MAX_XOR, MAX_VALUE);
bool mark[MAX_XOR];

int main(){
    //  freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(0);cin.tie(0);
    int n;
    cin >> n;
    for(int i = 0; i < n; i++){
        int x;
        cin >> x;
        for(auto val: a[x]){
            int xo = val^x;
            mark[xo] = 1;
            while(r[xo] > x){
                a[r[xo]].push_back(xo);
                r[xo]--;
            }
            a[x].clear();
        }
    }
    int k = 0;
    mark[0] = 1;
    for(int i = 0; i < MAX_XOR; i++){
        k += mark[i];
    }
    cout << k << "\n";
    for(int i = 0; i < MAX_XOR; i++){
        if(mark[i]) cout << i << " ";
    }
}
```

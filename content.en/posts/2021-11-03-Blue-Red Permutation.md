---
title: 'Problem: Blue-Red Permutation'
tags:
  - cp
  - greedy
---
Cho mảng n phần tử. Nếu phần tử có màu đỏ,được tăng giá trị. 
Nếu phần tử có màu xanh, được giảm giá trị. Hỏi sau cùng có thể thu được, mảng hoán vị của n hay không?

**Ràng buộc**

```
1≤t≤1e4
1≤n≤2⋅1e5
−1e9≤ai≤1e9
It is guaranteed that the sum of n over all input sets does not exceed 2e5.
```

**Input**

```
8
4
1 2 5 2
BRBR
2
1 1
BB
5
3 1 4 2 5
RBRRB
5
3 1 3 1 3
RBRRB
5
5 1 5 1 5
RBRRB
4
2 2 2 2
BRBR
2
1 -2
BR
4
-2 -1 4 0
RRRR
```

**Output**

```
YES
NO
YES
YES
NO
YES
YES
YES
```

<!--more-->

*Submit [tại đây](https://codeforces.com/contest/1607/problem/D)*

**Hướng dẫn**


**Code**

- Độ phưc tạp **O(nlogn)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long

signed main(){
    //  freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(0);cin.tie(0);
    int t;
    cin >> t;
    while(t--){
        int n;
        cin >> n;
        int a[n + 1];
        for(int i = 1; i <= n; i++){
            cin >> a[i];
        }
        pair<int,int> b[n + 1];
        bool ok = 1;
        for(int i = 1; i <= n; i++){
           char c;
           cin >> c;
           if(c == 'B'){
                a[i] = min(a[i], n);
                b[i] = make_pair(a[i], 1);
                if(a[i] < 1) ok = 0;
           }
           else{
                a[i] = max(a[i], 1LL);
                b[i] = make_pair(n, a[i]);
                if(a[i] > n) ok = 0;
           }
        }
        sort(b + 1, b + n + 1);
        for(int i = 1; i <= n; i++){
            int l, r; tie(r, l) = b[i];
            if(i > r || i < l) ok = 0;
        }
        cout << (ok? "yes\n": "no\n");
    }
}
```

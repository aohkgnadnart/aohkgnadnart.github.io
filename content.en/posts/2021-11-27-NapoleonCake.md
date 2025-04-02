---
title: 'Problem: Napoleon Cake'
tags:
  - cp
  - implementation
  - dp
  - fenwick
---
Cho mảng `a` gồm `n` phần tử và một mảng `b` gồm `n` phần tử gồm các phần tử ban đầu đều là `0`. Giá trị a[i] cho biết các phần tử từ `[a[i] - i + 1, i]` trong mảng `b` được thay đổi thành `1`.
Xuất ra mảng `b` sau cùng.

**Ràng buộc**

```
1≤t≤20000
1≤n≤2e5
0≤ai≤n
It is guaranteed that the sum of n over all test cases does not exceed 2e5.
```

**Input**

```
3
6
0 3 0 0 1 3
10
0 0 0 1 0 5 0 0 0 2
3
0 0 0
```

**Output**

```
1 1 0 1 1 1 
0 1 1 1 1 1 0 0 1 1 
0 0 0 
```

<!--more-->

*Submit [tại đây](https://codeforces.com/contest/1501/problem/B)*

**Hướng dẫn 1**

**Code**

- Độ phưc tạp **O(n)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long

signed main(){
    FILE *pFile = fopen("input.txt", "r");
    if(pFile != nullptr) freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(false);cin.tie(nullptr);
    int test;
    cin >> test;
    while(test--){
        int n;
        cin >> n;
        vector<int> a(n + 1, 0);
        for(int i = 1; i <= n; i++){
            int x;
            cin >> x;
            x = min(x, i);
            a[i - x + 1] = max(a[i - x + 1], x);
        }
        int m = 0;
        for(int i = 1; i <= n; i++){
            if(a[i] == 0) cout << 0 << " ";
            else{
                int m = i + a[i] - 1;
                for(int j = i; j <= m; j++){
                    cout << 1 << " ";
                    m = max(m, j + a[j] - 1);
                }
                i = m;
            }
        }
        cout << "\n";
    }
}
```

**Hướng dẫn 2**

- dùng fenwick sum cập nhật đoạn, get điểm.

**Code**

- Độ phưc tạp **O(nlogn)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
struct fenwick{
    int n;
    vector<int> v;
    fenwick(int _n){
        n = _n;
        v.assign(n + 1, 0);
    }
    void update(int p, int val){
        for(int i = p; i <= n; i += i&-i){
            v[i] += val;
        }
    }
    void updatelr(int l, int r, int val){
        update(l, val);
        update(r + 1, -val);
    }
    int get(int p){
        int res = 0;
        for(int i = p; i > 0; i -= i&-i){
            res += v[i];
        }
        return res;
    }
};
signed main(){
    FILE *pFile = fopen("input.txt", "r");
    if(pFile != nullptr) freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(false);cin.tie(nullptr);
    int test;
    cin >> test;
    while(test--){
        int n;
        cin >> n;
        fenwick fe(n);
        for(int i = 1; i <= n; i++){
            int x;
            cin >> x;
            x = min(x, i);
            fe.updatelr(i - x + 1, i, 1);
        }
        for(int i = 1; i <= n; i++){
            if(fe.get(i) > 0) cout << 1 << " ";
            else cout << 0 << " ";
        }
        cout << "\n";
    }
}
```

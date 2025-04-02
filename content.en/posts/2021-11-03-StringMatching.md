---
title: 'Problem: String Matching'
tags:
  - cp
  - strings
  - hashing
---
Cho một chuỗi và mẫu. Đếm số vị trí mẫu xuất hiện trong chuỗi.

**Ràng buộc**

```
1≤n,m≤1e6
```

**Input**

```
saippuakauppias
pp
```

**Output**

```
2
```

<!--more-->

*Submit [tại đây](https://cses.fi/problemset/task/1753)*

**Hướng dẫn**


**Code**

- Độ phưc tạp **O(n)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
struct hashing{
    int n;
    int A, B;
    vector<int> h, p;
    hashing(string &s, int _a, int _b){
        n = s.length();
        A = _a;
        B = _b;
        h = vector<int>(n);
        p = vector<int>(n);
        p[0] = 1;
        h[0] = s[0];
        for(int i = 1; i < n; i++){
            p[i] = p[i - 1] * A % B;
            h[i] = (h[i - 1] * A + s[i]) % B;
        }
    }
    int get(int l, int r){
        if(l == 0) return h[r];
        return (h[r] - h[l - 1]*p[r - l + 1] + B*B) % B;
    }
    int cal(string &s){
        int m = s.length();
        vector<int> h(m);
        h[0] = s[0];
        for(int i = 1; i < m; i++){
            h[i] = (h[i - 1] * A + s[i]) % B;
        }
        return h[m - 1];
    }
};
signed main(){
//    freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(0);cin.tie(0);
    string s,h;
    cin >> s >> h;
    hashing ha(s, 911382323, 972663749);
    int z = ha.cal(h);
    int n = s.length();
    int m = h.length();
    int res = 0;
    for(int i = m - 1; i < n; i++){
        if(ha.get(i - m + 1, i) == z) res++;
    }
    cout << res;
}
```

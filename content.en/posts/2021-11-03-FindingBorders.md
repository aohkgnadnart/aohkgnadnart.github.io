---
title: 'Problem: Finding Borders'
tags:
  - cp
  - strings
  - hashing
---
Cho chuỗi s. Tìm tất cả độ dài của các chuỗi mà nó vừa là tiền tố, vừa là hậu tố của chuỗi s.

**Ràng buộc**

```
1≤n≤1e6
```

**Input**

```
abcababcab
```

**Output**

```
2 5
```

<!--more-->

*Submit [tại đây](https://cses.fi/problemset/task/1732)*

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
    string s;
    cin >> s;
    hashing ha(s, 911382323, 972663749);
    int n = s.length();
    for(int i = 0; i + 1 < n; i++){
        if(ha.get(0, i) == ha.get(n - 1 - i, n - 1)){
            cout << i + 1 << " ";
        }
    }
}
```

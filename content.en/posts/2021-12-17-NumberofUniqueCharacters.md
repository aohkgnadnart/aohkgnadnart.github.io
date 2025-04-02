---
title: 'Problem: Number of Unique Characters'
tags:
  - cp
  - math
---
Định nghĩa `𝑓(𝑋)` là số ký tự duy nhất trong chuỗi `(𝑋)`. Ví dụ:
`𝑓(𝑎) = 1`, `𝑓(𝑎𝑏𝑑𝑒) = 4`, `𝑓(𝑎𝑏𝑑𝑒𝑑) = 3`, `𝑓(𝑎𝑏𝑏𝑎) = 0`.
Cho một chuỗi `𝑆`. Tính giá trị của biểu thức sau:

`𝐺(𝑆) = ∑∑𝑓(𝑆 [𝑖. .𝑗])`

với `𝑆[𝑖. .𝑗]` là chuỗi con liên tiếp từ `𝑖` đến `𝑗` của `𝑆` (lập chỉ mục dựa trên `1`).

**Ràng buộc**

```
𝟏 ≤ 𝑻 ≤ 𝟏𝟎
1 ≤ |𝑆| ≤ 1e5
'a' <= s[i] <= 'z'
```

**Input**

```
4
z
icpccentral
abcde
uuuu
```

**Output**

```
1
212
35
4
```

<!--more-->

*Submit [tại đây](https://oj.vnoi.info/problem/icpc21_mt_f)*

**Hướng dẫn**


**Code**

- Độ phưc tạp **O()**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
#define double long double

signed main(){
    FILE *pFile = fopen("input.txt", "r");
    if(pFile != nullptr) freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(false);cin.tie(nullptr);
    int test;
    cin >> test;
    while(test--){
        string s;
        cin >> s;
        vector<int> adj[26];
        for(int i = 0; i < 26; i++){
            adj[i].push_back(-1);
        }
        int n = s.length();
        for(int i = 0; i < n; i++){
            adj[s[i] - 'a'].push_back(i);
        }
        for(int i = 0; i < 26; i++){
            adj[i].push_back(n);
        }
        int res = 0;
        for(int i = 0; i < 26; i++){
            for(int j = 1; j + 1 < adj[i].size(); j++){
                int ll = adj[i][j] - adj[i][j - 1] - 1;
                int rr = adj[i][j + 1] - adj[i][j] - 1;
                res += (ll + 1) * (rr + 1);
            }
        }
        cout << res << "\n";
    }
}
```

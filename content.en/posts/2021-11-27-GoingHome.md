---
title: 'Problem: Going Home'
tags:
  - cp
  - brute force
  - math
  - dirichlet
---
Cho mảng `a` có `n` phần tử. Tìm `4` vị trí khác nhau `x, y, z, t` sao cho `ax + ay = az + at`. 

**Ràng buộc**

```
4≤n≤200000
1≤ai≤2.5e6
```

**Input**

```
6
2 1 5 2 7 4
```

**Output**

```
YES
2 3 1 6 
```

<!--more-->

*Submit [tại đây](https://codeforces.com/contest/1500/problem/A)*

**Hướng dẫn**

- Áp dụng **nguyên lí Diritlet** trên tập S, nhận thấy giá trị S trong thuộc [2, 5e6]. Như vậy nếu trong 5e6 + 1 lần duyệt a[i] + a[j] thì sẽ có giá trị S lặp lại.
- Nhưng nếu mảng a có 2 phần tử cùng giá trị thì cần gấp đôi số lần duyệt mới xuất hiện S lặp lại mà hợp lệ.
- Nhưng nếu mảng a có 3 phần tử cùng giá trị thì cần gập ba lần duyệt mới xuất hiện S lặp lại mà hợp lệ
- Nhưng nếu mảng a có 4 phần tử cùng giá trị thì... kết liễu nó luôn vì đó chính là giá trị hợp lệ cần tìm.

**Code**

- Độ phưc tạp **O(min(n * n, 5e6 * 3 + 1)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
const int MAX = 25e5;
const int N = 2e5;
int x[MAX * 2 + 1], y[MAX * 2 + 1];
int a[N + 1];
signed main(){
    FILE *pFile = fopen("input.txt", "r");
    if(pFile != nullptr) freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(false);cin.tie(nullptr);
    int n;
    cin >> n;
    for(int i = 1; i <= n; i++){
        cin >> a[i];
    }
    for(int i = 1; i <= n; i++){
        for(int j = i + 1; j <= n; j++){
            int s = a[i] + a[j];
            if(x[s] && x[s] != i && y[s] != j && y[s] != i){
                cout << "YES\n";
                cout << x[s] << " " << y[s] << " " << i << " " << j;
                return 0;
            }
            x[s] = i;
            y[s] = j;
        }
    }
    cout << "NO\n";
}
```

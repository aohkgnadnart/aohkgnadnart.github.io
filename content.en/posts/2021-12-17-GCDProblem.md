---
title: 'Problem: GCD Problem'
tags:
  - cp
  - theory number
---
Cho số nguyên dương `n`. Tìm `3` số nguyên dương phân biệt `a`, `b`, `c` sao cho `a + b + c = n` và `gcd(a, b) = c`. hoặc cho biết không thể tìm thấy.

**Ràng buộc**

```
1≤t≤105
10≤n≤1e9
```

**Input**

```
6
18
63
73
91
438
122690412
```

**Output**

```
6 9 3
21 39 3
29 43 1
49 35 7
146 219 73
28622 122661788 2
```

<!--more-->

*Submit [tại đây](https://codeforces.com/contest/1617/problem/B)*

**Hướng dẫn**

- Với `n` chẵn ta có thể tách thành `n / 2, n / 2 - 1, 1`. Vì ta biết rằng 2 số tự nhiên liên tiếp có `gcd(a, b) = 1`.
- Ngược lại, `n` lẻ: ta quan sát tới gcd của 2 số lẻ `n / 2 - 1 và n / 2 + 1` hoặc `n / 2 - 2 và n / 2 + 2`

**Code**

- Độ phưc tạp **O(1)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
#define double long double
const double E = 1e-6;
const int M = (int)1e9 + 7;

signed main() {
    FILE *pFile = fopen("input.txt", "r");
    if(pFile != nullptr) freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    int test;
    cin >> test;
    while(test--) {
        int n;
        cin >> n;
        if(n % 2 == 0){
            cout << n / 2 << " " << n / 2 - 1 << " " << 1 << "\n";
        }
        else{
            if((n / 2)&1) cout << n / 2 - 2 << " " << n / 2 + 2 << " " << 1 << "\n";
            else cout << n / 2 - 1 << " " << n / 2 + 1 << " " << 1 << "\n";
        }
    }
}
```

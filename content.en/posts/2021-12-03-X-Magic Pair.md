---
title: 'Problem: X-Magic Pair'
tags:
  - cp
  - recursion
---
Bạn được cung cấp một cặp số nguyên `(a,b)` và một số nguyên `x`.

Bạn có thể thay đổi cặp theo hai cách khác nhau: set (gán) `a=|a−b|`;set (gán) `b=|a−b|`,

Cặp `(a,b)` được gọi là x-magic nếu `x` có thể đạt được như `a` hoặc như `b` chỉ sử dụng các phép toán đã cho (tức là cặp `(a,b)` có `a = x` hoặc `b = x`).

Nhiệm vụ của bạn là tìm xem cặp `(a,b)` là x-magic hay không.

Bạn phải trả lời t trường hợp thử nghiệm độc lập.

**Ràng buộc**

```
1 <= t <= 1e4
1 <= a, b, x <= 1e18
```

**Input**

```
8
6 9 3
15 38 7
18 8 8
30 30 30
40 50 90
24 28 20
365 216 52
537037812705867558 338887693834423551 3199921013340
```

**Output**

```
YES
YES
YES
YES
NO
YES
YES
YES
```

<!--more-->

*Submit [tại đây](https://codeforces.com/contest/1612/problem/D)*

**Hướng dẫn**


**Code**

- Độ phưc tạp **O()**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long

bool solve(int a, int b, int x){
    if(b < x) return 0;
    if(a == 0) return x == b;
    if((b - x) % a == 0) return 1;
    return solve(b % a, a, x);
}
signed main(){
    FILE *pFile = fopen("input.txt", "r");
    if(pFile != nullptr) freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(false);cin.tie(nullptr);
    int t;
    cin >> t;
    while(t--){
        int a, b, x;
        cin >> a >> b >> x;
        if(a > b) swap(a, b);
        if(solve(a, b, x)) cout << "YES\n";
        else cout << "NO\n";
    }
}
```

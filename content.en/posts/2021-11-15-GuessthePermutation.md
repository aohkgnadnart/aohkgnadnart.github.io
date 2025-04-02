---
title: 'Problem: Guess the Permutation'
tags:
  - cp
  - interactive
  - binary search
  - combinatorics
---
Cho mảng gồm `n` phần tử tăng dần từ `1` tới `n`. Có các phân đoạn `[i, j - 1]` và `[j, k]` đã bị đảo ngược lại(`i < j < k` và `j - i > 1`). 
Bạn được phép hỏi xem đoạn `[l, r]` có bao nhiêu cặp nghịch thế. Số lần hỏi nhiều nhất là `40`.
Tìm `i, j, k`.

**Ràng buộc**

```
4≤n≤1e9
```

**Input**

```
2 
5 
4 
3 
3 
5 
2 
2 
1 
```

**Output**

```
? 1 5
? 2 5
? 3 5
! 1 3 5
? 1 5
? 2 5
? 3 5
! 2 4 5
```

<!--more-->

*Submit [tại đây](https://codeforces.com/contest/1589/problem/D)*

**Hướng dẫn**


**Code**

- Độ phưc tạp **O(logn)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
int ask(int l, int r){
    cout << "? " << l << " " << r << '\n';
    cout.flush();
    int ans;
    cin >> ans;
    return ans;
}
int get_i(int l, int r){
    while(true){
        if(r - l <= 1){
            if(ask(1, r) == 0) return r;
            return l;
        }
        int mid = ((l + r) >> 1);
        if(ask(1, mid) == 0) l = mid;
        else r = mid;
    }
}
signed main(){
    // freopen("input.txt", "r", stdin);
    // ios_base::sync_with_stdio(0);cin.tie(0);
    int t;
    cin >> t;
    while(t--){
        int n;
        cin >> n;
        int i = get_i(1, n);
        int j = i + (ask(i, n) - ask(i + 1, n)) + 1;
        int k = j + (ask(j, n) - ask(j + 1, n));
        cout << "! " << i << " " << j << " " << k << "\n";
    }
}
```

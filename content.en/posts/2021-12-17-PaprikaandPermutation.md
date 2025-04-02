---
title: 'Problem: Paprika and Permutation'
tags:
  - cp
  - greedy
  - permutation
---
Cho mảng `a` gồm `n` số nguyên dương. Bạn được phép thực hiện thao tác sau với số lần tùy thích: đặt `a[i] = a[i] % x`, `x` là số nguyên dương mà bạn chọn. 
Hỏi có thể thu được mảng `a` gồm `n` phần tử là hoán vị từ `[1, n]`.

**Ràng buộc**

```
1≤t≤1e4
1≤n≤1e5
1≤ai≤1e9
It is guaranteed that the sum of n over all test cases does not exceed 2e5.
```

**Input**

```
4
2
1 7
3
1 5 4
4
12345678 87654321 20211218 23571113
9
1 2 3 4 18 19 5 6 7
```

**Output**

```
1
-1
4
2
```

<!--more-->

*Submit [tại đây](https://codeforces.com/contest/1617/problem/C)*

**Hướng dẫn**

- Số `i` có thể thu được từ các số `a[j]` mà `a[j] > i * 2` hoặc a[j] = i.
- `i` càng nhỏ thì càng có ít sự lựa chọn, và ngược lại. Nên ta sẽ ưu tiên tạo ra các số `i` từ `[1, n]`
- Lúc này phát sinh một chuyện, nếu `a[j]` (giá trị `a[j]` nhỏ nhất mà `a[j] > i * 2`) mà `<= n` thì ta có dùng giá trị `a[j]` này không?
- Nếu dùng thì ta lại mất một giá trị khác để tạo nên giá trị `a[j]`. Mà giá trị khác này có thể dùng luôn để tạo nên giá trị `i` mà không cần phải qua nhiều bước.
- Như vậy với các phần tử `a[j]` của mảng `a`, ta sẽ chọn ra những thằng có giá trị trong khoảng `[1, n]`, nếu có `2` phần tử trùng thì cũng chỉ chọn `1` thôi. 
Ví dụ `a = {2, 5, 3, 3}` có `n = 4` vậy các giá trị được chọn ra trước là {2, 3}`.

**Code**

- Độ phưc tạp **O(nlogn)**

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
        multiset<int> mse;
        vector<int> mark(n + 1, 0);
        for(int i = 0; i < n; i++) {
            int x;
            cin >> x;
            if(x <= n && mark[x] == 0){
                mark[x] = 1;
                continue;
            }
            mse.insert(x);
        }

        int res = 0;
        for(int i = 1; i <= n; i++){
            if(mark[i]) continue;
            auto it = mse.lower_bound(i * 2 + 1);
            if(it != mse.end()){
                res++;
                mse.erase(it);
            }
            else{
                res = -1;
                break;
            }
        }
        cout << res << "\n";
    }
}
```

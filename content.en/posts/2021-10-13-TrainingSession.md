---
title: 'Problem: Training Session'
tags:
  - cp
  - combinatorics
---

Cho `n` cặp số `(x, y)`. Tính số cách chọn ra `3` cặp số `(x, y)` trong `n` cặp số, sao cho giá trị `x` của chúng khác nhau từng đôi **hoặc** giá trị `y` của chúng khác nhau từng đôi.

**Ràng buộc**

```
1≤t≤50000
3≤n≤2e5
1≤ai,bi≤n
It is guaranteed that there are no two problems that have the same topic and difficulty at the same time.
The sum of n over all testcases doesn't exceed 2⋅105.
```

**Input**

```
2
4
2 4
3 4
2 1
1 3
5
1 5
2 4
3 3
4 2
5 1
```

**Output**

```
3
10
```

<!--more-->

*Submit [tại đây](https://codeforces.com/contest/1598/problem/D)*

**Sai**

- Đó chính là `kêt quả = số bộ 3 có x khác + số bộ 3 có y khác - số bộ 3 có x khác và y khác`
- Việc tính số bộ 3 có x khác và y khác rất khó khăn.

**Hướng dẫn**

- Ta sử dụng phần bù - một phương pháp phổ biến trong toán tổ hợp, tức là `kết quả = tất cả - không hợp lệ`
- Số cách chọn 3 cặp số (x, y) bất kì từ n cặp số là: `n * (n - 1) * (n - 2) / 6`
- Số cách chọn ra 3 cặp số (x, y) không hợp lệ, xem hình

![image](https://user-images.githubusercontent.com/83690404/137056572-c48eeb80-a8c8-4bde-bc39-7d1bab9b0dd3.png)

- Ta thấy trường hợp không hợp lệ chỉ có 1 dạng, đó là `xa == xb != xc && ya != yb == yc`
- Như vậy với mỗi cặp số (xa, yb) ta cần chọn thêm 1 cặp số (xb, yb) có `xa == xb` và 1 cặp số (xc, yc) có `yb == yc`. viếc chọn thêm 2 cặp này là độc lập, nên dễ dàng tính được.

**Code**

- Độ phức tạp **O(n)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long

main(){
    // freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(0);cin.tie(0);
    int t;
    cin >> t;
    while(t--){
        int n;
        cin >> n;
        int a[n], b[n];
        vector<int> u(n + 1, 0), v(n + 1, 0);
        for(int i = 0; i < n; i++){
            cin >> a[i] >> b[i];
            u[a[i]]++;
            v[b[i]]++;
        }
        int res = n * (n - 1) * (n - 2) / 6;
        for(int i = 0; i < n; i++){
            res -= (u[a[i]] - 1) * (v[b[i]] - 1);
        }
        cout  << res << "\n";
    }
}
```

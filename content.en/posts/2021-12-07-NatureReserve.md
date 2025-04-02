---
title: 'Problem: Nature Reserve'
tags:
  - cp
  - binary search
  - real values
  - geometry
---
Cho tọa độ `n` điểm trên mặt phẳng Oxy. Tìm đường tròn có bán kính nhỏ nhất chứa `n` điểm này, và đường tròn này có đúng `1` giao điểm với đường thẳng `y = 0`.

Xuất ra bán kính (sai số không quá `1e-6`). Nếu không tồn tại đường tròn phù hợp yêu cầu, xuất `-1`.

**Ràng buộc**

```
1 <= n <= 1e5
-1e7 <= x[i], y[i] <= 1e7
```

**Input**

```
2
0 1
1 1
```

**Output**

```
0.625
```

<!--more-->

*Submit [tại đây](https://codeforces.com/contest/1059/problem/D)*

**Hướng dẫn**

- Chặt nhị phân cho bán kính R, tìm R nhỏ nhất thỏa mãn.
- Ta biết là nếu trong n điểm tồn tại các giá trị y trái dấu thì đáp án sẽ là -1. Vì lúc đó, đường tròn chứa n điểm sẽ nằm ở cả trên và dưới trục Ox.
- Với TH n điểm có giá trị y > 0 và có bán kính R thì tâm của đường tròn sẽ là (x[o], R).
- Đường tròn bán kính R chứa được n điểm khi mà từ mỗi điểm này, lấy tâm tại nó vẽ các đường tròn bán kính R, đường tròn này cắt đường thẳng y = R khi x[o] thuộc đoạn [u,v].
- Giao của n đoạn [u,v] nếu khác rỗng thì R thỏa mãn. Tức là tồn tại điệm (x[o], R) làm tâm đường tròn chứa n điểm.
- *Lưu ý: nếu thực hiện phép tính có số thực và số nguyên thì nên xếp số thực ở trước.*

![image](https://user-images.githubusercontent.com/83690404/145004000-d5b037d4-0330-4eb8-8f0b-6b6b1f4a6897.png)


**Code**

- Độ phưc tạp **O(nlogC)**

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
    int n;
    cin >> n;
    int a[n];
    int b[n];
    bool ok = 1;
    for(int i = 0; i < n; i++){
        cin >> a[i] >> b[i];
        ok &= (b[i] * b[0] > 0);
    }
    for(int i = 0; i < n; i++){
        b[i] = fabs(b[i]);
    }
    if(!ok) return cout << -1, 0;
    function<bool(double)> f = [&](double R){
        double l = -1e17, r = 1e17;
        for(int i = 0; i < n; i++){
            double z = R * b[i] * 2 - 1.0 * b[i] * b[i];
            if(z < 0) return false;
            z = sqrt(z);
            l = max(l, - z + a[i]);
            r = min(r, z + a[i]);
        }
        if(r <= l) return false;
        return true;
    };
    function<double()> biseReal = [&](){
        double l = 0, r = 1e20;
        for(int i = 1; i <= 200; i++){
            double mid = (l + r) * 0.5;
            if(f(mid)) r = mid;
            else l = mid;
        }
        return (l + r) * 0.5;
    };
    cout << fixed << setprecision(6);
    cout << biseReal();
}
```

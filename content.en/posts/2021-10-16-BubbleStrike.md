---
title: 'Problem: Bubble Strike'
tags:
  - cp
  - combinatorics

---
Môt game có `2` người chơi (bạn và đối thủ). Có `n` bản đồ. Hệ thống chọn ra `3` bản đồ từ `n` bản đồ. Mỗi người chơi được phép chọn `1` bản đồ để loại (`2` người chơi chọn độc lập, tức là có thể trùng).
Sau đó từ các bản đồ không được chọn, hệ thống chọn ra `1` bản đồ cho game đó. Bạn chiến thắng game đó khi bạn đã xem bản đồ của game đó. 
Tính số bản đồ bạn cần xem để xác suất chiến thắng trò chơi `>= P`. Đối thủ của bạn không biết bạn đã xem bản đồ nào.

**Ràng buộc**

```
3 ≤ N ≤  1e3
0 ≤ P ≤ 1

```

**Input**

```
7 1.0000
```

**Output**

```
6
```

<!--more-->

*Submit [tại đây](https://codeforces.com/problemset/problem/1599/C)*

**Hướng dẫn** 
- Đầu tiên, ta tính xác suất xảy ra cho từng trường hợp có thể. Các trường hợp có thể xảy ra đó là:
  - 3 bản đồ hệ thống chọn, bạn đều đã xem
  - 2 bản đồ bạn đã xem.
  - 1 bản đồ bạn đã xem.

- Tiếp đó ta tính xác suất bản đồ được hệ thống chọn là bản đồ đã xem.
  - 3 bản đồ đã xem thì **chắc chăn** hệ thống sẽ chọn trúng bản đồ bạn đã xem.
  - 2 bản đồ đã xem: thì bạn sẽ chọn bản đồ chưa xem để loại bỏ, như vậy cũng **chắc chắn** hệ thống chọn trúng bản đồ đã xem.
  - 1 bản đồ đã xem: bạn sẽ loại bỏ 1 bản đồ chưa xem. Bây giờ sẽ có 2 TH: `(1 / 3 * 1 / 2 + 1 / 3 = 1 / 2)`
    - Đối thủ của bạn loại bỏ 1 bản đồ chưa xem giống bạn(XS th này là 1 / 3): thì lúc này còn lại 2 bản đồ 1 chưa xem, 1 đã xem; Xs hệ thống chọn trúng bản đồ đã xem là 1 / 2; Như vậy xs chiến thắng của bạn game này là 1 / 3 * 1 / 2 = 1 / 6.
    - Đối thủ của bạn loại bỏ 1 bản đồ chưa xem khác bạn(XS th này là 1 / 3).

**Code**

- Độ phức tạp **O(n)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
int nCk(int n, int k){
    //voi k <= 3
    if(k == 0) return 1;
    if(k == 1) return n;
    if(k == 2) return n * (n - 1) / 2;
    return n * (n - 1) * (n - 2) / 6;
}
main(){
    // freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(0);cin.tie(0);
    int n;
    double P;
    cin >> n >> P;
    if(P <= 1e-5) return cout << 0, 0;
    for(int seen = 1; seen <= n; seen++){
        // He thong chon ra 3 ban do tu n ban do cho nguoi choi 1
        double res = 0;
        double check = 0;
        int mapDaXem = min(3LL, seen);
        for(; mapDaXem >= 2; mapDaXem--){
            //mapDaXem la so map da xem trong so 3 map duoc he thong chon ra
            double p = 1.0 * nCk(seen, mapDaXem) * nCk(n - seen, 3 - mapDaXem) / nCk(n, 3);
            res += p;
        }
        mapDaXem = 1;
        double p = 1.0 * nCk(seen, mapDaXem) * nCk(n - seen, 3 - mapDaXem) / nCk(n, 3);
        res += p * 1 / 2;
        if(res >= P) return cout << seen, 0;
    }
}
```

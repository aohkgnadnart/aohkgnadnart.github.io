---
title: 'Problem: Omkar and Heavenly Tree'
tags:
  - cp
  - tree

---

Tìm một cây có n đỉnh, thỏa mãn `m` `(m < n)` yêu cầu. Mỗi yêu cầu gồm `3` cố `a, b, c`, hiểu là trên đường đi đơn giản từ đỉnh `a` tới đỉnh `c` không chứa đỉnh `b`. 
Xuất ra `n - 1` cạnh của cây. Dễ dàng chứng minh được luôn tồn tại đáp án.

**Ràng buộc**

```
1≤t≤1e4
3≤n≤105
1≤m<n
1≤ai,bi,ci≤n, a, b, c are distinct
It is guaranteed that the sum of n across all test cases will not exceed 105.
```

**Input**

```
2
7 4
1 2 3
3 4 5
5 6 7
6 5 4
5 3
1 2 3
2 3 4
3 4 5
```

**Output**

```
1 2
1 3
3 5
3 4
2 7
7 6
5 1
1 3
3 2
2 4
```

<!--more-->

*Submit [tại đây](https://codeforces.com/contest/1586/problem/B)*

**Hướng dẫn**

- Đầu tiên ta nháp thử trường hợp trong m yêu câu có chứa 3 yêu cầu sau, `1 3 7`, `1 7 3`, `3 1 7`. Để giải quyết yêu cầu này ta buộc phải dùng 1 đỉnh khác nối với cả 3 đỉnh này.

![image](https://user-images.githubusercontent.com/83690404/137828712-3b5fb4d5-4f28-432c-843d-2757aaa9f969.png)

- Tiếp theo ta thấy nối tới chuyện chọn 1 đỉnh làm tâm để nối tới tất cả các đỉnh của đồ thị, dễ thấy việc này hoàn toàn có thể.

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
        int n, m;
        cin >> n >> m;
        vector<int> adj[n + 1];
        vector<bool> appear(n + 1, 0);
        while(m--){
            int x, y, z;
            cin >> x >> y >> z;
            appear[y] = 1;
        }
        int z = 0;
        for(int i = 1; i <= n; i++){
            if(appear[i] == 0){
                z = i;
                break;
            }
        }
        for(int i = 1; i <= n; i++){
            if(i == z) continue;
            cout << z << " " << i << "\n";
        }
    }
}
```

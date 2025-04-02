---
title: 'Problem: Minimize Distance'
tags:
  - cp
  - greedy
---
Tổng cộng `n` các kho hàng nằm trên một dãy số. kho chứatôi nằm ở điểm `xi` vì `1 ≤ i ≤ n`.

Bạn là một nhân viên bán hàng với `n` các túi hàng hóa, cố gắng phân phối một túi cho mỗi nkho bãi. Bạn vàn túi ban đầu ở nguồn gốc 0. Bạn có thể mang đếnktúi tại một thời điểm. Bạn phải thu thập số lượng hàng hóa cần thiết từ điểm xuất phát, chuyển chúng đến các kho tương ứng, sau đó quay trở lại điểm xuất phát để lấy lô hàng tiếp theo của bạn.

Tính toán khoảng cách tối thiểu bạn cần phải trải qua để chuyển tất cả các túi hàng hóa đến kho hàng. Bạn không phải trả lại nguồn gốc sau khi bạn đã giao tất cả các túi.

**Ràng buộc**

```
1≤t≤10500
1≤k≤n≤2e5
−109≤xi≤109
It is guaranteed that the sum of n over all test cases does not exceed 2e5.
```

**Input**

```
4
5 1
1 2 3 4 5
9 3
-5 -10 -15 6 5 8 3 7 4
5 3
2 2 3 3 3
4 2
1000000000 1000000000 1000000000 1000000000
```

**Output**

```
25
41
7
3000000000
```

<!--more-->

*Submit [tại đây](https://codeforces.com/contest/1591/problem/C)*

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
        int n, k;
        cin >> n >> k;
        vector<int> a, b;
        for(int i = 0; i < n; i++){
            int x;
            cin >> x;
            if(x < 0) a.push_back(x);
            else if(x > 0) b.push_back(x);
        }
        
        sort(a.begin(), a.end(), greater<int>());
        sort(b.begin(), b.end());
        n = a.size();
        int m = b.size();
        if(n == 0 && m == 0){
            cout << "0\n";
            continue;
        }
        int res = 1e18;
        int p = min((n % k == 0? k - 1:  n % k - 1), n - 1);
        if(n > 0 && m > 0){
            int res1 = 0;
            int res2 = 0;
            while(p < n){
                if(p == n - 1){
                    res1 += -a[n - 1] * 2;
                    break;
                }
                res1 += -a[p] * 2;
                if(p + k >= n){
                    res1 += -a[n - 1] * 2;
                    break;
                }
                p += k;
            }

            p = min((m % k == 0? k - 1: m % k - 1), m - 1);
            while(p < m){
                if(p < m - 1) res1 += b[p] * 2;
                else{
                    res1 += b[m - 1];
                    break;
                }
                if(p + k >= m - 1){
                    res1 += b[m - 1];
                    break;
                }
                p += k;
            }
            res = min(res, res1);

            p = min((m % k == 0? k - 1: m % k - 1), m - 1);
            while(p < m){
                if(p == m - 1){
                    res2 += b[m - 1] * 2;
                    break;
                }
                res2 += b[p] * 2;
                if(p + k >= m){
                    res2 += b[m - 1] * 2;
                    break;
                }
                p += k;
            }
            p = min((n % k == 0? k - 1:  n % k - 1), n - 1);
            while(p < n){
                if(p == n - 1){
                    res2 += -a[n - 1];
                    break;
                }
                res2 += -a[p] * 2;
                if(p + k >= n){
                    res2 += -a[n - 1];
                    break;
                }
                p += k;
            }
            res = min(res, res2);
        }
        int res3 = 0;
        if(n == 0){
            p = min((m % k == 0? k - 1: m % k - 1), m - 1);
            while(p < m){
                if(p < m - 1) res3 += b[p] * 2;
                else{
                    res3 += b[m - 1];
                    break;
                }
                if(p + k >= m - 1){
                    res3 += b[m - 1];
                    break;
                }
                p += k;
            }
            res = min(res, res3);
        }
        else if(m == 0){
            p = min((n % k == 0? k - 1:  n % k - 1), n - 1);
            while(p < n){
                if(p == n - 1){
                    res3 += -a[n - 1];
                    break;
                }
                res3 += -a[p] * 2;
                if(p + k >= n){
                    res3 += -a[n - 1];
                    break;
                }
                p += k;
            }
            res = min(res, res3);
        }
        cout << res << "\n";
    }
}
```

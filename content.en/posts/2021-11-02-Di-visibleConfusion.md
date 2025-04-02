---
title: 'Problem:  Di-visible Confusion'
tags:
  - cp
  - greedy
  - number theory
---
Cho mảng a có n phần tử. Hỏi có thể xóa tất cả các phần tử của mảng hay không? phần tử `a[i]` được xóa khi `a[i]` không chia hết cho `i + 1`, với `1 <= i <= |x|`. 
Chỉ số được đánh từ 1, cập nhật lại sau mỗi thao tác xóa.

**Ràng buộc**

```
1≤t≤10000
1≤n≤1e5
1≤ai≤1e9
It is guaranteed that the sum of n over all test cases doesn't exceed 3e5.
```

**Input**

```
5
3
1 2 3
1
2
2
7 7
10
384836991 191890310 576823355 782177068 404011431 818008580 954291757 160449218 155374934 840594328
8
6 69 696 69696 696969 6969696 69696969 696969696
```

**Output**

```
YES
NO
YES
YES
NO
```

<!--more-->

*Submit [tại đây](https://codeforces.com/contest/1604/problem/C)*

**Hướng dẫn**
  - Xóa từ trước ra sau.

**Code**

- Độ phưc tạp **O(nlogn)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long

signed main(){
    // freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(0);cin.tie(0);
    int t;
    cin >> t;
    while(t--){
        int n;
        cin >> n;
        int a[n + 1];
        for(int i = 1; i <= n; i++){
            cin >> a[i];
        }
        bool res = 1;
        for(int i = 1; i <= n; i++){
            bool temp = 0;
            for(int j = i + 1; j > 1; j--){
                if(a[i] % j != 0){
                    temp = 1;
                    break;
                }
            }
            res &= temp;
        }
        cout << (res? "YES\n": "NO\n");
    }
}
```

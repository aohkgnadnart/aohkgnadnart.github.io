---
title: 'Problem: XOR Specia-LIS-t'
tags:
  - cp
  - constructive algorithms
---
Cho mảng a gồm n phần từ. chia mảng a thành k subarrays sao cho mỗi phần tử trong a thuộc về 1 subarrays. 
Mỗi subarray có 1 giá trị x, chính là độ dài chuỗi con tăng dài nhất trong subarray (LIS). Sau đó xor tất cả các giá trị x lại được giá trị 0. 
Hỏi có tồn tại cách chia k subarrays theo yêu cầu của bài không?

**Ràng buộc**

```
1≤t≤10000
2≤n≤1e5
1≤ai≤1e9
It is guaranteed that the sum of n over all test cases doesn't exceed 3e5.
```

**Input**

```
4
7
1 3 4 2 2 1 5
3
1 3 4
5
1 3 2 4 2
4
4 3 2 1
```

**Output**

```
YES
NO
YES
YES
```

<!--more-->

*Submit [tại đây](https://codeforces.com/problemset/problem/1604/B)*

**Hướng dẫn**
  - Ta thấy nếu n chẵn thì, ta chia thành n subarrays, mỗi subarray có kích thước 1, LIS = 1. Như vậy sau khi xor lại được giá trị 0.
  - Ngược lại, n lẻ thì ta tìm một chỗ có thể ghép 2 phần từ liên tiếp lại cho số subarrays chẵn mà LIS của các subarray đều là 1. Nếu có thì yes, nếu ko thì no.

**Code**

- Độ phưc tạp **O(n)**

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
        int a[n];
        for(int i = 0; i < n; i++){
            cin >> a[i];
        }
        if(n % 2 == 0) cout << "YES\n";
        else{
            bool ok = 0;
            for(int i = 1; i < n; i++){
                ok = ok or (a[i] <= a[i - 1]);
            }
            cout << (ok? "YES": "NO") << "\n";
        }
    }
}
```

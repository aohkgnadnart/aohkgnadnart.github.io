---
title: 'Problem: Dominant Character'
tags:
  - cp
  - constructive algorithms
---
Cho chuỗi s có độ dài n được tạo nên từ 3 kí tự 'a', 'b', 'c'. Hãy tìm độ dài substring ngắn nhất của s thỏa mãn substring này có:

- độ dài > 1
- số kí tự 'a' trong substring lớn hơn số kí tự 'b'
- số kí tự 'a' trong substring lớn hơn số kí tự 'c' 

**Ràng buộc**

```
1≤t≤105
2≤n≤106
It is guaranteed that the sum of n over all test cases does not exceed 106.
```

**Input**

```
3
2
aa
5
cbabb
8
cacabccc
```

**Output**

```
2
-1
3
```

<!--more-->

*Submit [tại đây](https://codeforces.com/contest/1605/problem/C)*

**Hướng dẫn**

Nghĩ tới các substring thỏa mãn, ta phát hiện ra substring chỉ có thể là các TH như trong phần if của code.
- Nhận xét 1: nếu có 2 kí tự 'a' liên tiếp thì kết quả là 2.
- Nhận xét 2: nếu không phải 2 kí tự liên tiếp 'a_a' hoặc 'a__a', không thể 'a___a' được vì lúc này chắc chắn có số lượng kí tự 'b' hoặc 'c' lớn hơn số kí tự 'a'.
- Nhận xét 3: tiếp tục nháp để tìm ra tất cả các substring có thể có.

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
        string s;
        cin >> s;
        bool aa = 0;
        for(int i = 1; i < n; i++){
            if(s[i] == 'a' && s[i - 1] == 'a'){
                aa = 1;
                break;
            }
        }
        if(aa){
            cout << 2 << "\n";
            continue;
        }
        bool a_a = 0;
        for(int i = 2; i < n; i++){
            if(s[i] == 'a' && s[i - 2] == 'a'){
                a_a = 1;
                break;
            }
        }
        if(a_a){
            cout << 3 << "\n";
            continue;
        }
        bool a__a = 0;
        for(int i = 3; i < n; i++){
            if(s[i] == 'a' && s[i - 3] == 'a' && s[i - 2] != s[i - 1]){
                a__a = 1;
                break;
            }
        }
        if(a__a){
            cout << 4 << "\n";
            continue;
        }
        bool a__a__a = 0;
        for(int i = 6; i < n; i++){
            if(s[i] == 'a' && s[i - 3] == 'a' && s[i - 6] == 'a' && s[i - 2] != s[i - 4]){
                a__a__a = 1;
                break;
            }
        }
        if(a__a__a){
            cout << 7 << "\n";
            continue;
        }
        cout << "-1\n";
    }
}
```

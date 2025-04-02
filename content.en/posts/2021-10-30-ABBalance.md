---
title: 'Problem: AB Balance'
tags:
  - cp
  - constructive algorithms
---
Cho chuỗi s gồm 2 kí tự 'a' và(hoặc) 'b'. Mỗi thao tác bạn được phép đổi 1 ký tự 'a' thành 'b' và ngược lại. 
Hãy sử dụng số thao tác tối thiểu để làm cho chuỗi s có số substring(ab) bằng số substring (ba).
Xuất ra chuỗi s sau cùng.

**Ràng buộc**

```
1≤t≤1000
1≤|s|≤100, consisting only of characters a and/or b
```

**Input**

```
4
b
aabbbabaa
abbb
abbaab
```

**Output**

```
b
aabbbabaa
bbbb
abbaaa
```

<!--more-->

*Submit [tại đây](https://codeforces.com/contest/1606/problem/A)*

**Hướng dẫn**
  - Nếu chuỗi chỉ chứa 2 ký tự, a, b. thì chuỗi sau khi bỏ qua các phần tử không cần thiết sẽ là ababab... hoặc bababa...
  - Nhận thấy chỉ khi kí tự đầu và cuỗi khác nhau thì số lượng substring(ab) và số lượng substring(ba) luôn chênh lệch 1.

**Code**

- Độ phưc tạp **O(n)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
signed main(){
    //  freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(0);cin.tie(0);
    int t;
    cin >> t;
    while(t--){
        string s;
        cin >> s;
        if(s[0] != s.back()) s[0] = s.back();
        cout << s << "\n";
    }
}
```

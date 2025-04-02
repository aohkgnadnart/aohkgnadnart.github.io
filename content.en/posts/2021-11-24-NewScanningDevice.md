---
title: 'Problem: New Scanning Device'
tags:
  - cp
  - interactive
  - binary search
---
Cho lưới 1e9 x 1e9 có các ô đơn vị 1 x 1. Có một hình chữ nhật gồm các ô đơn vị được tô màu. Hình chữ nhật này có các cạnh song song với cạnh của lưới. Bạn được phép hỏi số ô tô màu trong hình chữ nhật (a, b) (c, d), 2 tọa này lần lượt là tọa độ góc trên bên trái và góc dưới bên phải. Số lần hỏi không quá 66. Hãy tìm ra (a, b) (c, d) của hình chữ nhật được tô màu.

<!--more-->

*Submit [tại đây](https://oj.vnoi.info/problem/icpc21_beta_n)*

**Hướng dẫn**

  - pending

**Code**

- Độ phưc tạp **O(log1e9)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
int z;
int ask(int a, int b, int c, int d){
    cout << "? " << a << " " << b << " " << c << " " << d << "\n";
    cout.flush();
    int x;
    cin >> x;
    return x;
}
void endGame(int a, int b, int c, int d){
    cout << "! " << a << " " << b << " " << c << " " << d << "\n";
    cout.flush();
}
int ud(){
    int u = 1, d = 1e9;
    while(true){
        if(d - u <= 1){
            if(ask(1, 1, u, 1e9) == z) return u;
            return d;
        }
        int mid = (u + d) / 2;
        if(ask(1, 1, mid, 1e9) == z) d = mid;
        else u = mid;
    }
}
int lr(){
    int l = 1, r = 1e9;
    while(true){
        if(r - l <= 1){
            if(ask(1, 1, 1e9, l) == z) return l;
            return r;
        }
        int mid = (l + r) / 2;
        if(ask(1, 1, 1e9, mid) == z) r = mid;
        else l = mid;
    }
}
signed main(){
//    freopen("input.txt", "r", stdin);
//    ios_base::sync_with_stdio(0);cin.tie(0);
    z = ask(1, 1, 1e9, 1e9);
    int r = ud();
    int c = lr();
    int doDaiCanh1 = ask(r, 1, r, c);
    int doDaiCanh2 = z / doDaiCanh1;
    endGame(r - doDaiCanh2 + 1,c - doDaiCanh1 + 1 , r, c);
}
```

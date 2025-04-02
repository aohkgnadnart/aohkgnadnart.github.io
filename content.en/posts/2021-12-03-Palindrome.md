---
title: 'Problem: Palindrome'
tags:
  - cp
  - palindrome
  - hashing
  - dp
---
Một xâu `S` chỉ chứa kí tự latin in thường.
Nếu có thể chặt xâu `S` thành `3` xâu con không rỗng và cả `3` xâu con đều là xâu đối xứng thì xuất `YES`, ngược lại xuất `NO`.

**Ràng buộc**

```
|s| <= 5000
'a' <= s[i] <= 'z'
```

**Input**

```
abadddddz
```

**Output**

```
YES
```

<!--more-->

*Submit [tại đây](https://codeforces.com/gym/353506/problem/G)*

**Hướng dẫn 1**


**Code**

- Độ phưc tạp **O(n * n)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
const int N = 5000;
string s;
int n;
bool f[N][N];
signed main(){
    FILE *pFile = fopen("input.txt", "r");
    if(pFile != nullptr) freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(false);cin.tie(nullptr);
    cin >> s;
    n = s.length();
    for(int i = 0; i < n; i++){
        bool ok = 1;
        int l = i, r = i;
        do{
            ok &= (s[l] == s[r]);
            f[l][r] = ok;
            l--;
            r++;
        }
        while(l >= 0 && r < n);
    }
    for(int i = 0; i + 1 < n; i++){
        bool ok = 1;
        int l = i, r = i + 1;
        do{
            ok &= (s[l] == s[r]);
            f[l][r] = ok;
            l--;
            r++;
        }
        while(l >= 0 && r < n);
    }
    bool ok = 0;
    for(int i = 1; i + 2 <= n; i++){
        if(!f[0][0 + i - 1]) continue;
        for(int j = 1; i + j < n; j++){
            if(!f[i][i + j - 1]) continue;
            ok |= f[i + j][n - 1];
        }
    }
    cout << (ok? "YES\n": "NO\n");
}
```

**Hướng dẫn 2**


**Code**

- Độ phưc tạp **O(n * n)**. Tuy nhiên thời gian chạy lên tới 500ms vì cài đặt hashing sử dụng nhiều lần phép lấy dư.

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
struct hashing{
    int n;
    int A, B;
    vector<int> h, p;
    hashing(string &s, int _A, int _B){
        n = s.length();
        A = _A;
        B = _B;
        h = vector<int>(n);
        p = vector<int>(n);
        p[0] = 1;
        h[0] = (s[0] - 'a') % B;
        for(int i = 1; i < n; i++){
            p[i] = p[i - 1] * A % B;
            h[i] = (h[i - 1] * A + (s[i] - 'a')) % B;
        }
    }
    int get(int l, int r){
        if(l == 0) return h[r];
        return (h[r] - h[l - 1] * p[r - l + 1] + B * B) % B;
    }
};

signed main(){
    FILE *pFile = fopen("input.txt", "r");
    if(pFile != nullptr) freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(false);cin.tie(nullptr);
    string s;
    cin >> s;
    string h = s;
    reverse(h.begin(), h.end());
    int n = s.length();
    hashing a(s, 911382323, 972663749);
    hashing b(h, 911382323, 972663749);
    bool res = 0;
    for(int i = 1; i + 2 <= n; i++){
        if(a.get(0, 0 + i - 1) != b.get(n - 1 - i + 1, n - 1)) continue;
        for(int j = 1; j + i < n; j++){
            if(a.get(i, i + j - 1) != b.get(n - 1 - i - j + 1, n - 1 - i)) continue;
            res |= (a.get(i + j, n - 1) == b.get(0, (n - 1) - (i + j) + 1 - 1));
        }
    }
    cout << (res? "YES\n": "NO\n");
}
```

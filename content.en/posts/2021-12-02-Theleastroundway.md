---
title: 'Problem: The least round way'
tags:
  - cp
  - dp
---
Có một ma trận vuông `n × n` , bao gồm các số nguyên không âm. 
Bạn nên tìm một cách như vậy trên đó bắt đầu ở ô phía trên bên trái của ma trận;
mỗi ô sau nằm ở bên phải hoặc đi xuống so với ô hiện tại;
đường kết thúc ở ô dưới cùng bên phải.

Hơn nữa, nếu chúng ta nhân với nhau tất cả các số trên đường đi, kết quả sẽ là "vòng" nhỏ nhất. Nói cách khác, nó phải kết thúc bằng số lượng số `0` ít nhất có thể.

**Ràng buộc**

```
2 <= n <= 1000
0 <= aij <= 1e9
```

**Input**

```
3 
1 2 3 
4 5 6 
7 8 9
```

**Output**

```
0 
DDRR
```

<!--more-->

*Submit [tại đây](https://codeforces.com/problemset/problem/2/B)*

**Hướng dẫn**


**Code**

- Độ phưc tạp **O()**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
const int N = 1000;
pair<int,int> dp[N + 1][N + 1][2];
pair<int,int> a[N + 1][N + 1];
int n;
signed main(){
    FILE *pFile = fopen("input.txt", "r");
    if(pFile != nullptr) freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(false);cin.tie(nullptr);
    cin >> n;
    int rr = 0;
    for(int i = 1; i <= n; i++){
        for(int j = 1; j <= n; j++){
            int x;
            cin >> x;
            if(x == 0){
                rr = i;
                continue;
            }
            while(x % 2 == 0){
                a[i][j].first++;
                x /= 2;
            }
            while(x % 5 == 0){
                a[i][j].second++;
                x /= 5;
            }
        }
    }
    for(int i = 1; i <= n; i++){
        for(int j = 0; j < 2; j++){
            dp[0][i][j] = make_pair(1e9, 1e9);
            dp[i][0][j] = make_pair(1e9, 1e9);
        }
    }
    dp[0][1][0] = make_pair(0, 0);
    for(int i = 1; i <= n; i++){
        for(int j = 1; j <= n; j++){
            vector<pair<int,int>> v;
            v.push_back(dp[i][j - 1][0]);
            v.push_back(dp[i][j - 1][1]);
            v.push_back(dp[i - 1][j][0]);
            v.push_back(dp[i - 1][j][1]);
            sort(v.begin(), v.end());
            dp[i][j][0] = v[0];
            dp[i][j][0].first += a[i][j].first;
            dp[i][j][0].second += a[i][j].second;
            sort(v.begin(), v.end(), [](pair<int,int> u, pair<int,int> v){
                return u.second < v.second || (u.second == v.second && u.first < v.first);
            });
            dp[i][j][1] = v[0];
            dp[i][j][1].first += a[i][j].first;
            dp[i][j][1].second += a[i][j].second;
        }
    }
    int r = n, c = n;
    pair<int,int> x;
    int u = min(dp[r][c][0].first, dp[r][c][0].second);
    int v = min(dp[r][c][1].first, dp[r][c][1].second);
    if(u < v) x = dp[r][c][0];
    else x = dp[r][c][1];
    string s;
    while(r > 0 && c > 0){
        x.first -= a[r][c].first;
        x.second -= a[r][c].second;
        if(r == 1 && c > 1){
            s.push_back('R');
            c--;
            continue;
        }
        if(c == 1 && r > 1){
            s.push_back('D');
            r--;
            continue;
        }
        if(r == 1 && c == 1) break;
        if(dp[r][c - 1][0] == x || dp[r][c - 1][1] == x){
            s.push_back('R');
            c--;
            continue;
        }
        if(dp[r - 1][c][0] == x || dp[r - 1][c][1] == x){
            s.push_back('D');
            r--;
            continue;
        }
        break;
    }
    if(rr > 0 && min(u, v) > 1){
        cout << 1 << "\n";
        string res = string(rr - 1, 'D') + string(n - 1, 'R') + string (n - rr, 'D');
        cout << res << "\n";
        return 0;
 
    }
    cout << min(u, v) << "\n";
    reverse(s.begin(), s.end());
    cout << s;
}
```

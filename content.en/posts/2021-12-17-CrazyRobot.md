---
title: 'Problem: Crazy Robot'
tags:
  - cp
  - 2d
  - dfs and similar
---
Có một lưới, bao gồm n hàng và m cột. Mỗi ô của lưới là tự do hoặc bị chặn. Một trong những ô trống chứa phòng thí nghiệm. Tất cả các ô bên ngoài đường viền của lưới cũng bị chặn.

Một người máy điên rồ đã trốn thoát khỏi phòng thí nghiệm này. Nó hiện đang ở trong một số ô trống của lưới. Bạn có thể gửi một trong các lệnh sau tới rô bốt: "di chuyển sang phải", "di chuyển xuống", "di chuyển sang trái" hoặc "di chuyển lên trên". Mỗi lệnh có nghĩa là di chuyển đến một ô lân cận theo hướng tương ứng.

Tuy nhiên, vì robot điên, nó sẽ làm bất cứ điều gì ngoại trừ việc tuân theo lệnh. Khi nhận được lệnh, nó sẽ chọn một hướng khác với hướng trong lệnh và ô ở hướng đó không bị chặn. Nếu có một hướng như vậy, thì nó sẽ di chuyển đến một ô lân cận theo hướng đó. Nếu không, nó sẽ không làm gì cả.

Chúng tôi muốn đưa robot đến phòng thí nghiệm để sửa nó. Đối với mỗi ô trống, hãy xác định xem liệu robot có thể bị buộc đến phòng thí nghiệm bắt đầu từ ô này hay không. Có nghĩa là, sau mỗi bước của rô bốt, một lệnh có thể được gửi đến rô bốt sao cho bất kể rô bốt chọn hướng nào khác nhau, nó sẽ kết thúc trong phòng thí nghiệm.

**Ràng buộc**

```
1≤t≤1000
1≤n,m≤1e6; n x m≤1e6
'.' — the cell is free;
'#' — the cell is blocked;
'L' — the cell contains a lab.
The grid contains exactly one lab. The sum of n⋅m over all testcases doesn't exceed 106.
```

**Input**

```
4
3 3
...
.L.
...
4 5
#....
..##L
...#.
.....
1 1
L
1 9
....L..#.
```

**Output**

```
...
.L.
...
#++++
..##L
...#+
...++
L
++++L++#.
```

<!--more-->

*Submit [tại đây](https://codeforces.com/contest/1613/problem/E)*

**Hướng dẫn**


**Code**

- Độ phưc tạp **O()**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long

signed main(){
    FILE *pFile = fopen("input.txt", "r");
    if(pFile != nullptr) freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(false);cin.tie(nullptr);
    int test;
    cin >> test;
    while(test--){
        int n, m;
        cin >> n >> m;
        int r, c;
        vector<vector<char>> a(n + 2, vector<char>(m + 2, '#'));
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++){
                cin >> a[i][j];
                if(a[i][j] == 'L'){
                    r = i;
                    c = j;
                }
            }
        }
        vector<vector<bool>> mark(n + 2, vector<bool>(m + 2, 0));
        queue<pair<int,int>> q;
        q.push(make_pair(r, c));
        mark[r][c] = 1;
        function<bool(int,int)> loang = [&](int x, int y){
            if(a[x][y] == '#') return 0;
            int cnt = 0;
            if(a[x + 1][y] == '.') cnt++;
            if(a[x][y + 1] == '.') cnt++;
            if(a[x - 1][y] == '.') cnt++;
            if(a[x][y - 1] == '.') cnt++;
            if(cnt < 2){
                a[x][y] = '+';
                mark[x][y] = 1;
                return 1;
            }
            return 0;
        };
        mark[r][c] = 1;
        while(!q.empty()){
            int x, y; tie(x, y) = q.front(); q.pop();
            if(mark[x][y + 1] == 0 && loang(x, y + 1)){
                q.push(make_pair(x, y + 1));
            }
            if(mark[x + 1][y] == 0 && loang(x + 1, y)){
                q.push(make_pair(x + 1, y));
            }
            if(mark[x][y - 1] == 0 && loang(x, y - 1)){
                q.push(make_pair(x, y - 1));
            }
            if(mark[x - 1][y] == 0 && loang(x - 1, y)){
                q.push(make_pair(x - 1, y));
            }
        }
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++){
                cout << a[i][j];
            }
            cout << "\n";
        }
    }
}
```

---
title: 'Problem: The Number of Imposters'
tags:
  - cp
  - graph
  - dfs and similar
  - connected component
---
Cho `n` người chơi cùng chơi game. mỗi người sẽ là `imposter` hoặc `crewmate`. `imposter` là người luôn nói dối, cewmate là người luôn nói thật. cho `m` nhận xét có dạng `(i, j, c)` ví dụ: `1 2 imposter`, tức là người chơi `1` nói người chơi `2` là `imposter`, như vậy nếu người chơi `2` đúng là `imposter` thì người chơi `1` là `crewmate`, và ngược lại.
Tính số lượng **tối đa** imposter  trong game.

**Ràng buộc**

```
1≤t≤1e4
1≤n≤2e5
0≤m≤5e5
the structure "i j c" where i and j are two distinct integers and c is a string (1≤i,j≤n; i≠j; c is either imposter or crewmate
There can be multiple comments for the same pair of (i,j).
It is guaranteed that the sum of all n does not exceed 2e5 and the sum of all m does not exceed 5e5.
```

**Input**

```
5
3 2
1 2 imposter
2 3 crewmate
5 4
1 3 crewmate
2 5 crewmate
2 4 imposter
3 4 imposter
2 2
1 2 imposter
2 1 crewmate
3 5
1 2 imposter
1 2 imposter
3 2 crewmate
3 2 crewmate
1 3 imposter
5 0
```

**Output**

```
2
4
-1
2
5
```

<!--more-->

*Submit [tại đây](https://codeforces.com/problemset/problem/1594/D)*

**Hướng giải**

- Quy bài toán về dạng đồ thị 2n đỉnh. với người chơi i tương ứng sẽ có 2 đỉnh i và i + n, đại diện cho 2 trường hợp là crewmate và imposter.
- Như vậy sẽ hình thành đồ thị với các thành phần liên thông. Trong đó nếu tồn tại 1 thành phần liên thông mà có đỉnh i và i + n liên thông với nhau thì suy ra không tồn tại game như vậy, xuất -1.

![image](https://user-images.githubusercontent.com/83690404/136875128-a32a6a71-0191-46ba-b217-53f2fc91b8ad.png)

Trong hình:
- đỉnh 1 - 5 - 6 là 1 thành phần liên thông, có 2 imposter
- đỉnh 2 - 3 là 1 thành phần liên thông, có 0 imposter
- đỉnh 4 là 1 thành phần liên thông, có 1 imposter.

**Code**

- Độ phức tạp **O(n + m)**

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
        vector<int> adj[2 * n + 1];
        while(m--){
            int x, y;
            string s;
            cin >> x >> y >> s;
            if(s[0] == 'i'){
                adj[x].push_back(y + n);
                adj[y + n].push_back(x);
                adj[x + n].push_back(y);
                adj[y].push_back(x + n);
            }
            else{
                adj[x].push_back(y);
                adj[y].push_back(x);
                adj[x + n].push_back(y + n);
                adj[y + n].push_back(x + n);
            }
        }
        vector<bool> visitted(2 * n + 1, 0);
        int cntImposter = 0;
        bool ok = 0;
        vector<int> temp(2 * n + 1, 0);
        int temp1 = 0;
        int cnt = 0;
        function<void(int)> dfs = [&](int x){
            visitted[x] = 1;
            temp[x] = temp1;
            cnt++;
            if(x > n && temp[x - n] == temp[x]) ok = 1;
            else if(x <= n && temp[x + n] == temp[x]) ok = 1;
            if(x > n) cntImposter++;
            for(auto v: adj[x]){
                if(visitted[v]) continue;
                dfs(v);
            }
        };
        int res = 0;
        for(int i = 1; i <= n; i++){
            if(visitted[i] == 0 && visitted[i + n] == 0){
                temp1++;
                dfs(i);
                if(ok) break;
                else res += max(cnt - cntImposter, cntImposter);
                cntImposter = 0;
                cnt = 0;
            }
        }
        if(ok){
            cout << "-1\n";
            continue;
        }
        cout << res << "\n";
    }
}
```

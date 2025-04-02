---
title: 'Problem: Road Improvement'
tags:
  - cp
  -  tree
  -  dp
  -  dfs and similar
---
Đất nước có `n` thành phố và `n - 1` con đường hai chiều, bạn có thể đi từ mọi thành phố này đến bất kỳ thành phố nào khác nếu bạn chỉ di chuyển dọc theo các con đường. Các thành phố được đánh số bằng các số nguyên từ `1` đến `n`.

Tất cả các con đường ban đầu đều xấu, nhưng chính phủ muốn cải thiện tình trạng của một số con đường. Chúng tôi sẽ cho rằng người dân hài lòng về việc cải tạo đường nếu con đường từ thủ đô nằm ở thành phố `x` đến bất kỳ thành phố nào khác có nhiều nhất một con đường xấu.

Nhiệm vụ của bạn là với mọi `x` có thể xác định số cách cải thiện chất lượng của một số con đường để đáp ứng điều kiện của người dân. Vì những giá trị đó có thể khá lớn, bạn cần in từng mô-đun giá trị `1000000007`.

**Ràng buộc**

```
n <= 2e5
```

**Input**

```
3
1 1
```

**Output**

```
4 3 3
```

<!--more-->

*Submit [tại đây](https://codeforces.com/problemset/problem/543/D)*

**Hướng dẫn**


**Code**

- Độ phưc tạp **O()**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
const int N = 2e5;
const int M = (int)1e9 + 7;
vector<int> adj[N + 1];
int upp[N + 1];
int doww[N + 1];
int all[N + 1];
int allM[N + 1];
int n;
int euclidExtend(int a, int b){
    //tim nghiem pt ax + by = 1 trong do gcd(a, b) = 1
    //nghiem co the am
    if(a == 0) return 0;
    int y = euclidExtend(b % a, a);
    return (1 - b * y) / a;
}
int divide(int a, int b){
    int u = __gcd(b, M);
    int z = (euclidExtend(b / u, M / u) + M * M) % M;
    return a * z % M;
}
void dfs(int u, int p){
    upp[u] = 1;
    for(auto v: adj[u]){
        if(v == p) continue;
        dfs(v, u);
        upp[u] = upp[u] * (upp[v] + 1) % M;
    }
}
void dfs1(int u, int p){
    if(doww[u] + 1 == M){
        allM[u]++;
        all[u] = 1;
    }
    else all[u] = (doww[u] + 1) % M;
    for(auto v: adj[u]){
        if(v == p) continue;
        if(upp[v] + 1 == M) allM[u]++;
        else all[u] = all[u] * (upp[v] + 1) % M;
    }
    for(auto v: adj[u]){
        if(v == p) continue;
        if(upp[v] + 1 == M){
            if(allM[u] > 1) doww[v] = 0;
            else doww[v] = all[u];
        }
        else doww[v] = divide((allM[u]? 0: all[u]), upp[v] + 1);
        dfs1(v, u);
    }
}
signed main(){
    FILE *pFile = fopen("input.txt", "r");
    if(pFile != nullptr) freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(false);cin.tie(nullptr);
    cin >> n;
    for(int i = 2; i <= n; i++){
        int p;
        cin >> p;
        adj[i].push_back(p);
        adj[p].push_back(i);
    }

    dfs(1, 0);
    dfs1(1, 0);
    for(int i = 1; i <= n; i++){
//            debug(i)
//            debug(doww[i])
//            debug(upp[i])
        if(allM[i]) cout << "0 ";
        else cout << all[i] << " ";
    }
}
```

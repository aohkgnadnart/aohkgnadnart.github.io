---
title: 'Problem: Tom and Jery'
tags:
  - cp
  - tree
  - dfs and similar
  - dp
---
Tom và Jerry đang đuổi theo nhau trong một mê cung được hình thành như một cái cây. 
Cây này có `𝑛` nút. Jerry hiện đang ở nút `𝑥` và có một quả bom do Tom đặt ở đây. 
Bom có tầm bắn `𝑡` nên khi phát nổ, tất cả các nút có khoảng cách đến nút 𝑥 nhỏ hơn hoặc bằng `𝑡` sẽ bị cháy. 
Nếu Jerry bị cháy, anh ta sẽ bị ngất và bị Tom bắt. Tất nhiên, Jerry muốn thoát khỏi khu vực phát nổ bằng cách chạy qua các cạnh trong mê cung. 
Mặt khác, Tom muốn bắt Jerry nên định chặn một vài cạnh trên mê cung để Jerry không thể di chuyển qua các cạnh này. 
Nhiệm vụ: Đưa ra một tập hợp `𝑚` truy vấn, mỗi truy vấn có hai số `𝑥` và `𝑡`, cho biết nút ban đầu mà Jerry và quả bom hiện đang ở, và phạm vi của quả bom. 
Hãy giúp Tom tìm số cạnh tối thiểu phải chặn để bắt được Jerry

**Ràng buộc**

```
1 ≤ 𝑛, 𝑚 ≤ 1e5
1 ≤ 𝑢, 𝑣 ≤ 𝑛; 𝑢 ≠ 𝑣
1 ≤ 𝑥 ≤ 𝑛; 0 ≤ 𝑡 ≤ 𝑛
```

**Input**

```
7 3
1 2
2 3
2 4
3 5
3 6
4 7
4 1
2 2
2 1
```

**Output**

```
1
0
2
```

<!--more-->

*Submit [tại đây]()*

**Hướng dẫn**


**Code**

- Độ phưc tạp **O(nlogn)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
const int N = 1e5;
vector<int> adj[N + 1];
vector<int> child[N + 1];
int par[N + 1];
int c[N + 1];
pair<int,int> d[N + 1];
pair<int,int> e[N + 1];
int f[N + 1];
void dfs(int u, int p){
    for(auto v: adj[u]){
        if(v == p) continue;
        child[u].push_back(v);
        par[v] = u;
        c[v] = c[u] + 1;
        dfs(v, u);
        pair<int,int> temp = make_pair(d[v].first + 1, v);
        if(temp.first > d[u].first){
            e[u] = d[u];
            d[u] = temp;
        }
        else if(temp.first > e[u].first){
            e[u] = temp;
        }
    }
    return ;
}
void dfs1(int u, int p){
    for(auto v: adj[u]){
        if(v == p) continue;

        int temp;
        if(u == 1) temp = 0;
        else temp = f[u] + 1;
        if(d[u].second != v) temp = max(temp, d[u].first + 1);
        else if(e[u].second != v) temp = max(temp, e[u].first + 1);
        f[v] = temp;
        dfs1(v, u);
    }
}
int bise(int x, int t){
    if(child[x].empty()) return 0;
    int l = 0, r = (int)child[x].size() - 1;
    while(true){
        if(r - l <= 1){
            if(child[x][l] > t) return (int)child[x].size() - l;
            if(child[x][r] > t) return (int)child[x].size() - r;
            return 0;
        }
        int mid = (l + r) / 2;
        if(child[x][mid] > t) r = mid;
        else l = mid;
    }
}
signed main(){
    FILE *pFile = fopen("input.txt", "r");
    if(pFile != nullptr) freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(false);cin.tie(nullptr);
    int n, m;
    cin >> n >> m;
    for(int i = 1; i < n; i++){
        int u, v;
        cin >> u >> v;
        adj[u].push_back(v);
        adj[v].push_back(u);
    }
    dfs(1, 0);
    dfs1(1, 0);
    for(int i = 1; i <= n; i++){
        for(auto &val: child[i]){
            val = d[val].first + 1;
        }
        sort(child[i].begin(), child[i].end());
    }
    while(m--){
        int x, t;
        cin >> x >> t;
        if(n == 1){
            cout << "0\n";
            continue;
        }
        int res = bise(x, t);
        if(f[x] > t) res++;
//        debug(x)
//        debug(t)
//        debug(res)
        cout << res << '\n';
    }
//    debug(d[2].first)
//    debug(d[2].second)
//    debug(e[2].first)
//    debug(e[2].second)
//    debug(f[2])
//    debug(d[3].first)
//    debug(d[3].second)
//    debug(e[3].first)
//    debug(e[3].second)
//    debug(f[3])
//    debug(d[4].first)
//    debug(d[4].second)
//    debug(e[4].first)
//    debug(e[4].second)
//    debug(f[4])
//    debug(d[7].first)
//    debug(d[7].second)
//    debug(e[7].first)
//    debug(e[7].second)
//    debug(f[7])
}
```

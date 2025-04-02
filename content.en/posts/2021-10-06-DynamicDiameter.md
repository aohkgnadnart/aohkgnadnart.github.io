---
title: 'Problem: Dynamic Diameter'
tag: 
    - cp
    - tree
---

Cho cây gồm `n` đỉnh. Hỏi nếu nối đỉnh `n + 1` vào đỉnh `i`, thì đường kính của cây lúc này là bao nhiêu. Xuất ra kết qua cho tất cả `i`.

**Ràng buộc**

```
1≤n≤3e5
```

**Input**

```
3
3 2
2 1
```

**Output**

```
3
2
3
```

<!--more-->

*Submit: [tại đây](https://codeforces.com/gym/102694/problem/B)*

**Sai 1**

- Tìm tâm của cây, sau đó dfs từ tâm, thu được khoảng cách từ các đỉnh đến tâm.
- Chọn ra 2 đỉnh có khoảng cách đến tâm xa nhất, cộng 2 khoảng cách đó lại chính là đường kính.(SAI)

![image](https://user-images.githubusercontent.com/83690404/136311652-5a41206c-6b7e-4a97-aa79-c6258b2716d3.png)

Ta thấy d[1] = 2, d[2] = 2. là 2 khoảng cách xa nhất đến tâm. Nhưng đường kính của cây chỉ là 3.

**Sai 2**

- Gọi path là đường dẫn có độ dài là đường kính của cây.
- dfs từ 1 đỉnh bất kì để tìm điểm mút của path.
- dfs từ điểm mút để tìm khoẳng cách của các đỉnh đến đỉnh mút. 
- Sau đó tính đường kính mới = max(diameter, d[i] + 1) , trước đó đã đổi d[điểm mut] = diameter.(SAI)

![image](https://user-images.githubusercontent.com/83690404/136312996-32d0f090-e0fb-4da1-b5dc-6957b71398ef.png)

Ta thấy d[2] = 2. Nhưng nếu đỉnh n + 1 được nối vào đỉnh 2 thì đường kính sẽ tăng thêm 1. Rõ ràng cách tính được trình bày trong thuật trên là sai.

**Hướng dẫn**

- Gọi path là đường dẫn có độ dài là đường kính của cây.
- dfs từ 1 đỉnh bất kì để tìm điểm mút của path.
- dfs từ điểm mút để tìm khoẳng cách của các đỉnh đến đỉnh mút. 
- điểm có d[i] lớn nhất là điểm mút còn lại của path
- ta tiếp tục dfs từ điểm mút mới này, thu được mảng e với e[i] là khoảng cách từ đỉnh i tới điểm mút mới này.
- Đường kính mới = max(diameter, max(d[i] + 1, e[i] + 1))

**Code**

- Độ phức tạp **O(n)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
const int N = 3e5;
int n;
vector<int> adj[N + 1];
vector<int> d(N + 1, 0);
void dfs(int x, int p){
    for(auto v: adj[x]){
        if(v == p) continue;
        d[v] = d[x] + 1;
        dfs(v, x);
    }
}
main(){
    ios_base::sync_with_stdio(0);cin.tie(0);
    cin >> n;
    for(int i = 1; i < n; i++){
        int x, y;
        cin >> x >> y;
        adj[x].push_back(y);
        adj[y].push_back(x);
    }
    dfs(1, 0);
    int root = max_element(d.begin() + 1, d.end()) - d.begin();
    d.assign(n + 1, 0);
    dfs(root, 0);
    int root1 = max_element(d.begin() + 1, d.end()) - d.begin();
    int diameter = d[root1];
    vector<int> e = d;
    d.assign(n + 1, 0);
    dfs(root1, 0);
    for(int i = 1; i <= n; i++){
        cout << max(diameter, max(d[i] + 1, e[i] + 1)) << "\n";
    }
}
```

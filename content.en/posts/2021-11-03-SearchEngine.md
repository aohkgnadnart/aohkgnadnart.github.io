---
title: 'Problem: Search Engine'
tags:
  - cp
  - strings
  - trie
---
Cho mảng n phần tử, mỗi phần tử gồm 1 chuỗi và 1 trọng số. Cho q truy vấn, mỗi truy vấn là một chuỗi x. 
Tìm chuỗi y trong mảng a sao cho x là tiền tố của y và trọng số của y là lớn nhất có thể.

**Ràng buộc**

```
1 ≤ n, weight, len(s), len(t) ≤ 1e6
1 ≤ q ≤ 1e5
total length of all strings in database entries ≤ 1e6
total length of all query strings ≤ 1e6
```

<!--more-->

*Submit [tại đây](https://www.hackerearth.com/practice/data-structures/advanced-data-structures/trie-keyword-tree/tutorial/)*

**Hướng dẫn**


**Code**

- Độ phưc tạp **O(x + y)** trong đó x là total length of all strings in database entries, y là total length of all query strings

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
struct TrieNode{
    TrieNode * child[26];
    int val;
    TrieNode(){
        for(int i = 0; i < 26; i++){
            child[i] = nullptr;
        }
        val = 0;
    }
};
TrieNode * root = new TrieNode();
void trieInsert(const string &s, int val){
    TrieNode * p = root;
    for(int i = 0; i < s.length(); i++){
        int x = s[i] - 'a';
        if(p->child[x] == nullptr){
            p->child[x] = new TrieNode();
        }
        p = p->child[x];
        p->val = max(p->val, val);
    }
}
int trieFind(const string &s){
    TrieNode * p = root;
    for(int i = 0; i < s.length(); i++){
        int x = s[i] - 'a';
        if(p->child[x] == nullptr){
            return 0;
        }
        p = p->child[x];
    }
    return p->val;
}
signed main(){
    // freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(0);cin.tie(0);
    int n, q;
    cin >> n >> q;
    for(int i = 0; i < n; i++){
        string s;
        cin >> s;
        int val;
        cin >> val;
        trieInsert(s, val);
    }
    while(q--){
        string h;
        cin >> h;
        int res = trieFind(h);
        if(res == 0) cout << -1 << "\n";
        else cout << res << '\n';
    }
}
```

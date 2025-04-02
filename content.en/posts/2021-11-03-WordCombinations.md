---
title: 'Problem: Word Combinations'
tags:
  - cp
  - strings
  - trie
  - dp
---
Cho 1 chuỗi s và n chuỗi. Hỏi có bao nhiêu cách tạo nên chuỗi s từ các chuỗi trong n chuỗi. Kết quả được lấy dư cho `1e9 + 7`.

**Ràng buộc**

```
1≤n≤5000 
1≤k≤1e5
the total length of the words is at most 1e6
```

**Input**

```
4
ab
abab
c
cb
```

**Output**

```
2
```

<!--more-->

*Submit [tại đây](https://cses.fi/problemset/task/1731)*

**Hướng dẫn**

**Code**

- Độ phưc tạp **O(n * n)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
const int M = (int)1e9 + 7;
const int N = 5000;
struct TrieNode{
    TrieNode * child[26];
    int cnt;
    TrieNode(){
        for(int i = 0; i < 26; i++){
            child[i] = nullptr;
        }
        cnt = 0;
    }
};
TrieNode* root = new TrieNode();
string s;
void trieInsert(const string &s){
    TrieNode * p = root;
    for(int i = 0; i < s.length(); ++i){
        int x = s[i] - 'a';
        if(p->child[x] == nullptr){
            p->child[x] = new TrieNode();
        }
        p = p->child[x];
    }
    (p->cnt)++;
}
int g[5000][5000];
int trieFind(int l, int r){
    TrieNode * p = root;
    for(int i = l; i <= r; ++i){
        int x = s[i] - 'a';
        if(p->child[x] == nullptr){
            g[l][i] = 0;
            for(int j = i + 1; j <= r; j++){
                g[l][j] = 0;
            }
            return 0;
        }
        p = p->child[x];
        g[l][i] = p->cnt;
    }
    return p->cnt;
}
signed main(){
//    freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(0);cin.tie(0);
    cin >> s;
    int q;
    cin >> q;
    while(q--){
        string x;
        cin >> x;
        trieInsert(x);
    }
    int n = s.length();
    for(int i = 0; i < n; i++){
        trieFind(i, n - 1);
    }
    int dp[n];
    dp[0] = g[0][0];
    for(int i = 1; i < n; i++){
        dp[i] = g[0][i];
        for(int j = i - 1; j >= 0; j--){
            dp[i] += dp[j] * g[j + 1][i] % M;
            dp[i] %= M;
        }
    }
    cout << dp[n - 1];
}
```

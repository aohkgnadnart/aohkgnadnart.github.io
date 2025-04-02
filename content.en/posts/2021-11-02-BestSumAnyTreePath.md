---
title: 'Problem: Best Sum Any Tree Path'
tags:
  - cp
  - tree
  - dfs and similar
  - dp
---
Cho cây có n `(1 ≤ n ≤ 1e5)` đỉnh đánh số từ 0 tới n - 1, cha của các đỉnh và trọng số của các đỉnh. Tìm được đi có tổng trọng số lớn nhất.
Biết `root = 0`, `parent[0] = -1`

![Screenshot 2021-11-02 101706](https://user-images.githubusercontent.com/83690404/139783508-40aba718-91f5-4761-8946-5f93adada1c7.png)


<!--more-->

*Submit [tại đây](https://www.hackerrank.com/test/5k8aftrdekm/questions/eftieqri7m5)*

**Hướng dẫn**


**Code**

- Độ phưc tạp **O(n)**

```cpp
#include <bits/stdc++.h>

using namespace std;

string ltrim(const string &);
string rtrim(const string &);



/*
 * Complete the 'bestSumAnyTreePath' function below.
 *
 * The function is expected to return an INTEGER.
 * The function accepts following parameters:
 *  1. INTEGER_ARRAY parent
 *  2. INTEGER_ARRAY values
 */

int bestSumAnyTreePath(vector<int> parent, vector<int> values) {
    int n = values.size();
    vector<int> adj[n];
    for(int i = 1; i < n; i++){
        adj[parent[i]].push_back(i);
    }
    vector<int> left(n, 0), right(n , 0), mid(n, 0);
    int res = 0;
    function<void(int)> dfs = [&](int u){
        int le = 0, ri = 0;
        for(auto v: adj[u]){
            dfs(v);
            if(left[v] > le){
                ri = le;
                le = left[v];
            }
            else if(left[v] > ri) ri = left[v];

        }
        mid[u] = values[u] + le + ri;
        left[u] = values[u] + le;
        right[u] = values[u] + ri;
        res = max(res, max(mid[u], left[u]));
    };
    dfs(0);
    return res;
}

int main()
{
    ofstream fout(getenv("OUTPUT_PATH"));

    string parent_count_temp;
    getline(cin, parent_count_temp);

    int parent_count = stoi(ltrim(rtrim(parent_count_temp)));

    vector<int> parent(parent_count);

    for (int i = 0; i < parent_count; i++) {
        string parent_item_temp;
        getline(cin, parent_item_temp);

        int parent_item = stoi(ltrim(rtrim(parent_item_temp)));

        parent[i] = parent_item;
    }

    string values_count_temp;
    getline(cin, values_count_temp);

    int values_count = stoi(ltrim(rtrim(values_count_temp)));

    vector<int> values(values_count);

    for (int i = 0; i < values_count; i++) {
        string values_item_temp;
        getline(cin, values_item_temp);

        int values_item = stoi(ltrim(rtrim(values_item_temp)));

        values[i] = values_item;
    }

    int result = bestSumAnyTreePath(parent, values);

    fout << result << "\n";

    fout.close();

    return 0;
}

string ltrim(const string &str) {
    string s(str);

    s.erase(
        s.begin(),
        find_if(s.begin(), s.end(), not1(ptr_fun<int, int>(isspace)))
    );

    return s;
}

string rtrim(const string &str) {
    string s(str);

    s.erase(
        find_if(s.rbegin(), s.rend(), not1(ptr_fun<int, int>(isspace))).base(),
        s.end()
    );

    return s;
}
```

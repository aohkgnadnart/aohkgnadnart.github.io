---
title: 'Problem: Make Bipartite'
tags:
  - cp
  - pending
  - graph
  - dp
---
Cho một đồ thị vô hướng với n+1 các đỉnh đánh số từ [0:n]

Với mỗi i=1,2,…,n, đồ thị có một cạnh vô hướng với trọng số là a[i] nối đỉnh i và đỉnh 0. 

Ngoài ra, đối với mỗi i=1,2,…,n, đồ thị có một cạnh vô hướng với trọng số là b[i] kết nối đỉnh i và đỉnh i + 1(riêng i = n thì kết nối đỉnh n và 1)

Biểu đồ không có cạnh nào ngoài các cạnh này N * 2 các cạnh trên.

Hãy để chúng tôi xóa một số cạnh khỏi biểu đồ này để biểu đồ sẽ là lưỡng phân.

Tổng trọng lượng tối thiểu của các cạnh phải bị xóa là bao nhiêu?

**Ràng buộc**

```
3 <= n <= 2e5
1 <= a[i], b[i] <= 1e9
tất cả giá trị trong input đều nguyên
```

**Input**

```
5
31 4 159 2 65
5 5 5 5 10
```

**Output**

```
16
```

<!--more-->

*Submit [tại đây](https://atcoder.jp/contests/abc229/tasks/abc229_f)*

**Hướng dẫn**


**Code**

- Độ phưc tạp **O()**

```cpp

```

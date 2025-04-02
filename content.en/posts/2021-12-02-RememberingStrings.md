---
title: 'Problem: Remembering Strings'
tags:
  - cp
  - pending
  - graph
---
Bạn có nhiều tập hợp `n` chuỗi có cùng độ dài, bao gồm các chữ cái tiếng Anh viết thường. Chúng ta sẽ nói rằng những chuỗi đó dễ nhớ nếu đối với mỗi chuỗi có một số vị trí `i` và một số chữ cái `c` của bảng chữ cái tiếng Anh, sao cho chuỗi này là chuỗi duy nhất trong tập hợp đa có chữ `c` ở vị trí `i`.

Ví dụ: một tập hợp nhiều chuỗi `{"abc", "aba", "adc", "ada"}` không dễ nhớ. Và multiset `{"abc", "ada", "ssa"}` rất dễ nhớ vì:
chuỗi đầu tiên là chuỗi duy nhất có ký tự `c` ở vị trí `3` ;
chuỗi thứ hai là chuỗi duy nhất có ký tự `d` ở vị trí `2` ;
chuỗi thứ ba là chuỗi duy nhất có ký tự `s` ở vị trí `2` .

Bạn muốn thay đổi một chút bộ đa năng của mình để dễ nhớ. Đối với `aij` tiền xu, bạn có thể thay đổi nhân vật trong `j` vị trí -thứ `i` của chuỗi -thứ vào bất kỳ chữ cái thường khác của bảng chữ cái tiếng Anh. Tìm số tiền tối thiểu bạn phải trả là bao nhiêu để làm cho tập hợp nhiều chuỗi dễ nhớ.

**Ràng buộc**

```
1 <= n, m <= 20
0 <= aij <= 1e6
```

**Input**

```
4 5
abcde
abcde
abcde
abcde
1 1 1 1 1
1 1 1 1 1
1 1 1 1 1
1 1 1 1 1
```

**Output**

```
3
```

<!--more-->

*Submit [tại đây](https://codeforces.com/problemset/problem/543/C)*

**Hướng dẫn**


**Code**

- Độ phưc tạp **O()**

```cpp

```

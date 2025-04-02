---
title: 'Problem: Kingdom of Cats'
tags:
  - cp
  - geometry
  - brute force
---
Choa tọa độ n điểm trong mp Oxy. Tính số tứ giác lồi khác nhau được tạo ra.

**Ràng buộc**

```
1≤n≤50
−1e9≤xi,yi≤1e9
tổng n trong tất cả các test không quá 500
n = 0 kết thúc chương trình
```

**Input**

```
7 
4 1 
3 1 
2 1 
1 1 
1 2 
1 3 
1 4 
4 
0 0 
0 2 
2 0 
2 2 
0
```

**Output**

```
9 
1
```

<!--more-->

*Submit [tại đây](https://open.kattis.com/problems/kingdomofcats)*

![image](https://user-images.githubusercontent.com/83690404/144561500-c6de60bb-a3d2-4ef5-9558-d440a08682ca.png)


**Hướng dẫn**


**Code**

- Độ phưc tạp **O(nlogn)**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define debug(x) cerr << #x << " = " << x << endl;
#define int long long
#define double long double
const double E = 1e-6;
const int M = (int)1e9 + 7;
class point {
  public:
    int x, y;
    point() {
        x = 0;
        y = 0;
    }
    point(int _x, int _y) {
        x = _x;
        y = _y;
    }
    friend int crossProduct(const point& a, const point& b) {
        return a.x * b.y - b.x * a.y;
    }
    friend int pointLocation(const point& a, const point& b, const point& c) {
        int x = crossProduct(b - a, c - b);
        if(x > 0) return 1;//left
        if(x < 0) return -1;//right
        return 0;
    }
    friend vector<point> convexHull(point a[], int n) {
        // n different points
        // return point clockwise
        if(n < 3) {
            vector<point> res(n);
            for(int i = 0; i < n; i++) {
                res[i] = a[i];
            }
            return res;
        }
        sort(a, a + n);
        vector<point> res;
        vector<point> b;
        for(int i = 0; i < n; i++) {
            while(res.size() > 1) {
                int x = pointLocation(res[(int)res.size() - 2], res.back(), a[i]);
                if(x > 0) {
                    b.push_back(res.back());
                    res.pop_back();
                } else break;
            }
            res.push_back(a[i]);
        }
        sort(b.begin(), b.end(), greater<point>());
        b.push_back(a[0]);
        for(auto val: b) {
            while(res.size() > 1) {
                int x = pointLocation(res[(int)res.size() - 2], res.back(), val);
                if(x > 0)  res.pop_back();
                else break;
            }
            res.push_back(val);
        }
        res.pop_back();
        return res;
    }
    friend vector<point> convexHullMin(point a[], int n){
        // n different points
        // return point clockwise
        vector<point> v = convexHull(a, n);
        if(v.size() < 3) return v;
        vector<point> res(1, v[0]);
        for(int i = 1; i + 1 < v.size(); i++){
            int x = pointLocation(v[i - 1], v[i], v[i + 1]);
            if(x == 0) continue;
            res.push_back(v[i]);
        }
        int x = pointLocation(v[(int)v.size() - 2], v.back(), v[0]);
        if(x < 0 || (x == 0 && (int)res.size() == 1)) res.push_back(v.back());
        return res;
    }
    friend int pointInPolygon(point a[], int n, const point& b) {
        // return 0: BOUNDARY
        // return 1: INSIDE
        // return -1: OUTSIDE
        srand(time(nullptr));
        // point c(1234567890, 1023485557);
        point c(1047159043, 343214337);
        c.x += rand() * rand();
        c.y += rand() * rand();
        int cnt = 0;
        for(int i = 0; i + 1 < n; i++) {
            if(fabs(fabs(a[i] - b) + fabs(a[i + 1] - b) - fabs(a[i] - a[i + 1])) < E) return 0;
            int x = lineSegmentIntersection(c, b, a[i], a[i + 1]);
            cnt += (x > 0);
        }
        if(fabs(fabs(a[n - 1] - b) + fabs(a[0] - b) - fabs(a[n - 1] - a[0])) < E) return 0;
        int x = lineSegmentIntersection(c, b, a[n - 1], a[0]);
        cnt += (x > 0);

        if(cnt&1) return 1;
        return -1;
    }
    friend double fabs(const point& a) {
        return sqrt(a.x * a.x + a.y * a.y);
    }
    friend int abs2(const point& a) {
        return a.x * a.x + a.y * a.y;
    }
    friend double triangleArea(const point& a, const point& b, const point& c) {
        return abs(crossProduct(b - a, c - a)) / 2.0L;
    }
    friend int triangleAreaX2(const point& a, const point& b, const point& c) {
        return abs(crossProduct(b - a, c - a));
    }
    friend double polygonArea(point a[], int n) {
        // the vertices a[i] and a[i + 1] are adjacent, and vertices a[0] and a[n - 1] also are adjacent
        return polygonAreaX2(a, n) / 2.0L;
    }
    friend int polygonAreaX2(point a[], int n) {
        // the vertices a[i] and a[i + 1] are adjacent, and vertices a[0] and a[n - 1] also are adjacent
        int res = 0;
        for(int i = 0; i + 1 < n; i++) {
            res += crossProduct(a[i], a[i + 1]);
        }
        res += crossProduct(a[n - 1], a[0]);
        return abs(res);
    }
    friend double dist(const point& a, const point& b, const point& c) {
        return fabs(crossProduct(b - a, c - a)) / fabs(a - b);
    }
    friend int lineSegmentIntersection(const point& a, const point& b, const point& c, const point& d) {
        //a != b and c != d
        // return 0: 0 intersection point
        // return 1: 1 intersection point
        // return 2: countless intersection point
        int cnt = 0;
        if(a == c || a == d) cnt++;
        if(b == c || b == d) cnt++;
        if(cnt > 0) return cnt;

        int x = pointLocation(a, b, c);
        if(x == 0 && fabs(fabs(a - c) + fabs(b - c) - fabs(a - b)) < E) return 1;
        int y = pointLocation(a, b, d);
        if(y == 0 && fabs(fabs(a - d) + fabs(b - d) - fabs(a - b)) < E) return 1;
        if(x == 0 && y == 0 && fabs(fabs(a - c) + fabs(a - d) - fabs(c - d)) < E) return 2;
        if(x * y < 0) {
            int z = pointLocation(c, d, a);
            int t = pointLocation(c, d, b);
            if(z == 0 && fabs(fabs(c - a) + fabs(d - a) - fabs(c - d)) < E) return 1;
            if(t == 0 && fabs(fabs(c - b) + fabs(d - b) - fabs(c - d)) < E) return 1;
            return z * t < 0;
        }
        return 0;
    }
    friend int minEuclidDistance(point a[], int n) {
        pair<int,int> u[n], v[n];
        for(int i = 0; i < n; i++) {
            u[i].first = a[i].x + a[i].y;
            u[i].second = i;
            v[i].first = a[i].y - a[i].x;
            v[i].second = i;
        }
        sort(u, u + n);
        sort(v, v + n);
        int res = 9e18;
        for(int i = 1; i < n; i++) {
            res = min(res, abs2(a[u[i].second] - a[u[i - 1].second]));
            res = min(res, abs2(a[v[i].second] - a[v[i - 1].second]));
        }
        return res;
    }
    friend tuple<int,int,int> lineEquation(const point& a, const point &b) {
        int u = a.x - b.x;
        int v = a.y - b.y;
        // lineEquation: -v * (x - x0) + u(y - y0) = 0
        return make_tuple(-v, u, v * a.x - u * a.y);
    }
    friend int countIntegerPointsInTheRangeAB(const point& a, const point& b) {
        // u * x + v * y + p = 0
        // y = -(u * x + p) / v;
        int u, v, p;
        tie(u, v, p) = lineEquation(a, b);
        int l = abs(a.x - b.x);
        int r = abs(a.y - b.y);
        return __gcd(l, r) + 1;
    }
    friend pair<int,int> polygonLatticePoints(point a[], int n) {
        // the vertices a[i] and a[i + 1] are adjacent, and vertices a[0] and a[n - 1] also are adjacent
        // n >= 3
        // We have: S = a + b / 2 - 1
        // 2 * S = 2 * a + b - 2
        int areaX2 = round(polygonArea(a, n) * 2);
        int value_b = 0;
        for(int i = 1; i < n; i++) value_b += countIntegerPointsInTheRangeAB(a[i], a[i - 1]);
        value_b += countIntegerPointsInTheRangeAB(a[n - 1], a[0]);
        value_b -= n;
        int value_a = (areaX2 - value_b + 2) / 2;
        return make_pair(value_a, value_b);
    }
    friend point operator- (const point& a, const point& b) {
        point res;
        res.x = a.x - b.x;
        res.y = a.y - b.y;
        return res;
    }
    friend point operator+ (const point& a, const point& b) {
        point res;
        res.x = a.x + b.x;
        res.y = a.y + b.y;
        return res;
    }
    friend bool operator> (const point& a, const point& b) {
        return a.x > b.x || (a.x == b.x && a.y > b.y);
    }
    friend bool operator== (const point& a, const point& b) {
        return a.x == b.x && a.y == b.y;
    }
    friend bool operator!= (const point& a, const point& b) {
        return a.x != b.x || a.y != b.y;
    }
    friend bool operator< (const point& a, const point& b) {
        return a.x < b.x || (a.x == b.x && a.y < b.y);
    }
};
signed main() {
    FILE *pFile = fopen("input.txt", "r");
    if(pFile != nullptr) freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    while(true) {
        int n;
        cin >> n;
        if(n == 0) return 0;
        point a[n];

        for(int i = 0; i < n; i++) {
            cin >> a[i].x >> a[i].y;
        }
        int res = 0;
        for(int i = 0; i < n; i++) {
            for(int j = i + 1; j < n; j++) {
                for(int l = j + 1; l < n; l++) {
                    for(int k = l + 1; k < n; k++) {
                        point b[4] = {a[i], a[j], a[l], a[k]};
                        vector<point> con = convexHullMin(b, 4);
                        if((int)con.size() == 4) res++;
                    }
                }
            }
        }
        cout << res << "\n";
    }
}
```

### 

这个题没有我想象的那么困难，但是当时确实是没做出来



二维平面上有 N 个点，编号为 1 到 N。第 i 个点（1 <= i <= N）的坐标为 (X_i, Y_i)。在此保证，X 坐标和 Y 坐标分别都是 (1, 2, ……, N) 的一个排列。

请找出满足以下条件的 i 的数量：以 (0,0) 为左下角顶点、(X_i, Y_i) 为右上角顶点，且各边平行于 x 轴和 y 轴的矩形，其内部（不包含边界）不包含这 N 个点中的任何一个点。

**数据范围 (Constraints)**

- 1 <= N <= 3 *10^5
- 1 <= X_i, Y_i <= N
- X 和 Y 分别是 (1, 2, ……, N) 的排列。
- 所有输入数据均为整数。

**输入格式 (Input)**

输入通过标准输入（Standard Input）给出，格式如下：

Plaintext

```
N
X_1 Y_1
X_2 Y_2
...
X_N Y_N
```

**输出格式 (Output)**

输出一个整数，表示答案。

**样例 1 (Sample Input 1)**

**输入：**

Plaintext

```
3
2 1
1 3
3 2
```

**输出：**

Plaintext

```
2
```

**样例说明：**

- i = 1 和 i = 2 的两个点满足条件。
- 对于 i = 3，以 (0,0) 为左下角顶点、(3,2) 为右上角顶点的矩形，其内部包含点 1（即坐标为 (2, 1) 的点），因此不满足条件。



**思路**

我们首先发现如果一个点在另一个点内部，那么一定会有a1.x<a2.x&&a1.y<a2.y这个神奇的式子

如果我们写两个这个for循环，就直接时间坏掉了

那我们应该怎么做呢，答案是很简单，那我们固定住一x，给他从小到大排列起来。这样我们在后续的对比中就只需要比较w[i],w[i+1]的y，就ok了。因为默认x是大于等于上一个元素的x。如果y小于前一个元素，那么不等式不成立，但是可以把这个更小的y给存储起来，因为y更小更容易作为内部元素，以此类推，我们就能得到所有有内部元素的点。用总数n减去res，那么就是答案ans！

```c++
#include <bits/stdc++.h>

#define x first
#define y second

using namespace std;

typedef pair<int, int> PII;


int res = 0;
vector <PII> h;
int n;
int min_ = 0x3f3f3f3f;

int main(){
	
	cin >> n;
	for (int i = 0; i < n; i++) {
		int a, b;
		cin >> a >> b;
		h.push_back({ a,b });

	}

	sort(h.begin(), h.end());
	min_ = h[0].y;
	for (int i = 0; i < n; i++) {
		if (h[i].y > min_)res++;
		else {
			min_ = h[i].y;
		}
	}
	cout << n - res;
	return 0;
}
```


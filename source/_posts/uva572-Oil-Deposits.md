---
title: uva572-Oil-Deposits
tags:
  - uva
  - dfs
abbrlink: c4d7ec58
date: 2022-05-02 12:50:18
cover: https://images.pexels.com/photos/2748716/pexels-photo-2748716.jpeg?auto=compress&cs=tinysrgb&dpr=2&w=500
---

# 题目
- [UVA572 油田 Oil Deposits](https://www.luogu.com.cn/problem/UVA572)
- 输入一个m行n列的字符矩阵，统计字符“@”组成多少个八连块。如果两个字符“@”所在的格子相邻（横、竖或者对角线方向），就说它们属于同一个八连块。例如，图中有两个八连块。\
![uva572](../img/uva572.png)

# 思路
- 实际上就是求图的连通分量个数，一般用dfs
# C++实现
```c++
#include <cstdio> 
#include <cstring>
const int maxn = 100;
int m, n, idx[maxn][maxn];//连通分量编号 
char pic[maxn][maxn];

void dfs(int r, int c, int id){
	if(r < 0 || c < 0 || r >= m || c >= n) return;
	if(pic[r][c] != '@' || idx[r][c] > 0) return;
	idx[r][c] = id;
	for(int dx = -1; dx <= 1; dx++)
		for(int dy = -1; dy <= 1; dy++)
			if(dx != 0 || dy != 0) dfs(r+dx, c+dy, id);
}
int main(){	
	while(scanf("%d%d", &m, &n) == 2 && m && n){
		for(int i = 0; i < m; i++) scanf("%s", pic[i]);
		memset(idx, 0, sizeof(idx));
		int cnt = 0;
		for(int i = 0; i < m; i++)
			for(int j = 0; j < n; j++)
				if(idx[i][j] == 0 && pic[i][j] == '@') dfs(i, j, ++cnt);//连通分量数量++ 
		printf("%d\n", cnt);
	}
	return 0;
}
```
# Java实现
```java
public class Space {
	static int row=5, column=5;
	static char[][] arr = new char[][] {
		{'*','*','*','*','@'},
		{'*','@','@','*','@'},
		{'*','@','*','*','@'},
		{'@','@','@','*','@'},
		{'@','@','*','*','@'},
	};
	static int[][] idx = new int[row][column];
	
	public static void main(String[] args) {	
		
		int connect_component_id = 0;
		for(int i = 0; i < row; i++)
			for(int j = 0; j < column; j++)
				if(idx[i][j] == 0 && arr[i][j] == '@')
					dfs(i, j, ++connect_component_id);
		
		System.out.println(connect_component_id);
	}
	
	public static void dfs(int r, int c, int id) {
		if(r < 0 || c < 0 || r >= row || c >= column) return;
		if(arr[r][c] == '*' || idx[r][c] > 0) return; // ！=0 也可以
		idx[r][c] = id;
		for(int dx = -1; dx <= 1; dx++)
			for(int dy = -1; dy <= 1; dy++)
				if(dx != 0 || dy != 0) dfs(r+dx, c+dy, id);
	}
}
```
---
layout: post
title: 矩阵中的路径
date: 2020-07-20 
description: LeetCode刷题
img: post-7.jpg
tags: [Blog, LeetCode]
author: zyp
---
> 难度：中等 执行用时:54.75%
内存消耗:100%

### 这道题用到了深度搜索树(DFS)的思想：

- 深度优先搜索属于图算法的一种，英文缩写为DFS即Depth First Search.其过程简要来说是对每一个可能的分支路径深入到不能再深入为止，而且每个节点只能访问一次。
- 深度优先遍历图的方法是，从图中某顶点v出发：
 1. 访问顶点v；
 2. 依次从v的未被访问的邻接点出发，对图进行深度优先遍历；直至图中和v有路径相通的顶点都被访问；
 3. 若此时图中尚有顶点未被访问，则从一个未被访问的顶点出发，重新进行深度优先遍历，直到图中所有顶点均被访问过为止。

### 错误反思：

- 一开始使用visited数组记录已经访问过的顶点，浪费空间、时间，后通过在原数组进行修改作为记录。
- dfs函数中缺少了检测语句 'if (f) return;'，导致超时。

{% highlight ruby %}
class Solution {
public:
	bool in(int x, int y,int row, int col)
	{
		if (x >= 0 && x < row&&y >= 0 && y < col) {
			return true;
		}
		else
			return false;
	}
	void dfs(int x, int y,int row, int col, vector<vector<char>>& board,string& path,string word) {
		if (f) return;
		if (path == word)
		{
			f = true;
			return;
		}
		for (int i = 0; i < 4; i++) {
			int tx = x + dir[i][0];
			int ty = y + dir[i][1];
			if (in(tx, ty, row, col) && board[tx][ty] == word[path.length()]) {
				path.append(1, board[tx][ty]);
				board[tx][ty] = '*';
				dfs(tx, ty, row, col, board, path, word);
			}
		}
		board[x][y] = path[path.length() - 1];
		path.erase(path.length() - 1);
		return;
	}
	bool exist(vector<vector<char>>& board, string word) {
		if (word.empty()) return true;
		int x, y, row, col;
		string path;
		row = board.size();
		col = board[0].size();
		for (int i = 0; i < row; i++) {
			for (int j = 0; j < col; j++) {
				if (word[0] == board[i][j]) {
					x = i;
					y = j;
					path.append(1, word[0]);
					board[i][j] = '*';
					dfs(x, y, row, col, board, path, word);
				}
			}
		}
		return f;
	}

private:
	int dir[4][2] = { { 0,1 },{ -1,0 },{ 0,-1 },{ 1,0 } };
	bool f=false ;
};
{% endhighlight %}

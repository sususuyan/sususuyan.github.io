---
layout: post
title: 字符串的排列
date: 2020-09-09
description: LeetCode刷题
img: pcr-1.jpg
tags: [Blog, LeetCode]
author: zyp
---
> 难度：中等 执行用时：54.71% 内存消耗：18.01%

回溯法（深度优先搜索）

{% highlight ruby %}
class Solution {
public:
	vector<string> permutation(string s) {
		dfs(0, s);
		return result;
	}

	void dfs(int x, string s) {
		if (x == s.length() - 1) {
			result.push_back(s);
			return;
		}
		set<char> repeat;
		for (int i = x; i < s.length(); i++) {
			if (repeat.count(s[i])) continue;
			repeat.insert(s[i]);
			swap(i, x, s);
			dfs(x + 1, s);
			swap(i, x, s);
		}
	}
	void swap(int a, int b, string& s) {
		char tmp = s[a];
		s[a] = s[b];
		s[b] = tmp;
	}
public:
	vector<string> result;
};
{% endhighlight %}
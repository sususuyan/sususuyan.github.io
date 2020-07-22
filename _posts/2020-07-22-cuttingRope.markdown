---
layout: post
title: 剪绳子
date: 2020-07-22
description: LeetCode刷题
img: post-8.jpg
tags: [Blog, LeetCode]
author: zyp
---
> 难度：中等 执行用时：100% 内存消耗：100%

## 数论方法：

### 对于剪出的每一段绳子:
- 若长度大于4，继续剪才能得到最大乘积；
- 若长度等于4，继续剪也无法增大乘积；
- 若长度等于2或3，继续剪会减小乘积；
- 对于长度为2,3的绳子段，将绳子剪成尽可能多的长度为3的绳子段，可以得到更大的乘积。

{% highlight ruby %}
class Solution {
public:
    int cuttingRope(int n) {
		if (n == 2)return 1;
		if (n == 3)return 2;
		if (n == 4)return 4;
		if (n % 3 == 2) {
			return pow(3, n / 3) * 2;
		}
		else if (n % 3 == 0) {
			return pow(3, n / 3);
		}
		else {
			return pow(3, n / 3 - 1) * 4;
		}
	}
};
{% endhighlight %}

## 动态规划方法：

- 这道题还可以通过动态规划的思想解决。
- 动态规划算法基本思想是将待求解问题分解成若干个子问题，子问题并不是相互独立的，通过保存子问题的答案，
避免重复计算，节省时间。

{% highlight ruby %}
class Solution {
public:
    int cuttingRope(int n) {
        if (n == 2)
            return 1;
        if (n == 3)
            return 2;
        vector<int> dp(n+1);
        dp[1] = 1;
        dp[2] = 2;
        dp[3] = 3;
        for(int i = 4; i <= n; i++) {
            int maxValue = 0;
            for(int j = 1; j <= i/2; j++) {
                maxValue = max(maxValue, dp[j] * dp[i-j]);
            }
            dp[i] = maxValue;
        }
        return dp[n];
    }
};
{% endhighlight %}
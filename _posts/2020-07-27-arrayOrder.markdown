---
layout: post
title: 调整数组顺序
date: 2020-07-27
description: LeetCode刷题
img: post-6.jpg
tags: [Blog, LeetCode]
author: zyp
---
> 难度：简单 执行用时：5.59% 内存消耗：100%

这道题难度不高，但是自己的做法用时过长，记录两种快速算法。

## 首尾双指针

- 定义头指针left，尾指针right
- left一直右移，直到指向的值为偶数
- right一直左移，直到指向的值为奇数
- 交换nums[left]和nums[right]
- 重复操作，直到left==right

{% highlight ruby %}
class Solution {
public:
    vector<int> exchange(vector<int>& nums) {
        int left = 0, right = nums.size() - 1;
        while (left < right) {
            if ((nums[left] & 1) != 0) {
                left ++;
                continue;
            }
            if ((nums[right] & 1) != 1) {
                right --;
                continue;
            }
            swap(nums[left++], nums[right--]);
        }
        return nums;
    }
};
{% endhighlight %}

## 快慢双指针

- 定义指针fast和low
- fast搜索奇数位置，low指向下一个奇数应当存放的位置

{% highlight ruby %}
class Solution {
public:
    vector<int> exchange(vector<int>& nums) {
        int low = 0, fast = 0;
        while (fast < nums.size()) {
            if (nums[fast] & 1) {
                swap(nums[low], nums[fast]);
                low ++;
            }
            fast ++;
        }
        return nums;
    }
};
{% endhighlight %}

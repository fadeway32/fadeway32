---
layout: LeetCode23-[下一个排列]

title: LeetCode23-[下一个排列]

date: 2023-04-16 23:59:38

tags: LeetCode

categories: Web


top: 23

path: /article/leetcode23

abbrlink: 1177767760
---
[LeetCode23. 下一个排列](https://leetcode.cn/problems/next-permutation/)

<img src="https://gitee.com/fadeway32/fadeway32/raw/master/img/202304122207716.png" alt="image-20230412220747623" style="zoom:150%;" />

解答：



~~~java
class Solution {
    // 解决这题源于 离散数学几应用的算法（以 3 4 5 2 1为例子）
    // 从后往前寻找第一个出现的正序对 （找到 4 5）
    // 之后 5开始都可以逆序 所以翻转之后都是正序 3 4 1 2 5
    // 交换这两个值 得到3 5  1 2 4 
    // 对于初始为逆序的序列将在反转步骤直接完成
    public void nextPermutation(int[] nums) {
        int len = nums.length;
        if(len < 2) return;
        
        int i =len -1;
        while(i>0 && nums[i-1] >= nums[i]){
            i--;
        }
        reverse(nums,i,len-1);
        // 为0直接返回数组
        if(i==0)return;
        
        // 拿到交换的值
        int j = i-1;
        // //找到第一个比nums[j]大的元素，交换即可
        while(i < len && nums[j] >= nums[i]){
            i++;
        }
        // 然后交换
        int temp = nums[j];
        nums[j] =nums[i];
        nums[i] = temp;

    }

    public void  reverse(int[] nums,int left,int end){
            while(left < end){
                int temp = nums[end];
                nums[end] =nums[left];
                nums[left] = temp;
                end--;
                left++;
            }
    }
}









~~~


---

layout: LeetCode10-倒水面积最大

title: LeetCode10-倒水面积最大

date: 2023-03-02 23:49:30

tags: LeetCode

categories: Web


top: 10

path: /article/leetcode10

abbrlink: 1677767739

---
# LeetCode10 倒水面积最大



![image-20230304224607558](https://gitee.com/fadeway32/fadeway32/raw/master/img/202303042246619.png)

题目的意思是怎么才能接水最大

思路： 接水面积 = （两个柱子之间的长度 * 较短的那个柱子的高度）

~~~java
class Solution{
    
    public int getMaxVolume(int[] arry){
        int x = 0;
        int y = arry.length -1;
        int volume =0 ;
        // 向中间靠
        while(x < y){
            volume = Math.max(volume,Math.min(arry[x],array[y]) * (y-x));
            if(arry[x] < arry[y]){
                x ++;
            }else{
                y--;
            }
        }
        return volume;  
        
    }
   
}




~~~


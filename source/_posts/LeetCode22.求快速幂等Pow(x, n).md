---

layout: LeetCode22-[Pow(x, n)]

title: LeetCode22-[Pow(x, n)]

date: 2023-04-10 23:59:38

tags: LeetCode

categories: Web


top: 22

path: /article/leetcode22

abbrlink: 1177767759

---
#### [LeetC0de22. Pow(x, n)](https://leetcode.cn/problems/powx-n/)

<img src="https://gitee.com/fadeway32/fadeway32/raw/master/img/202304102229237.png" alt="image-20230410222957180" style="zoom:150%;" />

利用二分法处理 负数特殊处理

~~~java
class Solution {
    
    
    public double myPow(double x, int n) {
        long n1 =n;
        double res = 1;
        
        //对负数进行处理
        if(n1 < 0){
            x= 1/x;
            n1= -n1;
        }

        // 二分处理
        double temp =x;
        while(n1  > 0){
            // 判断奇偶数
            if( (n1 & 1)==1){
                res *= temp;
            } 
            // 得出 Math.pow(x,n)
            // 负数特殊处理
            temp *= temp;
            // 除2
            n1  >>= 1;
            
        }
        return res;
    }
}
~~~


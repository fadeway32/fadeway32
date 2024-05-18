---

layout: LeetCode07-求数字翻转

title: LeetCode07-求数字翻转

date: 2023-02-28 23:48:30

tags: LeetCode

categories: Web

description: LeetCode07-求数字翻转

top: 7

path: /article/leetcode07

abbrlink: 1677507585

---

# LeetCode07-求数字翻转





![image-20230227222919973](https://gitee.com/fadeway32/fadeway32/raw/master/img/202302272229030.png)

然后似乎不是那么理想。

![img](https://gitee.com/fadeway32/fadeway32/raw/master/img/202302272229480.jpeg)

为什么呢？倒置过来不应该是 9646324351 吗。其实题目里讲了，int 的范围是 [-2^{31} ,2^{31}-1][−231,231−1] 也就是 [-2147483648,2147483647][−2147483648,2147483647] 。明显 9646324351 超出了范围，造成了溢出。所以我们需要在输出前，判断是否溢出。

对于大于 intMax 的讨论，此时 x 一定是正数，pop 也是正数。

- 如果 rev > intMax / 10 ，那么没的说，此时肯定溢出了。
- 如果 rev == intMax / 10 = 2147483647 / 10 = 214748364 ，此时 rev * 10 就是 2147483640 如果 pop 大于 7 ，那么就一定溢出了。但是！如果假设 pop 等于 8，那么意味着原数 x 是 8463847412 了，输入的是 int ，而此时是溢出的状态，所以不可能输入，所以意味着 pop 不可能大于 7 ，也就意味着 rev == intMax / 10 时不会造成溢出。
- 如果 rev < intMax / 10 ，意味着 rev 最大是 214748363 ， rev * 10 就是 2147483630 , 此时再加上 pop ，一定不会溢出。

对于小于 intMin 的讨论同理。

~~~java

class Solution {
    
    public int reserve(int x){
        int ret =0;
        while(x !=0){
            int pop  = x % 10; // 余数
            x = x / 10; // 除数
            // 必须对Integer 进行判断
            if(x > Integer.MAX_VALUE /10){
                return 0;
            }
             if(x <Integer.MIN_VALUE/10){
                 return 0;
             }
            ret =  ret * 10 + pop;
        }
        return ret;
    }
    
}



~~~


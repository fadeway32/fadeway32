---

layout: LeetCode21-[两数相除]

title: LeetCode21-[两数相除]

date: 2023-04-10 23:49:38

tags: LeetCode

categories: Web


top: 21

path: /article/leetcode21

abbrlink: 1177767749

---

[Leetcode21. 两数相除](https://leetcode.cn/problems/divide-two-integers/)

<img src="https://gitee.com/fadeway32/fadeway32/raw/master/img/202304102139796.png" alt="image-20230410213937719" style="zoom:150%;" />

两数相除



~~~java
记住两个模板

// 二分模版
int l =0; r=102400000;
while(l < r){
    int mid = (1+r+1) >> 1;
    if(check(mid)){
        l =  mid;
    }else{
        r = mid -1;
    }
}

// 快速阶乘

int mua(double a,double b){
    int ans =0;
    while(b > 0){
        if( (b & 1 )==1){
            ans += a;
        }
        a += a;
        b>>=1;
    }
}

~~~



ans:

~~~java
class Solution{
    /*
    * 要考虑精度溢出+
   		 二分 + 倍增乘法
		由于题目限定了我们不能使用乘法、除法和 mod 运算符。

        我们可以先实现一个「倍增乘法」，然后利用对于 x 除以 y，结果 x / y 必然落在范围 [0, x] 的规律进行二分。

        作者：AC_OIer
        链接：https://leetcode.cn/problems/divide-two-integers/solution/shua-chuan-lc-er-fen-bei-zeng-cheng-fa-j-m73b/
        来源：力扣（LeetCode）
        著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
    */
    public int divide(int  a, int b){
       long x=a,y=b;
        //判断余数是否为负数 负数进行取反操作
        boolean isNeg= false;
        if( (x>0 && <0) || ( x <0 && y >0) ){
            isNeg=true;
        }
        if( x<0){
            x= -x;
        }
        if(y<0){
            y= -y;
        }
        // 二分法 然后利用对于 x 除以 y，结果 x / y 必然落在范围 [0, x] 的规律进行二分。
        long l = 0, r = x;
        while(l < r){
            long mid = 1+r+1 >>1
             if (mul(mid, y) <= x) {
                l = mid;
            } else {
                r = mid - 1;
            }
        }
        // 取left值 
        long ans = isNeg ? -l : l;
        // 特殊值判断
        if (ans > Integer.MAX_VALUE || ans < Integer.MIN_VALUE) return Integer.MAX_VALUE;
	    return (int)ans;

        
    }
    
     long mul(long a, long k) {
        long ans = 0;
        while (k > 0) {
            if ((k & 1) == 1) ans += a;
            k >>= 1;
            a += a;
        }
        return ans;
    }


    
    
    
    
    
}




~~~


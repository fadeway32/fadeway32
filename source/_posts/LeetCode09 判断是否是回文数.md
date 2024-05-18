---

layout: LeetCode09-判断是否是回文数

title: LeetCode09-判断是否是回文数

date: 2023-03-02 23:48:30

tags: LeetCode

categories: Web


top: 9

path: /article/leetcode09

abbrlink: 1677767738

---

# LeetCode09 判断是否是回文数



![image-20230304214613532](https://gitee.com/fadeway32/fadeway32/raw/master/img/202303042146609.png)

判断是不是回文数，负数不是回文数

ans：

~~~java

class  Solution{
    
    
   public boolean isPalindrome(int x) {
     if(x < 0){
        return false;
     }
      String  xStr =x +"";
      int len =xStr.length();
      boolean  oushu = len % 2 ==0;
      int x2 = 0;
      int y1 = (x2+len) /2 ;
      int x1=  ((x2+len) /2 ) -1;
      if(!oushu){
            y1 += 1;
      }
       while(x1 >=0 && y1 < len ){
              if((xStr.charAt(x1) - xStr.charAt(y1)) != 0){
                  return false;
              }
              x1 -= 1;
              y1 +=1;
          }
        return true;
    }
    // Math.log 是以自然对数的底数ee为底 求目标值得为对数值
    // e 约等于 2.71
    //  int digit = (int) (Math.log(x) / Math.log(10) + 1); //总位数
    
}







~~~


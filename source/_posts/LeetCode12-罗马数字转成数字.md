---

layout: LeetCode12-罗马数字转成数字

title: LeetCode12-罗马数字转成数字

date: 2023-03-02 23:49:33

tags: LeetCode

categories: Web


top: 12

path: /article/leetcode12

abbrlink: 1677767741

---

# LeetCode12-罗马数字转成数字

![image-20230306215031490](https://gitee.com/fadeway32/fadeway32/raw/master/img/202303062150550.png)

思路：例举出所有的情况 然后转成数字

~~~java
class Solution {
    public int romanToInt(String s) {
      int[] ints = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
      String[] str = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};
      int sum =0;
      for(int i =0 ; i <= str.length -1;i++){
             String dividStr = str[i];
             while(s.startsWith(dividStr)){
                  sum += ints[i];
                  s =s.replaceFirst(dividStr,"");
               
             }
           

      }
      return sum;
     
    }
}

~~~


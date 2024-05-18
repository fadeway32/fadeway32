---

layout: LeetCode11-数字转成罗马数字

title: LeetCode11-数字转成罗马数字

date: 2023-03-02 23:49:32

tags: LeetCode

categories: Web


top: 11

path: /article/leetcode11

abbrlink: 1677767740

---

# LeetCode11-数字转成罗马数字

![image-20230306205525485](https://gitee.com/fadeway32/fadeway32/raw/master/img/202303062055559.png)



解答：



~~~java
class Solution{
    
    // 注意特殊情况 C  X  I
    // CM 900 CD 400 XC 90 XL 40 IX 9 IV 4
    public String IntToRomanNumber(int x){
      int[] ints = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
      String[] str = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};
        String needStr="";
        for(int i=0;i< ints.length;i++){
            while(x >= ints[i]){
                x = x - ints[i];
                needStr += str[i];
            }

        }
        return needStr;
        
    } 
    
}



~~~


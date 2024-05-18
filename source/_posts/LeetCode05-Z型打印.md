---

layout: leetcode05打印Z型

title: LeetCode05打印Z型

date: 2023-02-28 22:48:30

tags: LeetCode

categories: Web

description: LeetCode05-打印Z型

top: 6

path: /article/leetcode05

abbrlink: 1677507385

---




# LeetCode05-Z型打印

<div/>

![image-20230227214113607](https://gitee.com/fadeway32/fadeway32/raw/master/img/202302272141667.png)

就是给定一个字符串，然后按写竖着的 「z」的方式排列字符，就是下边的样子。

![](https://gitee.com/fadeway32/fadeway32/raw/master/img/202302272142766.png)

解法一

~~~java
class Soultion{
    
    
    // 思路 对字符串进行分组，遍历 判断顺序 存入不同的list然后再进行toString();
    
    public String convert(String s,int numberRows){
        if(numberRows==1){
            return s;
        }
       List<StringBuilder> list =new ArrayList<>();
        // 分段
       for(int i =0;i<Math.min(numberRows,s.length());i++){
           list.add(new StringBuilder());
       }
       int curRow=0; //定义当前行
       boolean goDown =false;// 定义true会数组越界
       for(int i=0; i<s.length();i++){
          list.get(curRow).append(s.charAt(i));
          if(curRow == 0|| curRow == numberRows-1 ){
              goDown =!goDown;
          }
          curRow += goDown?1:-1;
       }
       String needStr="";
       for(StringBuilder sb: list){
           needStr += sb.toString();
       }
        return needStr;
    }
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
}













~~~


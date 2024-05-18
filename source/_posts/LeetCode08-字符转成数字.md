---

layout: LeetCode08-字符转成数字

title: LeetCode08-字符转成数字

date: 2023-03-01 23:48:30

tags: LeetCode

categories: Web

description: LeetCode08-字符转成数字 字符串处理的题目往往涉及复杂的流程以及条件情况，如果直接上手写程序，一不小心就会写出极其臃肿的代码。 因此，为了有条理地分析每个输入字符的处理方法，我们可以使用自动机这个概念： 我们的程序在每个时刻有一个状态 s，每次从序列中输入一个字符 c，并根据字符 c 转移到下一个状态 s'。这样，我们只需要建立一个覆盖所有情况的从 s 与 c 映射到 s' 的表格即可解决题目中的问题。

top: 8

path: /article/leetcode08

abbrlink: 1677767737

---

# LeetCode08 字符转成数字



![image-20230302212427430](https://gitee.com/fadeway32/fadeway32/raw/master/img/202303022124496.png)

方法一：

引入自动状态机概念

自动状态机 有四种状态： 

开始状态  -> 转换状态 -> 计算状态 -> 结束状态


![image-20230302224008826](https://gitee.com/fadeway32/fadeway32/raw/master/img/202303022240880.png)
~~~java

class Solution{
 
    
 class Automaton {
 int sign = 1;
 long ans = 0;
 final String START ="start";
 final String SIGN ="signd";
 final String IN_NUMBER="in_number";
 final String END ="end";
 String state = START;
 
 private Map<String, String[]> map = new HashMap<>(){{
     put("start",new String[]{START,SIGN,IN_NUMBER,END});
     put("signd",new String[]{END,END,IN_NUMBER,END});
     put("in_number",new String[]{END,END,IN_NUMBER,END});
     put("end",new String[]{END,END,END,END});
 }}
 
 private int getState(char c){
     if(c==' '){
         return 0;
     }
     if(c == '-'||c=='+'){
         return 1;
     }
     if(c >= '0' && c <= '9'){
         return 2;
     }
     return 3;
 }
     
 public void get(char c) {
  	state  = map.get(state)[getState(c)];
    if(IN_NUMBER.equals(state)){
       ans = ans * 10 + c - '0';
       if(sign == 1){
           ans =Math.min(ans,Integer.MAX_VALUE);
       }else{
           ans = Math.min(ans, -(long)Integer.MIN_VALUE);
       }
    }else if(SIGN.equals(state)){
        sign = c =='+'?1:-1;
    }
 }

 }
    
    
 public int myAtoi(String str) {
    Automaton an = new Automaton();
    char[]  charry =str.toCharArray();
 	for(char c : charry){
        an.get(c);
    }    
 	return an.sign * ((int)an.ans);
}




}










~~~


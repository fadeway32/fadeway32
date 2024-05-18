---

layout: LeetCode19-判断[括号生成]

title: LeetCode19-判断[括号生成]

date: 2023-03-18 23:49:38

tags: LeetCode

categories: Web


top: 19

path: /article/leetcode19

abbrlink: 1677767748

---

# LeetCode19 判断[括号生成](https://leetcode.cn/problems/generate-parentheses/)



<div class="test" style="align=left"><img src="https://gitee.com/fadeway32/fadeway32/raw/master/img/202303182211984.png" alt="image-20230318221109936" style="zoom:150%;align=left" /></div>



ans:

~~~java

class Solution {
	
	// 栈解决 利用先进后出的原理 及取反比较
    public boolean isValid(String s) {
        if("".equals(s) || s.length() == 0){
            return false;
        }
        int length = s.length();
       
    

       Stack<Character> stack = new Stack();
       for(char c : s.toCharArray()){
           if(c == '('){
               stack.push(')');
           }else if(c=='{')
                stack.push('}');
            else if(c=='[')
                stack.push(']');
            else if (stack.empty()||c!=stack.pop()){
                return false;
            }
       }
       if(stack.empty()){
            return true;
       }
       
       return false;

       
    }

}
~~~


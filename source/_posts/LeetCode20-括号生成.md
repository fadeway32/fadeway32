---

layout: LeetCode20-[括号生成]

title: LeetCode20-[括号生成]

date: 2023-03-19 23:49:38

tags: LeetCode

categories: Web


top: 20

path: /article/leetcode20

abbrlink: 1677767749

---

# [LeetCode20-括号生成](https://leetcode.cn/problems/generate-parentheses/)

![image-20230320210406081](https://gitee.com/fadeway32/fadeway32/raw/master/img/202303202104156.png)

ans:

~~~java
class Solution{
    
    
    //括号生成
     public List<String> ans = new ArrayList<>();
    public List<String> generateParenthesis(int n) {
        dfs(n,n,"");
        return ans;
    }
    public void  dfs(int left,int rigth,String str){
        if(left == 0 && rigth ==0){
            ans.add(str);
            return;
        }
        if(left > rigth){
            return;
        }
        if(left > 0){
            dfs(left-1,rigth,str+"(");
        }
        if(rigth > 0){
            dfs(left,rigth-1,str+")");
        }
    }
}
~~~


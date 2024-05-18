
---

layout: LeetCode04-求字符串最长长度

title: LeetCode04-求字符串最长长度

date: 2023-02-15 22:48:30

tags: LeetCode

categories: Web

description: 

top: 5

path: /article/leetcode04

abbrlink: 1305786657

---


# LeetCode04 求字符串最长长度

<div class="align1" style="algin:left"><img src="https://gitee.com/fadeway32/fadeway32/raw/master/img/202302252030621.png" 


给定一个字符串，找到没有重复字符的最长子串，返回它的长度。

~~~java

class Solution{
    // 暴力解法 
    public int lengthOfLongestSubstring(String s) {
        int len = s.length();
        int ans = 0;
        for(int i=0;i<len;i++){
            for(int j=1;j<=len;j++){
                if(allUnique(s,i,j)){
                    ans = Math.max(ans,j-i);
                }
            }
        }
        return ans;
        
    }
    
    public boolean allUnique(String str,int i,int j){
		Set<Character>  set=new HashSet<>();
        for(int start=i;start<j;start++){
            if(set.contains(str.charAt(start))){
                return false;
            }else{
                set.add(str.charAt(start));
            }
        }
        return true;
    }
    
    // 滑动窗口 推荐指数****
    public int lengthOfLongestSubstring2(String s) {
        int len =s.length();
        int max=0;
        int left=0;
        HashMap<Character,Integer> map = new HashMap<>();
        for(int i=0;i<len;i++){
            if(map.containsKey(s.charAt(i))){
                left = Math.max(left,map.get(s.charAt(i))+1); // 有重复的key只能向前移动一位
            }
            map.put(s.charAt(i),i); //更新最新的窗口下标
            max =  Math.max(max,i-left+1); //  比较最新的值
        }
        return max;
    } 
    
}





~~~


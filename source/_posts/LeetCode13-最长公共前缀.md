---

layout: LeetCode13-最长公共前缀

title: LeetCode13-最长公共前缀

date: 2023-03-02 23:49:34

tags: LeetCode

categories: Web


top: 13

path: /article/leetcode13

abbrlink: 1677767742

---

# LeetCode13-最长公共前缀

![image-20230307221519753](https://gitee.com/fadeway32/fadeway32/raw/master/img/202303072215808.png)

ans:

~~~java
class Solution{
    
    public String getLongestPrefix(String[] arrayStr){
        if(arrayStr == null || arrayStr.length == 0){
            return "";
        }
        int count =  arrayStr.length;
        int length = arrayStr[0].length();
        
        for(int i=0;i<length;i++){
            char firstChar = arrayStr[0].charAt(i);
            for(int j =0;j<count;j++){
                if(i == length || firstChar != arrayStr[i].charAt(j)){
                    return arrayStr[j].substring(0,i);
                }
                
            }
        }
        return arrayStr[0];
        
        
 
    }
    
    
    
    
    
    
}




~~~


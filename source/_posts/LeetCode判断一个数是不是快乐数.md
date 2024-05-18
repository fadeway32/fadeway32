
---

layout: LeetCode判断一个数是不是快乐数

title: LeetCode判断一个数是不是快乐数

tags: LeetCode

categories: Web

top: 35

path: /article/1713796331

abbrlink: 1713796331



date: 2024-04-21 22:32:00


---
# LeetCode判断一个数是不是快乐数



快乐数的定义： 对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和，然后重复这个过程直到这个数变为 1，或是无限循环但始终变不到 1。如果可以变为 1，那么这个数就是快乐数。



例如，19 就是一个快乐数。因为：

1² + 9² = 82

8² + 2² = 68

6² + 8² = 100

1² + 0² + 0² = 1



~~~java
class Solution{
    
    public boolean isHappyNum(int num){
        HashSet<Interger> sets = new HashSet<>();
        while(num != 1 && sets.contains(num)){
            sets.add(num);
            num = getSum(num);
        }
        return num == 1;
    }
    
    
    public int getSum(int num){
        int totalNum = 0;
        while(num > 0){
            int digit =  num %  10;
            int n = num / 10;
            totalNum = digit * digit ;
        }
        return totalNum;
    }
    
    
    
}
~~~


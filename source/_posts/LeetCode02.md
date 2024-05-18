
---

layout: leetcode02-two sum 链表逆序

title: LeetCode02-两数加法计算-链表逆序

date: 2023-02-15 22:08:30

tags: LeetCode

categories: Web

description: LeetCode 两数之和

top: 3

path: /article/leetcode02

abbrlink: 1305786655

---




LeetCode 两数相加



给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

https://gitee.com/fadeway32/fadeway32/raw/master/img/20230224213414.png



<div class="aligin" align="left"><img src="https://gitee.com/fadeway32/fadeway32/raw/master/img/20230224213414.png" style="zoom:100%;" /></div>



解法：



~~~java
class Solution{
    
    // 逆序添加1
    public ListNode addTwoNumber(ListNode1 l1,ListNode2 l2){
        int carry = 0;
        ListNode  pre = new ListNode();
        ListNode cur =pre;
         while(l1 != null || l2 != null){
             int val1 =l1 ==null?0:l1.val;
             int val2 =l2 == null?0:l2.val;
             int sum = (val1+val2)+carry;
             carry =  sum /10;
             sum =sum % 10;
             cur.next =new ListNode(sum);
             cur =cur.next;
             if(l1 !=null){
                 l1 =l1.next;
             }
             if(l2 != null){
                 l2 =l2.next;
             }
          
         }
        // 处理最后两位进位有可能为1的情况 但最大为1，因为 9+9<20在最尾巴加一
        if(carry==1){
            cur.next =new ListNode(carry);
        }
        
        return pre.next;
    }
    
    
}

~~~






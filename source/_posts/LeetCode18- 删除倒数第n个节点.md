---

layout: LeetCode18- 删除倒数第n个节点

title: LeetCode18- 删除倒数第n个节点

date: 2023-03-17 23:49:38

tags: LeetCode

categories: Web


top: 18

path: /article/leetcode18

abbrlink: 1677767747

---

# LeetCode18- 删除倒数第n个节点

![image-20230318211344007](https://gitee.com/fadeway32/fadeway32/raw/master/img/202303182113068.png)

ans:

~~~java
class Solution{
    
    // 常用写法
    public ListNode  deleteNode(ListNode head ,int  n){
        if(head = null)return null;
        
       	// 定义虚拟头节点dw
       ListNode dump  = new ListNode();
        dump.next = head;
        ListNode  cur = dump;
        // 先找出长度
        int length = getLength(head);
        for(int i=1;i< length-n+1;i++){
            cur =cur.next;
        }
        
       	cur.next = cur.next.next;
        return dump.next;
    }
    
    
    public int getLength(ListNode node){
        int length =0;
        while(node != null){
            ++length;
            node  = node.next;
        }
        return node;
    }
    
    
    public ListNode slowNode(ListNode head,int n){
        if(head = null)return null;
        
       	// 定义虚拟头节点dw
       ListNode dump  = new ListNode();
        dump.next = head;
        ListNode  cur = dump;
        ListNode slow = cur;
        ListNode fast =cur;
        for(int i=0;i<=n ;i++){
            fast = fast.next;
        }
        while(fast.next != null){
            fast = fast.next;
            slow = slow.next;
        }
        slow.next = slow.next.next;
        return dump.next;
        
    }
    
    
    
}



~~~


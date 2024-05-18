---

layout: LeetCode判断回文链表

title: LeetCode判断回文链表

tags: LeetCode

categories: Web

top: 36

path: /article/1715260887683

abbrlink: 1715260887683



date: 2024-05-09 21:21:00


---

# 判断回文链表





判断链表回文思路

1. **使用栈**：
   - 遍历链表，将所有元素依次入栈。
   - 再次遍历链表，同时从栈中弹出元素进行比较。
   - 如果链表中的元素和栈中弹出的元素完全一致，则链表是回文的。
2. **反转链表后半部分**：
   - 找到链表的中点（可以使用快慢指针法）。
   - 反转链表的后半部分。
   - 将前半部分和反转后的后半部分进行比较。
   - 如果两者相同，则链表是回文的。
   - 最后，恢复链表的后半部分（再次反转）。
3. **递归**：
   - 递归地检查链表的首尾元素是否相同。
   - 递归地将链表的首尾元素向

~~~java

这边使用第二种

class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}

class Solution{
    public boolean isPalindrome(ListNode head) {

        if(head == null || head.next == null) return true;
        // 找到链表的中点
        ListNode slow = head;
        ListNode fast = head;
        while(fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        // 反转链表的后半部分
        ListNode secondHalfStart = reverseList(slow.next);

        // 比较数据
        // 比较前半部分和反转后的后半部分
        ListNode p1 = head;
        ListNode p2 = secondHalfStart;
        boolean isPalindrome = true;
        while(isPalindrome && p2 != null) {
            if(p1.val != p2.val) isPalindrome = false;
            p1 = p1.next;
            p2 = p2.next;
        }

        // 恢复链表的后半部分
        slow.next = reverseList(secondHalfStart);
        return  isPalindrome;
    }

    private ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode curr = head;
        while(curr != null) {
            ListNode nextTemp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = nextTemp;
        }
        return prev;
    }



}


~~~


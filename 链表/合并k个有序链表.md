# 6.2打卡
# leetcode 23
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
 /**
 * 思路：讲k个链表两两合并，不断递归，直到全部合并
 * 时间复杂度：kn*logk
 * 空间复杂度：O(logk)
 */
class Solution {
    //合并两个链表
    public ListNode mergeTwoList(ListNode l1,ListNode l2){
       if(!(l1!=null&&l2!=null)){
           return l1==null?l2:l1;
       }
       ListNode head = new ListNode(-1);
       ListNode cur = head;
       while(l1!=null&&l2!=null){
           if(l1.val<l2.val){
               cur.next = l1;
               l1 = l1.next;
               cur = cur.next;
           }else{
               cur.next = l2;
               l2 = l2.next;
               cur = cur.next;
           }
       }
       cur.next = l1==null?l2:l1;
       return head.next;

    }
    //合并L到R之间的链表
    public ListNode mergeList(ListNode[] lists,int L,int R){
        if(L==R){
            return lists[L];
        }
        if(L>R){
            return null;
        }
        int mid = (R-L)/2+L;
        //递归调用，先合并L到mid，在合并mid+1到R，然后整体合并
        return mergeTwoList(mergeList(lists,L,mid),mergeList(lists,mid+1,R));
    }
    public ListNode mergeKLists(ListNode[] lists) {
        if(lists==null){
            return null;
        }
        return mergeList(lists,0,lists.length-1);
    }
}
```

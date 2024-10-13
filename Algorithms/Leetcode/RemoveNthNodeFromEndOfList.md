# Remove Nth node from End of Linked List

- Linked List
- Two pointers

## Problem Statement

Given the head of a linked list, remove the nth node from the end of the list and return its head.

**Example 1:**
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]

**Example 2:**
Input: head = [1], n = 1
Output: []

**Example 3:**
Input: head = [1,2], n = 1
Output: [1]

**Constraints:**

- The number of nodes in the list is sz.
- 1 <= sz <= 30
- 0 <= Node.val <= 100
- 1 <= n <= sz

## Intuition

My initial thought, was to somehow use recursion to solve this. The idea was that, the pointer moves to the end due to recursion, and when backtraces, the nth node can be figured out. However, the main issue here is that, we can't control the integer value during backtracking.

if n = 1 -> 2 -> 3 -> 4 during recursion

n = 4 -> 3 -> 2 -> 1 during backtracking.

So recursion cannot help here. I even thought of using another parameter in the function, still no success.

Then, i came across the Two-Pointer solution, by maintaining two pointers at nth distance and traversing both.

## Solution

```
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* leftptr = head;
        ListNode* rightptr = head;
        for(int i=0;i<n;i++)
        {
            if(rightptr != nullptr)
            {
                rightptr = rightptr->next;
            }
            else
            {
                break;
            }
        } 
        while(rightptr != nullptr && rightptr->next != nullptr)
        {
            rightptr = rightptr->next;
            leftptr = leftptr->next;
        }
        if(head == leftptr && rightptr == nullptr)
        {
            head = leftptr->next;
        }
        else if(leftptr->next != nullptr)
        {
            leftptr->next = (leftptr->next)->next;
        }
        return head;
    }
```
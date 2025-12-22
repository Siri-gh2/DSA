## 📌 Problem Link:
- [LeetCode – Add Two Numbers in LinkedList](https://leetcode.com/problems/add-two-numbers/description/))

---

## C++ Implementation


class Solution {

public:

    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    
        ListNode* dummy = new ListNode(0);
        ListNode* curr = dummy;
        int c = 0;
        
        while (l1 || l2 || c) {
            int x = (l1 != nullptr) ? l1->val : 0;
            int y = (l2 != nullptr) ? l2->val : 0;

            int sum = x + y + c;
            c = sum / 10;

            curr->next = new ListNode(sum % 10);
            curr = curr->next;

            if (l1) l1 = l1->next;
            if (l2) l2 = l2->next;
        }

        return dummy->next;
    }
};

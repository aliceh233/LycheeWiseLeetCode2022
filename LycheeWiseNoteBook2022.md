# Table of contents
- [Linked List](#linked-list)

## Linked List
Singly Linked List has head with a value and a pointer pointed to the next node, for each node there are a value and a pointer pointed to the next node.

Typical operations for Linked-list are:
- merge two Linked-list (LeetCode:21)

```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */


struct ListNode* mergeTwoLists(struct ListNode* list1, struct ListNode* list2){  
    //create a listnode called head
    struct ListNode head;
    //creat a pointer pointed to head
    struct ListNode *h = &head;
    
    //assert if two linked-lists are both NULL, if yes then return NULL
    if(list1==NULL && list2==NULL) {
        return NULL;
    }
    //assert if one of the linked-lists is NULL, if yes then return the other list
    if (list2 == NULL) {
        return list1;
    }
    if (list1 == NULL) {
        return list2;
    }
    // create a loop to check if the pointer points to a NULL node then stop
    while (list1 != NULL && list2 != NULL) {
        
        if (list1->val < list2->val) {
            // if list1 has a value smaller than list2, we can 
            // the header will pointer to the list1 
            // (CAUTION: it is the header's next pointer pointed to the list1, if we make h = list1, we will lose the pointer and also change the value of last node)
            h->next = list1;
            // move list1's pointer to list1's next node
            list1 = list1->next;
            // move header pointer to next node
            // now it is the list1 node we just pointed to!
            h = h->next;
            
        } else {
            //same here
            h->next = list2;
            list2 = list2->next;
            h = h->next;
        }
    }
    // if two linked-list don't have the same amount of nodes
    // the rest of nodes will attach to the end.
    if (list1 != NULL) {
        h->next = list1;
    }
    if (list2 != NULL) {
        h->next = list2;
    }
    
    // This is the magic! we return the next node of the header node we created, not the           
    // pointer, because the pointer h now is pointing to the lastest node.
    return head.next;
}
```

Linked List have different transformations as following:

- Double Linked List: Double Linked List has a head pointed to next node, for each node there are a value, a pointer pointed to the last node, and a pointer pointed to the next node.
- Static List
- Symmetric Matrix
- Sparse Matrix
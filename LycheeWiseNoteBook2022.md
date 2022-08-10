# Table of contents
- [Linked List](#linked-list)

## Linked List
Singly Linked List has head with a value and a pointer pointed to the next node, for each node there are a value and a pointer pointed to the next node.

### Leetcode for Linked-list:
- merge two Singly Linked-list (LeetCode:21)

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

- merge k sorted linked-list array (Leetcode: 23): that's a smart solution from *zhazhalaila*
```c
// This solution is so smart and has only 20ms runtime, Zhazhalaila did it by comparing all the nodelist pairs by pairs. its algorithm is similar to merge sort. 

//his/her/their instructions:
/*
Recursive and resursive to solve this problem.
We can imagine construct a binary tree to absorb recursion.
                       result
					   /     \
					  A       B
					 / \      / \
					C   D    E   F
At the begin, we merge C and D to get CD. Then we merge CD and A to get ACD. Then we merge E and F to get EF. Then we merge EF and B to get BEF. Last, we merge ACD and BEF to get result.
*/

typedef struct ListNode Node;
Node* partion(Node** lists, int start, int end);
Node* mergeTwoLists(Node* l1, Node* l2);

struct ListNode* mergeKLists(struct ListNode** lists, int listsSize) {
    //compare all lists from 0 to the end.
    return partion(lists, 0, listsSize-1);
}

Node* partion(Node** lists, int start, int end) {
    //if start is the end, that means there is only one list in this list, return that list.
    if (start == end)
        return lists[start];
    // if there is still much list we need to sort:
    if (start < end) {
        //define where is the middle point
        int middle = (start + end) / 2;
        //operate left lists recursively
        Node* l1 = partion(lists, start, middle);
        //operate right lists recursively 
        Node* l2 = partion(lists, middle+1, end);
        //now merge two sorted link-list
        return mergeTwoLists(l1, l2);
    } else {
        return NULL;
    }
}

Node* mergeTwoLists(struct ListNode* l1, struct ListNode* l2) {
    //base cases
    if(l1 == NULL && l2 == NULL)
        return NULL;
    if (l1 == NULL)
        return l2;
    if (l2 == NULL)
        return l1;
    //a temp node
    Node* new_node;
    //if l1's value is bigger or equal to l2, then assign the temp value as l2, the next value will be compare with l1 recursively
    if (l1->val >= l2->val) {
        new_node = l2;
        new_node->next = mergeTwoLists(l1, l2->next);
    } else {
        new_node = l1;
        new_node->next = mergeTwoLists(l1->next, l2);
    }
    return new_node;
}
```


Linked List have different transformations as following:

- Double Linked List: Double Linked List has a head pointed to next node, for each node there are a value, a pointer pointed to the last node, and a pointer pointed to the next node.
- Static List
- Symmetric Matrix
- Sparse Matrix
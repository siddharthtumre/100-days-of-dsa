---
title: "Day 5 - Hacker Data Structures(Linked Lists)"
date: "2022-06-13"
---
## Solved Problems
[Delete duplicate-value nodes from a sorted linked list](https://www.hackerrank.com/challenges/delete-duplicate-value-nodes-from-a-sorted-linked-list/problem)

```cpp
SinglyLinkedListNode* removeDuplicates(SinglyLinkedListNode* llist) {

    SinglyLinkedListNode *head = llist;

    while(head->next!=NULL){
        if(head->next->data == head->data){
            head->next = head->next->next;
        }else{
            head = head->next;  
        }
    }
    return llist;
}
```

[Cycle Detection](https://www.hackerrank.com/challenges/detect-whether-a-linked-list-contains-a-cycle/problem)

```cpp
bool has_cycle(SinglyLinkedListNode* head) {

    SinglyLinkedListNode *slow, *fast;
    slow = head;
    fast = head;

    while(slow!=NULL && fast!=NULL && fast->next!=NULL){
        slow = slow->next;
        fast = fast->next->next;

        if(slow==fast){
            return 1;
        }
    }
    return 0;
}
```

[Find Merge Point of Two Lists](https://www.hackerrank.com/challenges/find-the-merge-point-of-two-joined-linked-lists/problem)

```cpp
int findMergeNode(SinglyLinkedListNode* head1, SinglyLinkedListNode* head2) {

    int len1 = 0;
    int len2 = 0;

    SinglyLinkedListNode *current1 = head1;
    while(current1!=NULL){
        len1++;
        current1=current1->next;

    }

    SinglyLinkedListNode *current2 = head2;
    while(current2!=NULL){
        len2++;
        current2=current2->next;

    }

    if(len1>len2){
        int count=len1-len2;
        while(count!=0){
            count--;
            head1 = head1->next;
        }

    }else{
        int count=len2-len1;
        while(count!=0){
            count--;
            head2 = head2->next;
        }

    }

    while(head1!=head2){
        head1=head1->next;
        head2=head2->next;
    }

    return head1->data;
}
```

[Reverse a doubly linked list](https://www.hackerrank.com/challenges/reverse-a-doubly-linked-list/problem)

```cpp
DoublyLinkedListNode* reverse(DoublyLinkedListNode* llist) {
    DoublyLinkedListNode *cur = llist;
    DoublyLinkedListNode *temp = NULL;

    while(cur!=NULL){
        temp = cur->prev;
        cur->prev = cur->next;
        cur->next = temp;
        
        cur = cur->prev;
    }
    
    if(temp!=NULL){
        llist = temp->prev;
    }
    return llist;
}
```

[Merge two sorted linked lists](https://www.hackerrank.com/challenges/merge-two-sorted-linked-lists/problem?isFullScreen=true)

```cpp
SinglyLinkedListNode* mergeLists(SinglyLinkedListNode* head1, SinglyLinkedListNode* head2) {
    SinglyLinkedListNode *mergedList = new SinglyLinkedListNode(-1);
    
    SinglyLinkedListNode *temp = mergedList;
    while(head1!=NULL && head2!=NULL){
        if(head1->data<=head2->data){
            temp->next = head1;
            head1=head1->next;
        }else if(head1->data>head2->data){
            temp->next = head2;
            head2=head2->next;
        }
        temp = temp->next;
    }
    
    if(head1!=NULL){
            temp->next = head1;
    }else if(head2!=NULL){
        temp->next = head2;
    }
    
    return mergedList->next;
}
```

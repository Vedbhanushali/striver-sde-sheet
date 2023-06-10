# Day 2

## Pascal Triangle 

https://www.codingninjas.com/codestudio/problems/pascal-s-triangle_8230805?challengeSlug=striver-sde-challenge

### Approach - 
formula to caluculate value of element is  
**start c = 1**  
**and c = c*(i-j)/(j);**   
**remeber this.** 

```
#include <bits/stdc++.h>

vector<vector<long long int>> printPascal(int n) 
{
  // Write your code here.
  vector<vector<long long int>> answer;
        long long int c = 1;
        for(int i=1;i<=n;i++){
            c=1;
            // cout<<c;
            vector<long long int> temp;
            temp.emplace_back(c);
            for(int j=1;j<i;j++){
                c = c*(i-j)/(j);
                temp.emplace_back(c);
                // cout<<c;
            }
            // cout<<endl;
            answer.emplace_back(temp);
        }
        return answer;
}

```
 
## Reverse a LinkedList - 

https://www.codingninjas.com/codestudio/problems/reverse-linked-list_8230724?challengeSlug=striver-sde-challenge

### Approach 
will need prev and after pointer , will move such way that curr will point back to prev and will move all three pointers forward such a way that prev points to curr , curr points to after , and after points to next of curr node.

```
#include <bits/stdc++.h>

/****************************************************************

    Following is the class structure of the LinkedListNode class:

    template <typename T>
    class LinkedListNode
    {
    public:
        T data;
        LinkedListNode<T> *next;
        LinkedListNode(T data)
        {
            this->data = data;
            this->next = NULL;
        }
    };

*****************************************************************/

LinkedListNode<int> *reverseLinkedList(LinkedListNode<int> *head) 
{
    // Write your code here
    LinkedListNode<int>* prev = NULL;
    LinkedListNode<int>* curr = head;
    
    while(curr!=NULL){
            LinkedListNode<int>* forward = curr->next;
            curr->next = prev;
            prev = curr;
            curr = forward;
    }
    //prev contains head
    // head = prev;
    return prev;
}
```
## Middle Of Linked List - 

https://www.codingninjas.com/codestudio/problems/middle-of-linked-list_8230764?challengeSlug=striver-sde-challenge&leftPanelTab=0


## Appproach
will use two pointer approach one slow pointer and second fast pointer , fast pointer moves two nodes and slow pointer moves one node when fast pointer reaches the last node slow pointer would be pointing to the middle of the node.

```
/*
Following is the class structure of the Node class:

class Node
{
public:
    int data;
    Node *next;
    Node()
    {
        this->data = 0;
        next = NULL;
    }
    Node(int data)
    {
        this->data = data; 
        this->next = NULL;
    }
    Node(int data, Node* next)
    {
        this->data = data;
        this->next = next;
    }
};
*/

Node *findMiddle(Node *head) {
    // Write your code here
    Node* fast = head;
    Node* slow = head;

    while(fast!=NULL){
        fast = fast->next;
        if(fast!=NULL){
            slow = slow->next;
            fast = fast->next;
        }
    }
    return slow;
}


```
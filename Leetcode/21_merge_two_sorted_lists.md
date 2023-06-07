# 21. Merge Two Sorted Lists
You are given the heads of two sorted linked lists list1 and list2.

Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

## Example 1: 
```
Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]
```

## Example 2: 
```
Input: list1 = [], list2 = []
Output: []
```

## Example 3: 
```
Input: list1 = [], list2 = [0]
Output: [0]
```

## Constraints: 
```
The number of nodes in both lists is in the range [0, 50].
-100 <= Node.val <= 100
Both list1 and list2 are sorted in non-decreasing order.
```

## My Solution: 
```js
const mergeTwoLists = (list1, list2) => {
    // Create a new blank node referencing the head node.
    const head = new ListNode();
    // Create another variable to track new nodes that are added to the head node.
    let current = head;
    // Loop through both input list nodes while both nodes exist.
    while(list1 && list2) {
        // Compare the nodes from list1 and list2. If list1's node represents a smaller value compared to that of list2's, assign it to current.next so that the list node is head (blank) -> list1. Then, have list1 point to the next node in its list.
        if(list1.val < list2.val) {
            current.next = list1.val;
            list1 = list1.next;
        } 
        // Same idea, but the opposite for when list2's node has smaller value.
        else {
            current.next = list2.val;
            list2 = list2.next;
        }
    }
    // By the time we jump out of the while loop, at least one of the lists should be null. Whatever that is remaining will be assigned to current.next, so we have head -> first current -> second current -> ... -> last current -> whatever that is remaining from either list1 or list2. 
    current.next = list1 || list2;
    // If we return head, we would return a blank node along with the two lists sorted. We need to return head.next, which starts with the first node we got from the first iteration of the while loop. 
    return head.next;
}
```
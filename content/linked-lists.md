---
title: "Linked Lists"
layout: "bundle"
outputs: ["Reveal"]
date: 2020-05-19T23:36:32+10:00
---

{{< slide class="center" >}}

## Linked Lists

---

## Linked Lists

A linked list is a data structure, where a sequence of values is scattered throughout the memory, but is still contiguous to the user.  

They are used in the implementation of other data structures (i.e. Stacks and Queues)

---

## Why Linked Lists

{{% section %}}

_Managing memory is important to program efficiency._  

||Linked List|Array|
|---:|:------:|:---:|
|Overhead|Little<!-- Amortisation! -->|<u>***None***</u>|
|Access|Sequential|<u>***Random***</u>|
|Size|<u>***Variable***</u>|Fixed|
|Expansion|<u>***Cheap***</u>|Expensive|

---

{{<slide transition="fade" >}}

### Array Expansion (Low Load)

> ```
|X|X|X| | | | | | | | | | | | | | | | | | |
```

```c
char *X = malloc(3); // Allocate 3 bytes for X
X = realloc(X, 5); // Request 5 bytes for X
```
> ```
|X|X|X|X|X| | | | | | | | | | | | | | | | |
```

The additional two bytes were assigned in place, good.

---

{{<slide transition="fade" >}}

### Array Expansion (Medium Load)

> ```
|X|X|X|O|O|O|O|O| | | | | | | | | | | | | |
```

```c
char *X = malloc(3); // Allocate 3 bytes for X
char *O = malloc(5); // Allocate 5 bytes for O
X = realloc(X, 5); // Request 5 bytes for X
```

> ```
| | | |O|O|O|O|O|X|X|X|X|X| | | | | | | | |
```

The original location did not have enough free contiguous space. Location was moved.  
Data has to be copied to the new location.

---

{{<slide transition="fade" >}}

### Array Expansion (High Load)

> ```
|X|X|X|O|O|O|O|O|O|O|O|O|O|O|O|O|O| | | | |
```

```c
char *X = malloc(3); // Allocate 3 bytes for X
char *O = malloc(14); // Allocate 14 bytes for O
X = realloc(X, 5); // Request 5 bytes for X
// Program Crash!
```

The original location did not have enough free contiguous space. There is no other memory location that has enough free contiguous space.  

The program will crash!

---

{{<slide transition="fade" >}}

### Linked List Expansion (High Load)

> ```
|X|x|X|x|O|O|O|O|O|O|O|O| | |Y| | |Z|Z| | |
```

```c
LinkedList X = new_linked_list(2); // Create a linked list
char *O = malloc(8); // Allocate 8 bytes for O
char *Y = malloc(1); // Allocate 1 byte for Y
char *Z = malloc(2); // Allocate 2 bytes for Z
add_nodes(X, 3); // Request 3 more nodes for X
```

> ```
|X|x|X|x|O|O|O|O|O|O|O|O|X|x|Y|X|x|Z|Z|X|x|
```

With a linked list, our data does not need to be stored in the same location.

---

Use arrays when you have a finite number of items.  

Use linked lists when you have a dynamic amount.


{{% /section %}}

---

## Basic Structure

{{% section %}}

```c
struct LinkedList {
  struct LinkedList_Node *head;
};

struct LinkedList_Node {
  int value;
  struct LinkedList_Node *next;
};

/* ... */
struct LinkedList *createLinkedList();
struct LinkedList_Node *createLinkedListNode(int value);
```

We define `struct LinkedList` to be a container which keeps track of the start of the list. We also define `struct LinkedList_Node` which contains the node's value, and a pointer to the next node.

---

```c
typedef struct LinkedList {
  LinkedListNode *head;
} LinkedList;

typedef struct LinkedList_Node {
  int value;
  LinkedListNode *next;
} LinkedListNode;

/* ... */
LinkedList *createLinkedList();
LinkedListNode *createLinkedListNode(int value);
```

Using `typedef`s, we can reduce redundancy and make our code more succinct.

---

```c
typedef struct LinkedList_Node *LinkedListNode;
struct LinkedList_Node {
  int value;
  LinkedListNode next;
};

typedef struct LinkedList {
  LinkedListNode head;
} *LinkedList;

/* ... */
LinkedList createLinkedList();
LinkedListNode createLinkedListNode(int value);
```

We can `typedef` our `LinkedListNode` and `LinkedList` to be pointers to their struct types.

{{% /section %}}

---

## Linked List Operations

* Create / Destroy
* Insert
* Search
* Delete
* Sort
* Count

---

## Container Initialisation

```c
LinkedList *createLinkedList() {
    // Allocate the memory for just the container
    LinkedList container = malloc(sizeof(*container));
    if (container == NULL) return;

    // Initialise values
    container->next = NULL;

    // Give the address of the LinkedList container
    return container;
}
```

```c
int main() {
    LinkedList list = createLinkedList();
}
```

---

## Node Initialisation

```c
LinkedListNode *createLinkedListNode(int data) {
    // Allocate the memory for the node
    LinkedListNode node = malloc(sizeof(*node));
    if (container == NULL) return;

    // Initialise values
    node->value = data;
    node->next = NULL;

    // Give the address of the LinkedListNode
    return node;
}
```

```c
int main() {
    LinkedList list = createLinkedList();
    LinkedListNode node = createLinkedListNode(5);
}
```

---

## Insertion

{{% section %}}

```c
void LinkedListInsert(LinkedList container, int data) {
    // Check that the container exists
    /* ... */

    // Create the LinkedListNode (also check for error)
    /* ... */

    // Add the LinkedListNode to the end of container
    /* ... */
    // ... What if the container is empty?
    // ... What if the container has one item?
    // ... What if the container has two items?
    // ... What if the container has n items?
}
```

---

```c
void LinkedListInsert(LinkedList container, int data) {
    // Check that the container exists
    if (container == NULL) return;

    // Create the LinkedListNode (also check for error)
    LinkedList node = createLinkedListNode(data);
    if (node == NULL) return;

    // Add the LinkedListNode to the end of the container
    if (container->head == NULL) {
        container->head = cur;
        return;
    }

    // Find the last node in the Linked List
    LinkedListNode cur = container->head;
    while (cur->next != NULL) {
        cur = cur->next;
    }

    // Reassign the last node to point to our new node
    cur->next = node;
}
```

{{% /section %}}

---

## Count

```c
int LinkedListCount(LinkedList container) {
    // Check that the container exists
    if (container == NULL) return -1;
    
    int count = 0;
    LinkedListNode cur = container->head;
    while (cur) {
        // For each node, increment the count
        count++;
        cur = cur->next;
    }

    return count;
}
```

---

## Search

```c
boolean LinkedListSearch(LinkedList container, int data) {
    if (container == NULL) return false;

    LinkedListNode cur = container->head;
    while (cur) {
        // Return true if the node matches the data
        if (cur->value == data) {
            return true;
        }
        cur = cur->next;
    }

    return false;
}
```

---

{{< slide transition="fade" >}}

## Deletion by Value

Delete one node with the value in `data`

```c
boolean LinkedListNodeDeleteByVal(LinkedList container, int data) {
    if (container == NULL) return false;

    LinkedListNode cur = container->head;
    LinkedListNode prev = NULL;
    while (cur) {
        if (cur->value == data) {
            if (prev == NULL) {
                container->head = cur->next;
            } else {
                prev->next = cur->next;
            }
            free(cur);
            return true;
        }
        prev = cur;
        cur = cur->next;
    }

    return false;
}
```

---

## Deletion by Value (All)

Delete one node with the value in `data`

```c
void LinkedListNodeDeleteByVal(LinkedList container, int data) {
    if (container == NULL) return;

    LinkedListNode cur = container->head;
    LinkedListNode prev = NULL;
    while (cur) {
        if (cur->value == data) {
            if (prev == NULL) {
                container->head = cur->next;
            } else {
                prev->next = cur->next;
            }
            free(cur);
        }
        prev = prev->next;
        cur = prev->next;
    }
}
```

---

## Deletion by Node

```c
boolean LinkedListNodeDeleteByNode(LinkedList container, LinkedListNode node) {
    if (container == NULL) return;
    if (node == NULL) return;

    if (container->head == node) {
        container->head = node->next;
        free(node);
        return true;
    }

    LinkedListNode cur = container->head;
    while (cur) {
        if (cur->next == node) {
            cur->next = node->next;
            free(node);
            return true;
        }
        cur = cur->next;
    }

    return false;
}
```

---

## Destruction

{{% section %}}

```c
void LinkedListFree(LinkedList container) {
    if (container == NULL) return;

    LinkedListNode cur = container->head;
    while(cur) {
        LinkedListNode next = cur->next;
        free(cur);
        cur = next;
    }

    free(container);
}
```

---

```c
void BAD_LinkedListFree(LinkedList container) {
    if (container == NULL) return;

    LinkedListNode cur = container->head;
    while(cur) {
        free(cur);
        cur = cur->next;
    }

    free(container);
}
```

Why shouldn't we do it this way?  
{{%fragment%}}As we've released the memory for `cur`,<br/>`cur->next` will be gibberish{{%/fragment%}}

{{% /section %}}

---

## Sort

* Bubble Sort (By changing value)
* Bubble Sort (By changing reference)

---

## Merge

Implement a linked list function that merges two linked lists together.

---

## Complexity Analysis

// Calculate these!

<!-- It's O(n) for most operations, O(1) for insertion and deletion -->

---

## Improved Structure

```c
typedef struct LinkedList_Node *LinkedListNode;
struct LinkedList_Node {
  int value;
  LinkedListNode next;
};

typedef struct LinkedList {
  LinkedListNode head;
  LinkedListNode tail;
  int count;
} *LinkedList;

/* ... */
LinkedList createLinkedList();
LinkedListNode createLinkedListNode(int value);
```

---

## Improved Initialisation

```c
LinkedList createLinkedList() {
    LinkedList container = malloc(sizeof(*container));
    container->head = NULL;
    container->tail = NULL;
    container->size = 0;
    return container;
}
```

## Improved Insertion

```c

void LinkedListInsert(LinkedList container, int data) {
    if (container == NULL) return;

    LinkedList node = createLinkedListNode(data);
    if (node == NULL) return;

    container->count++;

    // Add the LinkedListNode to the end of the container
    if (container->head == NULL) {
        container->head = cur;
        container->tail = cur;
        return;
    }

    container->tail->next = node;
    container->tail = node;
}
```

## Improved Count

```c
int LinkedListCount(LinkedList container) {
    // Check that the container exists
    if (container == NULL) return -1;

    return container->count;
}
```

---

<!-- pointer pointers! -->
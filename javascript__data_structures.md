# Data Structures

## Singly Linked List and 

A singly linked list only has access to the node after it. Doubly linked list have access to the previous node and the next node. For a list to perform successfully it must know about two nodes.  The head node and the tail node. 

### Operations on linked lists

- Adding a node to the head
- Adding a node to the tail
- Removing the head 
- removing the tail
- searching the list

### Structure of a node

Each node has the following

- value: the value a node is holding
- next: next node
- prev: previous node

```javascript
function Node(value, next, prev) {
  this.value = value;
  this.next = next;
  this.prev = prev;
}
```

### Structure of a LinkedList

- head: The first node in a list
- tail: The last node in a list

```javascript
function LinkedList() {
  this.head = null;
  this.tail = null;
}
```

## Adding a node to the head

```javascript
LinkedList.prototype.addToHead = function(value) {
  const newNode = new Node(value, this.head, null);
  if (this.head) this.head.prev = newNode;
  else this.tail = newNode;
  this.head = newNode;
}
```

## Adding a node to the tail

```javascript
LinkedList.prototype.addToTail = function(value) {
  const newNode = new Node(value, null, this.tail);
  if (this.tail) this.tail.next = newNode;
  else this.head = newNode;
  this.tail = newNode;
}
```

## Removing a node from the head

```javascript
LinkedList.prototype.removeHead = function() {
  if (!this.head) return null;
  const val = this.head.value;
  this.head = this.head.next;
  if (this.head) this.head.prev = null;
  else this.tail = null;
  return val;

}
```

## Removeing a node from the tail

```javascript
LinkedList.prototype.removeTail = function() {
  if (!this.tail) return null;
  const val = this.tail.value;
  this.tail = this.tail.prev;
  if (this.tail) this.tail.next = null;
  else this.head = null;
  return val;

}
```


[Back](javascript.md)
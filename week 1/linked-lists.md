
# Go Linked Lists

## Introduction
In Go, a linked list is a data structure consisting of a sequence of nodes, each containing its own data and a reference (or link) to the next node in the sequence.

## Implementing a Linked List
Since Go doesn't have a built-in linked list, it's often implemented using structs.

### Defining a Node
```go
type Node struct {
    Data int
    Next *Node
}
```

### Defining a Linked List
```go
type LinkedList struct {
    Head *Node
    Tail *Node
}
```

## Basic Operations

### Adding Elements
```go
func (l *LinkedList) Append(data int) {
    newNode := &Node{Data: data}
    if l.Head == nil {
        l.Head = newNode
        l.Tail = newNode
    } else {
        l.Tail.Next = newNode
        l.Tail = newNode
    }
}
```

### Traversing the List
```go
func (l *LinkedList) Display() {
    for current := l.Head; current != nil; current = current.Next {
        fmt.Println(current.Data)
    }
}
```

### Searching for an Element
```go
func (l *LinkedList) Find(data int) *Node {
    for current := l.Head; current != nil; current = current.Next {
        if current.Data == data {
            return current
        }
    }
    return nil
}
```

### Deleting an Element
```go
func (l *LinkedList) Delete(data int) {
    if l.Head == nil {
        return
    }

    if l.Head.Data == data {
        l.Head = l.Head.Next
        return
    }

    for current := l.Head; current.Next != nil; current = current.Next {
        if current.Next.Data == data {
            current.Next = current.Next.Next
            if current.Next == nil {
                l.Tail = current
            }
            return
        }
    }
}
```

## Doubly Linked Lists
A doubly linked list allows traversal in both directions. Each node has two links: next and prev.

### Defining a Doubly Linked List Node
```go
type DoublyNode struct {
    Data int
    Next *DoublyNode
    Prev *DoublyNode
}
```

### Example: Insertion in a Doubly Linked List
```go
func (l *LinkedList) InsertAtFront(data int) {
    newNode := &DoublyNode{Data: data}
    newNode.Next = l.Head
    if l.Head != nil {
        l.Head.Prev = newNode
    }
    l.Head = newNode
}
```

## Circular Linked Lists
A circular linked list is a sequence of nodes in which the last node points back to the first node.

### Example: Creating a Circular Linked List
```go
func (l *LinkedList) CreateCircular(data int) {
    newNode := &Node{Data: data}
    if l.Head == nil {
        l.Head = newNode
        newNode.Next = l.Head
    } else {
        newNode.Next = l.Head.Next
        l.Head.Next = newNode
    }
}
```

## Complex Algorithms
Implementing algorithms such as reversing a linked list or detecting a cycle.

### Example: Reversing a Linked List
```go
func (l *LinkedList) Reverse() {
    var prev, next *Node
    current := l.Head
    for current != nil {
        next = current.Next
        current.Next = prev
        prev = current
        current = next
    }
    l.Head = prev
}
```

### Example: Detecting a Cycle
```go
func (l *LinkedList) HasCycle() bool {
    slow := l.Head
    fast := l.Head
    for fast != nil && fast.Next != nil {
        slow = slow.Next
        fast = fast.Next.Next
        if slow == fast {
            return true
        }
    }
    return false
}
```

## Example: Full Program
Here is a complete example showcasing a simple linked list implementation.

```go
package main

import "fmt"

type Node struct {
    Data int
    Next *Node
}

type LinkedList struct {
    Head *Node
    Tail *Node
}

func (l *LinkedList) Append(data int) {
    newNode := &Node{Data: data}
    if l.Head == nil {
        l.Head = newNode
        l.Tail = newNode
    } else {
        l.Tail.Next = newNode
        l.Tail = newNode
    }
}

func (l *LinkedList) Display() {
    for current := l.Head; current != nil; current = current.Next {
        fmt.Println(current.Data)
    }
}

func main() {
    list := &LinkedList{}
    list.Append(1)
    list.Append(2)
    list.Append(3)

    list.Display()
}
```

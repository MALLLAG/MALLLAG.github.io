---
title: Linked List
tags: DataStructure
comments: true
---

# 연결 리스트란 ?

연결 리스트의 노드는 데이터와 링크 공간으로 만들어지고, 연결 리스트를 이루는 작은 단위를 뜻한다. <br>
*(노드란 자료 구조에 데이터를 담거나 표현하는 기초적인 단위를 의미. 특정 값이나 포인터가 될 수 있다.)*

**데이터 영역**은 이름 그대로 값을 저장하며 **포인터 영역**은 자신을 제외한 인접한 노드를 가리킬 때 사용한다. <br>
하나의 노드는 포인터 영역에서 다음 노드를 가리킨다.

<br>
<hr>

# 특징

1. 크기를 미리 정하지 않고도 동적 할당이 가능하다.
2. 삽입과 삭제 연산에서 오버헤드가 배열보다 적다.
3. 특정 인덱스로 접근이 불가능하므로 데이터를 검색하려면 첫 노드부터 끝까지 방문해야 한다.

```
배열의 경우 고정된 크기에서 데이터 중간에 삽입이 이루어지면 배열의 크기를 다시 조정하고 데이터를 옮기는 오버헤드가 발생한다.
하지만 연결 리스트의 삽입은 데이터가 중간에 삽입되어도 노드 간의 포인터만 수정하면 되기 때문에 배열에 비해 유리하다.
```

<br>
<hr>

# 종류

연결 리스트의 종류는 크게 3가지가 있다. <br>

- 포인터 영역을 가지고 다음 노드를 가리키는 **단일 연결 리스트**
- 자신의 앞과 뒤 노드를 가리키기 위해 두 개의 포인터 영역을 가지고 있는 **이중 연결 리스트**
- 마지막 노드가 처음 노드를 가리키고 있는 **원형 연결 리스트**

## 단일 연결 리스트

<img width="506" alt="1" src="https://github.com/MALLLAG/MALLLAG.github.io/assets/87420630/55f13730-e502-49b6-b0ee-877a0f675e5d">

## 이중 연결 리스트

<img width="719" alt="2" src="https://github.com/MALLLAG/MALLLAG.github.io/assets/87420630/f37a9289-f7aa-45b3-bf2a-b799b2b447f2">

## 원형 단일 연결 리스트

<img width="482" alt="3" src="https://github.com/MALLLAG/MALLLAG.github.io/assets/87420630/5775e3ea-ba7c-4bcb-9fdd-e29b9465283c">

<br>
<hr>

# 구현

## 단일 연결 리스트

```kotlin
class Node<T>(
    val data: T,
    var next: Node<T>? = null
)

class SinglyLinkedList<T> {
    private var head: Node<T>? = null

    fun isEmpty(): Boolean {
        return head == null
    }

    fun append(data: T) {
        if (head == null) {
            head = Node(data)
            return
        }

        var pointer = head
        while (pointer?.next != null) {
            pointer = pointer.next
        }

        pointer?.next = Node(data)
    }

    fun delete(data: T) {
        var pointer = head

        if (pointer?.data == data) {
            var removeNode = head
            head = head?.next

            removeNode = null
            return
        }

        var temp = pointer
        while (pointer != null && pointer?.data != data) {
            temp = pointer
            pointer = pointer.next
        }

        if (pointer?.next == null) {
            temp?.next = null
        } else {
            temp?.next = pointer.next
        }
        pointer = null
    }

    fun printAll() {
        var pointer = head

        val builder = StringBuilder()
        while (pointer?.next != null) {
            builder.append(pointer.data)
            builder.append(" -> ")
            pointer = pointer.next
        }

        builder.append(pointer?.data)
        println(builder.toString())
    }
}
```

## 이중 연결 리스트

```kotlin
class Node<T>(
    val data: T,
    var prev: Node<T>? = null,
    var next: Node<T>? = null
)

class DoubleLinkedList<T> {
    private var head: Node<T>? = null

    fun isEmpty(): Boolean {
        return head == null
    }

    fun append(data: T) {
        if (head == null) {
            head = Node(data)
            return
        }

        var pointer = head
        while (pointer?.next != null) {
            pointer = pointer.next
        }

        val newNode = Node(data)
        newNode.prev = pointer
        pointer?.next = newNode
    }

    fun printPrevNode(data: T) {
        if (head == null) {
            println("이중 연결 리스트가 비어 있습니다.")
            return
        }

        if (head?.data == data) {
            println("$data 앞의 노드는 존재하지 않습니다.")
            return
        }

        var pointer = head
        while (pointer != null && pointer.data != data) {
            pointer = pointer.next
        }

        if (pointer == null) {
            println("노드 $data 는 존재하지 않습니다.")
        } else {
            println("노드 $data 의 앞 노드 값은 ${pointer.prev?.data} 입니다")
        }
    }

    fun delete(data: T) {
        var pointer = head

        if (pointer?.data == data) {
            var removeNode = head
            head = head?.next

            removeNode = null
            return
        }

        var prevNode = pointer
        while (pointer != null && pointer.data != data) {
            prevNode = pointer
            pointer = pointer.next
        }

        var temp = pointer?.next
        if (temp == null) {
            prevNode?.next = null
        } else {
            temp.prev = prevNode
            prevNode?.next = pointer?.next
        }

        pointer = null
    }

    fun printAll() {
        var pointer = head

        val builder = StringBuilder()
        while (pointer != null) {
            builder.append(pointer.data)
            builder.append(" <-> ")
            pointer = pointer.next
        }

        builder.delete(builder.lastIndexOf(" <-> "), builder.length)
        println(builder.toString())
    }
}
```

## 원형 단일 연결 리스트

```kotlin
class Node<T>(
    val data: T,
    var next: Node<T>? = null
)

class CircularLinkedList<T> {
    private var head: Node<T>? = null
    private var tail: Node<T>? = null

    fun append(data: T) {
        if (head == null && tail == null) {
            val node = Node(data)
            head = node
            tail = node
            return
        }

        var pointer = tail
        pointer?.next = Node(data)

        tail = pointer?.next
        tail?.next = head
    }

    fun delete(data: T) {
        var pointer = head

        if (pointer?.data == null) {
            var removeNode = head
            head = head?.next

            removeNode = null
            return
        }

        var temp: Node<T>? = null
        while (pointer?.next != tail && pointer?.data != data) {
            temp = pointer
            pointer = pointer?.next
        }

        if (pointer?.next?.data == data) {
            tail = pointer
            tail?.next = head
        } else {
            temp?.next = pointer?.next
        }
        pointer = null
    }

    fun printAll() {
        var pointer = head

        val builder = StringBuilder()
        while (pointer != tail) {
            builder.append(pointer?.data)
            builder.append(" -> ")
            pointer = pointer?.next
        }
        builder.append(pointer?.data)
        builder.append("(tail) -> ")

        builder.append(head?.data)
        builder.append("(head)")

        println(builder.toString())
    }
}
```








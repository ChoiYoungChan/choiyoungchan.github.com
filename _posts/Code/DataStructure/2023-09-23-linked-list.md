---
title:  "[Data Structure] 연결리스트(Linked List)"
excerpt: Linked List

categories:
  - datastructure
tags:
  - [data structure, 연결리스트, Linked List, 링크드리스트]

toc: true
toc_sticky: true
 
date: 2023-09-23
last_modified_at: 2023-09-23
---

## 연결리스트(Linked List)란?
---
연결리스트(Linked List)란? <br>
-> 데이터를 노드(데이터, 포인터)로 구성하여 한줄로 쭉 연결시킨 선형 데이터 구조로 저장하는 자료구조 입니다. <br>
각 노드에는 데이터와 다음 노드를 가리키는 포인터(링크)로 이루어져 있으며, 이중연결리스트, 원형 연결리스트등 여러 종류가 있습니다. <br>
연결리스트를 응용해서 트리 또는 그래프 자료구조를 구현 하는것도 가능하며, 동적 메모리 할당이나 메모리 관리 등 사용하는 부분이 많으니 반드시 익혀야할 기본적인 자료구조입니다. <br>

물론 List<T>, LinkedList<T>는 C#에서 컬렉션으로 제공하고 있습니다.<br>
하지만, 직접 만들어 보는게 많은 도움이 되기 때문에 직접 구현하는 방식으로 예제 코드를 작성, 이후 C#에서 제공하는 LinkedList<T>를 사용하는 것을 보여 드리겠습니다. <br>

## 사용하는 이유(용도)
---
- 동적 메모리 할당. 연결 리스트는 동적으로 데이터를 추가하거나 삭제할 수 있어 메모리를 효율적으로 활용합니다.
- 삽입과 삭제의 효율성. 중간에 데이터를 추가하거나 삭제할 때 배열과 달리 데이터를 이동시킬 필요가 없어 연결 리스트가 유용합니다.
- 메모리 관리. 배열은 크기가 고정되지만 연결 리스트는 동적으로 크기가 조절 가능합니다.



## 문제점&주의사항
---
- 검색 속도: 특정 위치에 직접 접근할 수 없어 검색 작업이 느립니다. 검색에는 순차 접근이 필요합니다
- 메모리 오버헤드: 각 노드는 포인터를 가지고 있어 메모리 사용량이 늘어날 수 있습니다.
- 연결 끊김 문제: 올바르게 노드를 연결하지 않으면 데이터가 손실될 수 있습니다.


### 예제
---
단일 연결리스트(Singly Linked List) <br>
단방향으로 노드들을 연결한 간단한 구조의 연결리스트 입니다.<br>

```C#
using System;
using System.Collections.Generic;

class Node
{
    public int _data;
    public Node _nextNode;

    public Node(int data)
    {
        this._data = data;
        this._nextNode = null;
    }
}

class LinkedListSampleCode
{
    Node _head;

    void Add(int data)
    {
        Node node = new Node(data);
        node._nextNode = _head;
        _head = node;
    }

    void AddAfter(int currentdata, int newdata)
    {
        Node prevnode = null;
        for(Node temp = head; temp != temp._nextNode != null; temp._nextNode)
        {
            if(temp._data == currentdata) prevnode = temp;
            if(prevnode == null)
            {
                Console.WriteLine("{0} data is not in the list");
                return;
            }
        }
        Node node = new Node(newdata);
        node._nextNode = prevnode._nextNode;
        prevnode._nextNode = node;
    }

    void AddLast(int data)
    {
        Node node = new Node(data);
        if(=_head == null)
        {
            _head = node;
            return;
        }
        Node lastNode = GetLastNode();
        lastNode = node;
    }

    void Remove(int removeNode)
    {
        Node temp = _head;
        Node prevnode = null;
        if(temp != null && temp._data == removeNode)
        {
            _head = temp._nextNode;
            return;
        }
        while(temp == null)
        {
            prevnode = temp;
            temp = temp.next;
        }
        prevnode._nextNode = temp._nextNode;
    }

    Node GetNode(int index)
    {
        Node temp = _head;
        for(int count = 0; count < index && temp._nextNode != null; count++)
        {
            temp = temp._nextNode;
        }
        return temp;
    }

    Node GetLastNode()
    {
        Node temp = _head;
        while(temp._nextNode != null) temp = temp._nextNode;

        return temp;
    }
}


```
<br>

이중 연결리스트(Double Linked List) <br>
직전 노드와 다음 노드를 가리키는 포인터를 모두 가지고 있어 양방향으로 탐색이 가능한 연결리스트 입니다. <br>
삽입과 삭제가 효율적이며 순방향&역방향 탐색이 가능하지만, 각 노드가 이전노드와 다음 노드의 참조를 저장하기 때문에 단일 연결리스트 보다 메모리 사용량이 더 많습니다. <br>

```C#
using System;

class Node
{
    public int _data;
    public Node _nextNode;
    public Node _prevNode;

    public Node(int data)
    {
        this._data = data;
        this._prevNode = null;
        this._nextNode = null;
    }
}

class DoubleLinkedListSample
{
    Node _head;
    Node _tail;

    public DoubleLinkedListSample()
    {
        this._head = null;
        this._tail = null;
    }

    public void Add(int data)
    {
        Node node = new Node(data);

        if (this._head == null)
        {
            this._head = node;
            this._tail = node;
        }
        else
        {
            node._prevNode = this._tail;
            this._tail._nextNode = node;
            this._tail = node;
        }
    }

    public void AddFirst(int data)
    {
        Node node = new Node(data);

        node._nextNode = this._head;
        this._head._prevNode = node;
        this._head = node;
    }

    public void Remove(int data)
    {
        Node current = this._head;

        while (current != null)
        {
            if (current._data == data)
            {
                if (current == this._head)
                {
                    this._head = current._nextNode;
                    if (this._head != null)
                    {
                        this._head._prevNode = null;
                    }
                }
                else if (current == this._tail)
                {
                    this._tail = current._prevNode;
                    this._tail._nextNode = null;
                }
                else
                {
                    current._prevNode._nextNode = current._nextNode;
                    current._nextNode._prevNode = current._prevNode;
                }
                break;
            }
            current = current._nextNode;
        }
    }
```
<br>

원형 연결리스트(Circular Linked List) <br>
상기의 이중 연결리스트에서 마지막 노드를 처음 노드에 연결시키는 방식의 연결리스트 입니다. <br>
```C#

```
<br>

C#에서 제공하는 LinkedList<T>를 사용<br>
```C#
using System;

public class Node
{
    public int Data;
    public Node Next;

    public Node(int data)
    {
        Data = data;
        Next = null;
    }
}

public class CircularLinkedList
{
    private Node tail;

    public CircularLinkedList()
    {
        tail = null;
    }

    // 노드 추가
    public void Add(int data)
    {
        Node newNode = new Node(data);

        if (tail == null)
        {
            // 리스트가 비어 있는 경우
            tail = newNode;
            tail.Next = tail; // 자기 자신을 가리킴
        }
        else
        {
            // 기존 노드 뒤에 새 노드를 추가
            newNode.Next = tail.Next;
            tail.Next = newNode;
            tail = newNode;
        }
    }

    // 노드 삭제
    public void Delete(int data)
    {
        if (tail == null)
        {
            Console.WriteLine("리스트가 비어 있습니다.");
            return;
        }

        Node current = tail.Next;
        Node previous = tail;

        do
        {
            if (current.Data == data)
            {
                if (current == tail)
                {
                    // 마지막 노드를 삭제하는 경우
                    if (current.Next == tail)
                    {
                        // 리스트에 노드가 하나뿐인 경우
                        tail = null;
                    }
                    else
                    {
                        previous.Next = current.Next;
                        tail = previous;
                    }
                }
                else
                {
                    previous.Next = current.Next;
                }

                Console.WriteLine($"{data} 삭제됨");
                return;
            }

            previous = current;
            current = current.Next;

        } while (current != tail.Next);

        Console.WriteLine($"{data}를 찾을 수 없습니다.");
    }

    // 리스트 출력
    public void Display()
    {
        if (tail == null)
        {
            Console.WriteLine("리스트가 비어 있습니다.");
            return;
        }

        Node current = tail.Next;
        do
        {
            Console.Write($"{current.Data} -> ");
            current = current.Next;
        } while (current != tail.Next);

        Console.WriteLine("(head)");
    }
}

class Program
{
    static void Main(string[] args)
    {
        CircularLinkedList cll = new CircularLinkedList();

        // 노드 추가
        cll.Add(10);
        cll.Add(20);
        cll.Add(30);
        cll.Display();

        // 노드 삭제
        cll.Delete(20);
        cll.Display();

        cll.Delete(40); // 없는 노드 삭제 시도
        cll.Display();

        // 마지막 노드 삭제
        cll.Delete(10);
        cll.Delete(30);
        cll.Display();
    }
}

```
<br>


<br>
[Top](#){: .btn .btn--primary }{: .align-right}
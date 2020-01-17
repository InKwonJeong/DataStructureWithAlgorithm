# Queue


### 스택의 개념
- 큐(queue)는 컴퓨터의 기본적인 자료 구조의 한가지로, 먼저 집어 넣은 데이터가 먼저 나오는 FIFO (First In First Out)구조로 저장하는 형식을 말한다. 영어 단어 queue는 표를 사러 일렬로 늘어선 사람들로 이루어진 줄을 말하기도 하며, 먼저 줄을 선 사람이 먼저 나갈 수 있는 상황을 연상하면 된다. 나중에 집어 넣은 데이터가 먼저 나오는 스택과는 반대되는 개념이다.

- 덱(deque, "deck"과 발음이 같음 ←double-ended queue)은 양쪽 끝에서 삽입과 삭제가 모두 가능한 자료 구조의 한 형태이다. 두 개의 포인터를 사용하여, 양쪽에서 삭제와 삽입을 발생 시킬 수 있다. 큐와 스택을 합친 형태로 생각할 수 있다.

1. Queue Interface

```java
public interface Queue<T> {
  void enqueue(T newEntry);
  T dequeue();
  T getFront();
  boolean isEmpty();
  void clear();
  int size();

}
```

2. Node를 이용한 Queue 구현.
```java
import java.util.NoSuchElementException;

public class LinkedQueue<T> implements Queue<T> {

    private Node firstNode;
    private Node lastNode;
    private int size;

    public LinkedQueue() {
        firstNode = null;
        lastNode = null;
        size = 0;
    }

    @Override
    public void enqueue(T newEntry) {
        Node newNode = new Node(newEntry, null);
        if(isEmpty())
            firstNode = newNode;
        else
            lastNode.setNextNode(newNode);
        lastNode = newNode;
        size++;
    }

    @Override
    public T dequeue() {
        T front = getFront();
        assert firstNode != null;
        firstNode = firstNode.getNextNode();

        if(firstNode == null)
            lastNode = null;

        size--;
        return front;
    }

    @Override
    public T getFront() {
        if(isEmpty())
            throw new NoSuchElementException();
        else
            return firstNode.getData();
    }

    @Override
    public boolean isEmpty() {
        return firstNode == null && lastNode == null;
    }

    @Override
    public void clear() {
        firstNode = null;
        lastNode = null;
        size = 0;
    }

    @Override
    public int size() {
        return size;
    }

    private class Node {
        private T data;
        private Node next;

        private Node(T dataPortion) {
            this(dataPortion, null);
        }

        private Node(T dataPortion, Node nextNode) {
            data = dataPortion;
            next = nextNode;
        }

        T getData() {
            return data;
        }

        void setData(T newData) {
            data = newData;
        }

        Node getNextNode() {
            return next;
        }

        void setNextNode(Node nextNode) {
            next = nextNode;
        }
    }
}
```

3. Deque Interface

```java
public interface Deque<T> {
    void addToFront(T newEntry);
    T removeFront();
    void addToBack(T newEntry);
    T removeBack();
    T getFront();
    T getBack();
    boolean isEmpty();
    void clear();
    int size();
}
```

4. Node를 이용한 Deque 구현.
```java
import java.util.NoSuchElementException;

public class LinkedDeque<T> implements Deque<T> {

    private Node firstNode;
    private Node lastNode;
    private int size;

    public LinkedDeque() {
        firstNode = null;
        lastNode = null;
        size = 0;
    }

    @Override
    public void addToFront(T newEntry) {
        Node newNode = new Node(newEntry, firstNode, null);
        if(isEmpty())
            lastNode = newNode;
        else
            firstNode.setPreviousNode(newNode);

        firstNode = newNode;
        size++;
    }

    @Override
    public T removeFront() {
        T front = getFront();
        assert firstNode != null;
        firstNode = firstNode.getNextNode();

        if(firstNode == null)
            lastNode = null;
        else
            firstNode.setPreviousNode(null);

        size--;
        return front;
    }

    @Override
    public void addToBack(T newEntry) {
        Node newNode = new Node(newEntry, null, lastNode);
        if(isEmpty())
            firstNode = newNode;
        else
            lastNode.setNextNode(newNode);

        lastNode = newNode;
        size++;
    }

    @Override
    public T removeBack() {
        T back = getBack();
        assert lastNode != null;
        lastNode = lastNode.getPreviousNode();

        if(lastNode == null)
            firstNode = null;
        else
            lastNode.setNextNode(null);

        size--;
        return back;
    }

    @Override
    public T getFront() {
        if(isEmpty())
            throw new NoSuchElementException();
        else
            return firstNode.getData();
    }

    @Override
    public T getBack() {
        if(isEmpty())
            throw new NoSuchElementException();
        else
            return lastNode.getData();
    }

    @Override
    public boolean isEmpty() {
        return firstNode == null && lastNode == null;
    }

    @Override
    public void clear() {
        firstNode = null;
        lastNode = null;
        size = 0;
    }

    @Override
    public int size() {
        return size;
    }

    private class Node {
        private T data;
        private Node next;
        private Node previous;

        private Node(T dataPortion) {
            this(dataPortion, null, null);
        }

        private Node(T dataPortion, Node nextNode, Node previousNode) {
            data = dataPortion;
            next = nextNode;
            previous = previousNode;
        }

        T getData() {
            return data;
        }

        void setData(T newData) {
            data = newData;
        }

        Node getNextNode() {
            return next;
        }

        void setNextNode(Node nextNode) {
            next = nextNode;
        }

        Node getPreviousNode() {
            return previous;
        }

        void setPreviousNode(Node previous) {
            this.previous = previous;
        }
    }
}
```

5. 우선순위 큐

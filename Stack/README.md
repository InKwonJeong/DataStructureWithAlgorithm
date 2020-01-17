# Stack

### 스택의 개념
- 제한적으로 접근할 수 있는 나열 구조이다. 그 접근 방법은 언제나 목록의 끝에서만 일어난다. 끝먼저내기 목록(Pushdown list)이라고도 한다. 스택은 한 쪽 끝에서만 자료를 넣거나 뺄 수 있는 선형 구조(LIFO - Last In First Out)으로 되어 있다. 자료를 넣는 것을 '밀어넣는다' 하여 푸쉬(push)라고 하고 반대로 넣어둔 자료를 꺼내는 것을 팝(pop)이라고 하는데, 이때 꺼내지는 자료는 가장 최근에 푸쉬한 자료부터 나오게 된다. 이처럼 나중에 넣은 값이 먼저 나오는 것을 LIFO 구조라고 한다.

1. Stack Interface

```java
public interface Stack<T> {
    void push(T newEntry);
    T pop();
    T peek();
    int size();
    boolean isEmpty();
    void clear();
}

```

2. Array를 이용한 Stack구현.

```java
import java.util.Arrays;
import java.util.EmptyStackException;

public class ArrayStack<T> implements Stack<T>{

    private T[] stack;
    private int topIndex;
    private boolean initialized = false;
    private int initialCapacity;
    private static final int DEFAULT_INITIAL_CAPACITY = 50;
    private static final int MAX_CAPACITY = 10000;

    public ArrayStack(int initialCapacity) {
        if(initialCapacity < DEFAULT_INITIAL_CAPACITY)
            initialCapacity = DEFAULT_INITIAL_CAPACITY;
        else
            checkCapacity(initialCapacity);
        initializeDataFields(initialCapacity);
    }

    public ArrayStack() {
        this(DEFAULT_INITIAL_CAPACITY);
    }

    @Override
    public void push(T newEntry) {
        checkInitialization();
        ensureCapacity(); // 스택의 크기를 검사하여 내부 Array의 크기를 증가시켜서 overFlow를 방지한다.
        stack[++topIndex] = newEntry;
    }

    @Override
    public T pop() {
        checkInitialization();
        if(isEmpty())
            throw new EmptyStackException();
        else {
            T top = stack[topIndex];
            stack[topIndex--] = null;
            return top;
        }
    }

    @Override
    public T peek() {
        checkInitialization();
        if(isEmpty())
            throw new EmptyStackException();
        else
            return stack[topIndex];
    }

    @Override
    public int size() {
        return topIndex + 1;
    }

    @Override
    public boolean isEmpty() {
        return topIndex < 0;
    }

    @Override
    public void clear() {
        initializeDataFields(initialCapacity);
    }

    private void checkCapacity(int capacity) {
        if(capacity > MAX_CAPACITY)
            throw new IllegalStateException(
                    "Attempt to create a stack whose capacity exceeds allowed maximum of "
                            + MAX_CAPACITY);
    }

    private void initializeDataFields(int initialCapacity) {
        @SuppressWarnings("unchecked")
        T[] tempStack = (T[]) new Object[initialCapacity];
        stack = tempStack;
        topIndex = -1; // index 시작이 0 이라서 topIndex 의 값을 -1로 시작해야된다.
        this.initialCapacity = initialCapacity;
        initialized = true;
    }

    private void ensureCapacity() {
        if(topIndex == stack.length - 1) {
            int newLength = 2 * stack.length;
            checkCapacity(newLength);
            stack = Arrays.copyOf(stack, newLength);
        }
    }

    private void checkInitialization() {
        if(!initialized)
            throw new SecurityException(
                    "ArrayStack object is not initialized properly");
    }

}
```

3. Node를 이용한 Stack 구현.

```java
import java.util.EmptyStackException;

public class LinkedStack<T> implements Stack<T>{
    private Node topNode;
    private int size;


    public LinkedStack() {
        topNode = null;
        size = 0;
    }

    @Override
    public void push(T newEntry) {
        topNode = new Node(newEntry, topNode);
        size++;
    }

    @Override
    public T pop() {
        T top = peek();
        assert topNode != null;
        topNode = topNode.getNextNode();
        size--;
        return top;
    }

    @Override
    public T peek() {
        if(isEmpty())
            throw new EmptyStackException();
        else
            return topNode.getData();
    }

    @Override
    public int size() {
        return size;
    }

    @Override
    public boolean isEmpty() {
        return topNode == null;
    }

    @Override
    public void clear() {
        topNode = null;
        size = 0;
    }

    private class Node{
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

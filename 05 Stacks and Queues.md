> When we are dialing with sequence, number till here, items in sequence, 
> When take answer so far we use stack

### Inbuilt application

#### Stack

```java
Stack<Integer> stack = new Stack<>();  
stack.push(34);  
stack.push(23);  
System.out.println(stack.pop());

Stack (Class)
|
|--- push(E item): Pushes an item onto the top of the stack.
|
|--- pop(): Removes and returns the top element of the stack. Throws EmptyStackException if the stack is empty.
|
|--- peek(): Looks at the top element of the stack without removing it. Throws EmptyStackException if the stack is empty.
|
|--- empty(): Checks if the stack is empty.
|
|--- search(Object o): Determines if an object is on the stack and returns the 1-based position from the top of the stack. Returns -1 if the object isn't on the stack.
|
|--- size(): Returns the number of elements in the stack.
|
|--- contains(Object o): Checks if the stack contains a specified element.
|
|--- iterator(): Returns an iterator for the elements in the stack.
|
|--- toArray(): Converts the stack to an array.
|
|--- clear(): Removes all the elements from the stack.
|
|--- ... (other utility methods inherited from Vector, as Stack extends Vector)


```

#### Queue

```java
Queue<Integer> queue = new LinkedList<>();  
queue.add(3);  
queue.add(4);  
System.out.println(queue.remove());
Queue (Interface)
|
|--- add(E e): Adds an element to the queue. Throws an exception if it fails.
|
|--- offer(E e): Adds an element to the queue. Returns a boolean indicating success/failure.
|
|--- remove(): Removes and returns the element from the front of the queue. Throws an exception if the queue is empty.
|
|--- poll(): Removes and returns the element from the front of the queue. Returns null if the queue is empty.
|
|--- element(): Retrieves but does not remove the element from the front of the queue. Throws an exception if the queue is empty.
|
|--- peek(): Retrieves but does not remove the element from the front of the queue. Returns null if the queue is empty.
|
|--- size(): Returns the number of elements in the queue.
|
|--- isEmpty(): Checks if the queue is empty.
|
|--- contains(Object o): Checks if the queue contains a specified element.
|
|--- iterator(): Returns an iterator for the elements in the queue.
|
|--- toArray(): Converts the queue to an array.
|
|--- clear(): Removes all the elements from the queue.
|
|--- ... (other utility methods)

```

#### Deque

```java
Deque<Integer> deque = new ArrayDeque<>();  
deque.add(32);  
deque.addLast(32);  
deque.removeFirst();
```

### Stack Implementation

```java
package com.kumar;  
  
public class CustomStack {  
    protected int[] data;  
    private static final int DEFAULT_SIZE = 10;  
    int ptr = -1;  
  
    public CustomStack(){  
        this(DEFAULT_SIZE);  
    }  
  
    public CustomStack(int size){  
        this.data = new int[size];  
    }  
  
    public boolean push(int item){  
        if(ifFull()){  
            System.out.println("Stack is Full");  
            return false;  
        }  
        ptr++;  
        data[ptr] = itm;  
        return true;  
    }  
  
    public int pop() throws Exception {  
        if(isEmpty()){  
            throw new Exception("Can pop from empty stack");  
        }  
        return data[ptr--];  
    }  
    public int peek() throws Exception {  
        if(isEmpty()){  
            throw new Exception("Can peek into empty stack");  
        }  
        return data[ptr];  
    }  
  
    private boolean isFull(){  
        return ptr == data.length - 1;  
    }  
  
    private boolean isEmpty(){  
        return ptr==-1;  
    }  
}
```


### Dynamic Stack Implementation

```java
package com.kumar;  
  
public class DynamicStack extends CustomStack{  
    public DynamicStack(){  
        super();  
    }  
    public DynamicStack(int size){  
        super(size);  
    }  
  
  
    @Override  
    public boolean push(int item) {  
        if(this.isFull()){  
            //double the array size  
            int temp[] = new int[data.length * 2];  
  
            //copy all previous items in new Data  
            for(int i=0;i<data.length;i++){  
                temp[i] = data[i];  
            }  
            data = temp;  
        }  
  
        //Insert Item  
        return super.push(item);  
    }  
}
```

### Circular Queue Implementation

```java
package com.kumar;  
  
public class CircularQueue {  
    protected int[] data;  
    private static final int DEFAULT_SIZE = 10;  
    protected int front = 0;  
    protected int end = 0;  
    protected int size = 0;  
  
    public CircularQueue(){  
        this(DEFAULT_SIZE);  
    }  
  
    public CircularQueue(int size){  
        this.data = new int[size];  
    }  
  
    public boolean isFull(){  
        return size == data.length;  
    }  
  
    public boolean isEmpty(){  
        return size == 0;  
    }  
  
    public boolean insert(int item) throws Exception{  
        if(isFull()){  
            return false;  
        }  
        data[end++] = item;  
        end = end % data.length;  
        size++;  
        return true;  
    }  
  
    public int remove() throws Exception{  
        if(isEmpty()){  
            throw new Exception("Queue is Empty");  
        }  
        int removed = data[front++];  
        front = front % data.length;  
        size--;  
        return removed;  
    }  
  
    public int front() throws Exception{  
        if(isEmpty()){  
            throw new Exception("Queue is Empty");  
        }  
        return data[front];  
    }  
  
    public void display(){  
        int tempFront = front;  
        int count = 0;  
        while(count < size){  
            System.out.print(data[tempFront++] + " ");  
            tempFront = tempFront % data.length;  
            count++;  
        }  
    }  
}
```

### Game of two stacks

```java
public class TwoStack {  
    static int twoStacks(int x,int[] a, int[] b){  
        return solve(x,a,b, 0, 0)-1;  
    }  
    private static int solve(int x, int[] a, int[] b, int sum, int count){  
        if(sum>x){
            return count;  
        }  
        if(a.length == 0 || b.length ==0){  
            return count;  
        }
        int ans1 = solve(x, Arrays.copyOfRange(a,1,a.length),b,sum+a[0],count+1);  
        int ans2 = solve(x, a, Arrays.copyOfRange(b,1,b.length),sum+b[0], count+1);  
          
        return Math.max(ans1,ans2);  
    }  
}
```

## Important Tips

1. Separate the algorithms from the worker functions
2. Think about what we are doing before what you doing


### Maximum area of Rectangle in Stack






### Ques) Remove Outermost Parenthesis


```java
class Solution {
    public String removeOuterParentheses(String s) {
        StringBuilder res = new StringBuilder();
        int open = 0;

        for (char ch: s.toCharArray()){
            if(ch == '('){
                open++;
                if(open>1){
                    res.append(ch);
                }
            }
            else{
                if(open>1){
                    res.append(ch);
                }
                open--;
            }
        }
        return res.toString();
    }
}
```


### Ques) Reverse First K elements of Queue

```java
    public Queue<Integer> modifyQueue(Queue<Integer> q, int k) {
        // add code here.
        if(k>q.size() || q.size() == 0 || k<0){
            return q;
        }
        Stack<Integer> stack = new Stack<>();
        for(int i=0; i<k; i++){
            int n = q.poll();
            stack.push(n);
        }
        while(!stack.isEmpty()){
            int n = stack.pop();
            q.offer(n);
        }
        for (int i = 0; i < q.size() - k; i++) {
            q.offer(q.poll());
        }
        return q;
    }
```

### Ques) Delete Middle of stack

```java
    public void deleteMid(Stack<Integer>s,int sizeOfStack){
        // code here
        int mid= sizeOfStack/2;
        
        Stack<Integer> stack = new Stack<>();
        
        while(mid>-1){
            stack.push(s.pop());
            mid--;
        }
        stack.pop();
        while(!stack.isEmpty()){
            s.push(stack.pop());
        }
    }
```


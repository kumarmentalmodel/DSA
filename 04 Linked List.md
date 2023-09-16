```java
package com.kumar;  
  
public class LL {  
    private Node head;  
    private Node tail;
    private int size; 
  
    public LL(){  
        this.size = 0;  
    }  
    private class Node{  
        private int value;  
        private Node next;  
  
        public Node(int value){  
            this.value = value;  
        }  
        public Node(int value, Node next){  
            this.value = value;  
            this.next = next;  
        }  
    }  
    public void insertFirst(int val){  
        Node node = new Node(val);  
        node.next = head;  
        head = node;  
  
        if(tail == null){  
            tail = node;  
        }  
        size += 1;  
    }  
  
    public int deleteFirst(){  
        int val = head.value;  
        head=head.next;  
        if(head==null){  
            tail=null;  
        }  
        size--;  
        return val;  
    }  
    //Insert Recursively  
    public void insertRec(int val, int index){  
        head = insertRec(val, index, head);  
        if (index == size - 1) {  
            while (tail.next != null) {  
                tail = tail.next;  
            }//update tail  
        }  
    }  
    private Node insertRec(int val, int index, Node node){  
        if(index == 0){  
            Node temp = new Node(val, node);  
            size++;  
            return temp;  
        }  
        node.next = insertRec(val, --index, node.next);  
        return node;  
    }  
  
    public void insertLast(int val) {  
        if(tail == null){  
            insertFirst(val);  
            return;  
        }  
        Node node = new Node(val);  
        tail.next = node;  
        tail = node;  
        size++;  
    }  
  
    public Node get(int index){  
        Node node = head;  
        for(int i=0; i<index; i++){  
            node = node.next;  
        }  
        return node;  
    }  
  
    public Node find(int value){  
        Node node = head;  
        for(int i=0; i<size; i++){  
            if(node.value == value){  
                return node;  
            }  
        }  
        return null;  
    }  
  
    public int deleteLast(){  
        if(size <= 1){  
            return deleteFirst();  
        }  
        Node secondlast = get(size-2);  
        int val = tail.value;  
        tail = secondlast;  
        tail.next = null;  
        return val;  
  
    }  
  
    public void insert(int val, int index){  
        if(index == 0){  
            insertFirst(val);  
            return;  
        }  
        if(index >= size){  
            insertLast(val);  
            return;  
        }  
        Node temp = head;  
        for(int i=1;i<index;i++){  
            temp=temp.next;  
        }  
        Node node = new Node(val,temp.next);  
        temp.next = node;  
        size++;  
    }  
  
    public int delete(int index){  
        if(index == 0){  
            return deleteFirst();  
        }  
        if(index == size-1){  
            return deleteLast();  
        }  
        Node prev = get(index-1);  
        int val = prev.next.value;  
        prev.next = prev.next.next;  
        return val;  
    }  
  
    public void display() {  
        Node temp = head;  
        while (temp!=null){  
            System.out.print(temp.value + " -> ");  
            temp = temp.next;  
        }  
        System.out.println("END");  
    }  
    //Remove Duplicates  
    public void duplicates(){  
        Node node = head;  
        while(node.next != null){  
            if( node.value == node.next.value){  
                node.next = node.next.next;  
                size--;  
            }  
            else{  
                node= node.next;  
            }  
        }  
        tail = node;  
        tail.next = null;  
    }  
  
    // Merge two Linked List  
    public static LL merge(Node first, Node second){  
        Node f = first;  
        Node s = second;  
  
        LL ans = new LL();  
        while(f != null && s != null){  
            if(f.value < s.value){  
                ans.insertLast(f.value);  
                f = f.next;  
            }  
            else{  
                ans.insertLast(s.value);  
                s = s.next;  
            }  
        }  
        while (f != null){  
            ans.insertLast(f.value);  
            f = f.next;  
        }  
        while (s != null){  
            ans.insertLast(s.value);  
            s = s.next;  
        }  
        return ans;  
    }  
    
    //Reverse Linked List Recursively  
    private void reverse(Node node){  
        if(node == tail){  
            head = tail;  
            return;  
        }  
        reverse(node.next);  
        tail.next = node;  
        tail = node;  
        tail.next = null;  
    }  
}
```

### Insert Recursively in Linked List

```java 
public void insertRec(int val, int index){  
    head = insertRec(val, index, head);  
}  

private Node insertRec(int val, int index, Node node){  
    if(index == 0){  
        Node temp = new Node(val, node);  
        size++;  
        return temp;  
    }  
    node.next = insertRec(val, index--, node.next);  
    return node;  
}
```

### Doubly Linked List

```java
package com.kumar;  

public class DL {  
    private class Node{  
        int value;  
        Node next;  
        Node prev;  
  
        public Node(int val){  
            this.value = val;  
        }  
  
        public Node(int val, Node next, Node prev){  
            this.value = val;  
            this.next = next;  
            this.prev = prev;  
        }  
    }  
    public DL(){  
        this.size = 0;  
    }  
    private Node head;  
    private Node tail;  
    private int size;  
  
    public void display(){  
        Node node = head;  
        while(node!=null){  
            System.out.print(node.value + "->");  
            node=node.next;  
        }  
        System.out.println("END");  
    }  
    public void reverseDisplay(){  
        Node node = head;  
        Node last = null;  
        while(node!=null){  
            last = node;  
            node=node.next;  
        }  
        while(last != null){  
            System.out.print(last.value + "->");  
            last = last.prev;  
        }  
        System.out.println("END");  
    }  
  
    public void insertFirst(int val){  
        Node node = new Node(val);  
        node.next = head;  
        node.prev = null;  
        if(head != null){  
            head.prev = node;  
        }  
        head = node;  
    }  
  
    public void insertLast(int val){  
        Node temp = new Node(val);  
        if(head == null){  
            head = temp;  
            return;  
        }  
        Node node = head;  
        Node last = null;  
        while(node!=null){  
            last = node;  
            node = node.next;  
        }  
        temp.prev = last;  
        last.next = temp;  
    }  
  
    public void insert(int after, int val){  
        Node p = find(after);  
  
        if(p==null){  
            System.out.println("Node not present");  
            return;  
        }  
  
        Node node = new Node(val);  
        node.next = p.next;  
        p.next = node;  
        node.prev = p;  
        if(node.next != null){  
            node.next.prev = p;  
        }  
  
    }  
  
    public Node find(int val){  
        Node node = head;  
        while(node!=null){  
            if(node.value == val){  
                return node;  
            }  
            node=node.next;  
        }  
        return null;  
    }  
  
    public int deleteFirst(){  
        int val = head.value;  
        if(head.next != null){  
            head.next.prev = null;  
        }  
        head = head.next;  
        return val;  
    }  
    public int deleteLast(){  
        Node node = head;  
        Node last = null;  
        while (node!=null) {  
            last = node;  
            node = node.next;  
        }  
        Node secondLast = last.prev;  
        int val = last.value;  
        secondLast.next = null;  
        return val;  
    }  
    public int delete(int index){  
        Node p = head;  
        for(int i=1; i<index; i++) {  
            p = p.next;  
        }  
        int val = p.next.value;  
        p.next = p.next.next;  
        if(p.next.next != null){  
            p.next.next.prev = p;  
        }  
        return val;  
    }  
}
```

### Circular Linked List

```java
package com.kumar;  
  
public class CLL {  
    private Node head;  
    private Node tail;  
    private int size;  
  
    public CLL(){  
        this.head = null;  
        this.tail = null;  
    }  
    private class Node{  
        Node next;  
        int value;  
        public Node(int value) {  
            this.value = value;  
        }  
    }  
  
    public void insert (int val){  
        Node node = new Node(val);  
        if (head == null) {  
            head = node;  
            tail = node;  
            return;  
        }  
        node.next = head;  
        tail.next = node;  
        tail = node;  
    }  
    public void display(){  
        Node node =head;  
        if(node != null){  
            do{  
                System.out.print(node.value + "->");  
                node = node.next;  
            }while(node != head);  
        }  
        System.out.println("end");  
    }  
    public void delete(int val){  
        Node node = head;  
        if(node == null){  
            return;  
        }  
  
        if(node.value == val){  
            head = node.next;  
            tail.next = head;  
            return;  
        }  
        do{  
        //yaha khade hokar aage wale ki val match kari h
            Node n = node.next;  
            if(n.value == val){  
                node.next = n.next;  
                break;  
            }  
            node = node.next;  
        }while(node != head);  
    }  
}
```

### Q1 Remove Duplicates from Sorted Linked List

```java
public ListNode deleteDuplicates(ListNode head) {  
    if(head == null){  
        return head;  
    }  
    ListNode node = head;  
    while(node.next != null){  
        if( node.val == node.next.val){  
            node.next = node.next.next;  
        }  
        else{  
            node= node.next;  
        }  
    }  
    return head;  
}
```

### Q3 Find head of cycle

```java
```

### Q4 Is Happy Number

```java
class Solution {  
    public boolean isHappy(int n) {  
        int slow = n;  
        int fast = n;  
        do{  
            slow = findSquare(slow);  
            fast = findSquare(findSquare(fast));  
        }while(slow != fast);  
  
        if(slow == 1){  
            return true;  
        }  
        return false;  
    }  
    private int findSquare(int n){  
        int ans =0;  
        while(n>0){  
            int rem =  (n%10);  
            ans += rem*rem;  
            n = n/10;  
        }  
        return ans;  
    }  
}

```

### Reverse a Linked List Iteratively

```java
//reverse a linked list iteratively  
public void reverseIter(){  
    Node prev = null;  
    Node pres = head;  
    Node next = null;  
    if(head.next!=null){  
        next = head.next;  
    }  
    while(pres!=null){  
        pres.next = prev;  
        prev = pres;  
        pres = next;  
        if(next != null){  
            next = next.next;  
        }  
    }  
    head = prev;  
}
```

### Q6 Reverse Part of Linked List

```java
public ListNode reverseBetween(ListNode head, int left, int right) {  
    if(left == right){  
        return head;  
    }  
    ListNode prev = null;  
    ListNode current = head;  
    for(int i=0; current!=null && i<left-1; i++){  
        prev = current;  
        current = current.next;  
    }  
  
    ListNode last = prev;  
    ListNode newEnd = current;  
  
    ListNode next = current.next;  
    for(int i=0; current !=null && i< right -left +1;i++){  
        current.next = prev;  
        prev = current;  
        current = next;  
        if(next!=null){  
            next = next.next;  
        }  
    }  
    if(last!=null){  
        last.next = prev;  
    }else{  
        head = prev;  
    }  
    newEnd.next = current;  
    return head;  
}
```

### Q7 Check Palindrome in Linked List

```java
public boolean isPalindrome(ListNode head) {  
    ListNode mid = middleNode(head);  
    ListNode headSecond = reverseList(mid);  
    ListNode rereverseNode = headSecond;  
  
    while(head!=null && headSecond!=null){  
        if(head.val != headSecond.val){  
            break;  
        }  
        head = head.next;  
        headSecond = headSecond.next;  
    }  
  
    reverseList(rereverseNode);  
  
    return head==null || headSecond == null;  
}
```

### Q8 Reorder list

```java
public void reorderList(ListNode head) {  
    if(head == null || head.next == null) return;  
  
    ListNode middleNode = middleNode(head);  
    ListNode hs = reverseList(middleNode);  
  
    //rearrange  
    ListNode hf = head;  

    while(hf!=null && hs!=null){  
        ListNode temp = hf.next;  
        hf.next = hs;  
        hf = temp;  

        temp = hs.next;  
        hs.next = hf;  
        hs = temp;  
    }  
    if(hf!=null){  
        hf.next = null;  
    }  
    head = hf;  
}
```
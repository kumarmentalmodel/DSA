Rules -> 
1. Make subproblems
2. Make input smaller 


###  Q1 Power Set

![[WhatsApp Image 2023-09-07 at 1.29.32 PM.jpeg]]

Method 1

```java
import java.util.Stack;  
  
public class Main {  
    public static void solve(String ip, String op){  
        if(ip.length() == 0){  
            System.out.println(op);  
            return;  
        }  
        String op2 = op + ip.charAt(0);  
        //remove first character of input string  
        ip = ip.substring(1);  
          
        solve(ip,op);  
        solve(ip,op2);  
    }  
  
    public static void main(String[] args) {  
        solve("abc","");  
    }  
}
```

Method 2

```java
import java.util.Stack;  
  
public class Main {  
    public static void solve(String ip,int index, String curr){  
        if(index == ip.length()){  
            System.out.println(curr);  
            return ;  
        }  
        solve(ip,index+1,curr+ip.charAt(index));  
        solve(ip,index+1,curr);  
    }  
  
    public static void main(String[] args) {  
        solve("abchg",0,"");  
    }  
}
```

### Q2 Lucky numbers


```java
import java.util.Stack;  
  
public class Main {  
    public static boolean solve(int n,int index){  
        if(n%index == 0){  
            return false;  
        }  
        if(index > n){  
            return true;  
        }  
        return solve(n - n/index,index+1);  
    }  
  
    public static void main(String[] args) {  
        System.out.println(solve(13,2));  
    }  
}

```


### Q3 Reverse a Number

method 1
```java
    public static int reverse(int n, int ans){  
        if(n==0){  
            return ans;  
        }  
        return reverse(n/10, ans*10 + n%10);  
    }
```

method 2
```java
    static int reverse(int n){  
        int base = (int)(Math.log10(n) + 1);  
        return helper(n,base);  
    }  
    static int helper(int n, int base){  
        if(n==0)  
            return 0;  
        return (n%10)*(int)Math.pow(10,base-1) + helper(n/10,base-1);  
    }
```

![[WhatsApp Image 2023-09-07 at 6.17.13 PM.jpeg]]

### Q4 Fibonacci

```java
public class Fibonacci {
	static int fibonacci(int n) {
		if(n<2) {
			return n;
		}
		return fibonacci(n-1) + fibonacci(n-2);
	}
	public static void main(String[] args) {
		for(int i=0; i<8; i++) {
			System.out.print(fibonacci(i) + " ");
		}
	}
}
```

### Q5 Linear Search 

Solve using a recursion, We have to return the ArrayList.

```java
public class practice {
	static ArrayList<Integer> search(int[] arr, int index, int target) {
		ArrayList<Integer> list = new ArrayList<>();
		if(index == arr.length -1)
			return list;
		if(arr[index] == target) 
			list.add(index);
		ArrayList<Integer> ansFromBelow = search(arr, index+1, target);
		list.addAll(ansFromBelow);
		return list;
	}
	
	public static void main(String[] args) {
		int[] arr = {4,52,3,5,634,34,5,3};
		System.out.println(search(arr,0,344));
	}
}
```

### Q6 Rotated Binary Search

```java
class Solution
{
    int search(int A[], int l, int h, int key)
    {
        // l: The starting index
        // h: The ending index, you have to search the key in this range
        // Complete this function
        int mid = (l+h)/2;
        if(A[mid] == key){
            return mid;
        }
        if(l>=h){
            return -1;
        }
        if(A[l]<=A[mid]){
            if(key>=A[l] && key<A[mid]){
                return search(A,l,mid-1,key);
            }
            else{
                return search(A,mid+1,h,key);
            }
        }
        else{
            if(key>A[mid] && key<=A[h]){
                return search(A,mid+1,h,key);
            }
            else{
                return search(A,l,mid-1,key);
            }
        }
    }
}
```

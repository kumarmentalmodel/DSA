### Q1 Number of zeroes in sorted binary array


```java
	int arr = [1,1,0,0,0,0,0,0,0];
    int search(int arr[], int start, int end){
        int middle = start + (end-start)/2;
        if(middle == 0 && arr[middle] == 0){
            return 0;
        }
        if(arr[middle] == 1){
            if(arr[middle+1] == 0)
                return middle+1;
            else{
                return search(arr,middle,end);
            }
        }
        else{
            if(arr[middle-1] == 1){
                return middle;
            }
            else{
                return search(arr,start,middle);
            }
        }
    }
    
    int countZeroes(int[] arr, int n) {
        // code here
        return n - search(arr,0,n-1);
    }
```
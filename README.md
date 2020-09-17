# Sorting hands-on

### Bubble Sort
* Main points in bubble sort
  - run outer loop from `0` to `n-1`
  - run inner loop from `1` to `n-i` OR `0` to `n-i-1`
  - Even the Best case complexity is O(n2)
  - Sorting is stable
  - Bubble sort is comparatively slower
```
import java.util.*;

public class Sorting {
  
  public static void swap(int arr[],int i,int j){
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
  }
  
  public static void bubbleSort(int arr[],int n){
    for(int i=0;i<n-1;i++){
      for(int j=1;j<n-i;j++){
        if(arr[j]<arr[j-1]){
          swap(arr,j,j-1);
        }
      }
    }
  }
}
```
* Optimized version of bubble sort, by adding a flag check if swap was happened in the iteration or not.
  - In this best case is O(N)
```
import java.util.*;

public class Sorting {
  
  public static void swap(int arr[],int i,int j){
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
  }
  
  public static void bubbleSortOptimized(int arr[],int n){
    for(int i=0;i<n-1;i++){
      boolean noSwap = true;
      for(int j=1;j<n-i;j++){
        if(arr[j]<arr[j-1]){
          noSwap = false;
          swap(arr,j,j-1);
        }
      }
      if(noSwap){
        break;
      }
    }
  }
}
```

### Insertion Sort
* Main points in insertion sort
  - Set a marker for the sorted section, after the furst element. Therefore, run outer loop from `1` to `n`
  - run inner loop from `i-1` to `0` and with additional check that the current inner loop element is greater than current outer loop element.
  - Best suited algorithm for small length arrays.
  - Best case complexity is O(N)
  - It is stable sort
  - Number of swaps reduced than bubble sort
```
import java.util.*;

public class Sorting {
  
  public static void swap(int arr[],int i,int j){
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
  }
  
  public static void insertionSort(int arr[],int n){
    for(int i=1;i<n;i++){
      int key = arr[i];  // first element of unsorted array
      int j = i-1; // last index of sorted array
      while(j>=0 && arr[j]>key){
        swap(arr,j,j+1);
        j--; // go till the index where arr[j] is less than key
      }
      // j is the key where value is less than the key, so it needs to be inserted at j+1.
      arr[j+1] = key;
    }
  }
}
```

### Selection sort
* Best case complexity for selection sort is O(n2)
* unstable
```
import java.util.*;

public class Sorting {
  
  public static void swap(int arr[],int i,int j){
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
  }
  
  public static void selectionSort(int arr[],int n){
    for(int i=0;i<n;i++){
      int min_index = i;
      for(int j=i+1;j<n;j++){
        if(arr[j]<arr[min_index]){
          min_index = j;
        }
      }
      swap(arr,i,min_index);
    }
  }
}
```

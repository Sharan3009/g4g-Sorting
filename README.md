# Sorting hands-on

### Bubble Sort
* Main points in bubble sort
  - run outer loop from `0` to `n-1`
  - run inner loop from `1` to `n-i` OR `0` to `n-i-1`
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

### Insertion Sort
* Main points in insertion sort
  - Set a marker for the sorted section, after the furst element. Therefore, run outer loop from `1` to `n`
  - run inner loop from `i-1` to `0` and with additional check that the current inner loop element is greater than current outer loop element.
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

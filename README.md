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

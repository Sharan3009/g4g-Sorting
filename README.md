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

### Selection Sort
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

### Merge Sort
* This takes O(n) auxillary space.
```
import java.util.*;

public class Sorting {
  
  public static void mergeSort(int arr[],int l,int r){
    if(l<r){
      int mid = l + (r-l)/2;
      mergeSort(arr,l,mid);
      mergeSort(arr,mid+1,r);
      merge(arr,l,mid,r);
    }
  }
  
  public static void merge(int arr[],int l, int m, int r){
    int n1 = m-l+1;
    int n2 = r-m;
    int left[] = new int[n1];
    int right[] = new int[n2];
    
    for(int i=0;i<n1;i++){
      left[i] = arr[l+i];
    }
    
    for(int i=0;i<n2;i++){
      right[i] = arr[m+1+i];
    }
    
    int i=0;
    int j=0;
    int k = l;
    while(i<n1 && j<n2){
      if(left[i]<=right[j]){
        arr[k++] = left[i++];
      } else {
        arr[k++] = right[j++];
      }
    }
    while(i<n1){
      arr[k++] = left[i++];
    }
    while(j<n2){
      arr[k++] = right[j++];
    }
  }
}
```
* This takes O(1) auxillary space
* Precaution: multiplication may lead to memory overflow and will lead to unexpected result of big numbers.
```
import java.util.*;

public class Sorting{
  
  public static void mergeSort(int arr[],int n){
    int max = Integer.MIN_VALUE;
    for(int i=0;i<n;i++){
      if(arr[i]>max){
        max = arr[i] + 1;
      }
    }
    mergeSortRec(arr,0,n-1,max);
  }
  
  public static void mergeSortRec(int arr[],int l,int r, int maxEle){
    if(l<r){
        int mid = l + (r-l)/2;
        mergeSortRec(arr,l,mid,maxEle);
        mergeSortRec(arr,mid+1,r,maxEle);
        mergeO1(arr,l,mid,r,maxEle);
    }
  }
  
  public static void mergeO1(int arr[],int l, int m, int r, int maxEle){
    int i = l;
    int j = m+1;
    int k = l;
    while(i<=m && j<=r){
      if(arr[i]%maxEle<=arr[j]%maxEle){
        arr[k]+= (arr[i++]%maxEle)*maxEle;
      } else {
        arr[k]+= (arr[j++]%maxEle)*maxEle;
      }
      k++;
    }
    while(i<=m){
      arr[k]+= (arr[i++]%maxEle)*maxEle;
      k++;
    }
    while(j<=r){
      arr[k]+= (arr[j++]%maxEle)*maxEle;
      k++;
    }
    
    for(int index=l;index<=r;index++){
      arr[index]/=maxEle;
    }
  }
}
```

### Quick Sort
* Quick sort using **Lomuto** partition
* unstable
```
import java.util.*;

public class Sorting{

  public static void swap(int arr[],int i, int j){
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
  }

  public static void quickSortLomuto(int arr[],int l, int r){
    if(l<r){
      int p = lomutoPartition(arr,l,r);
      quickSortLomuto(arr,l,p-1);
      quickSortLomuto(arr,p+1,r);
    }
  }
  
  public static int lomutoPartition(int arr[],int l, int r){
    int pivot = arr[r];
    int i = l-1;
    for(int j=l;j<=r-1;j++){
      if(arr[j]<=pivot){
        i++;
        swap(arr,i,j);
      }
    }
    swap(arr,i+1,r);
    return i+1;
  }
}
```

* Quick sort using **Hoare** partition
* unstable
* Much better than Lomuto partition
```
import java.util.*;

public class Sorting{

  public static void swap(int arr[],int i, int j){
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
  }
  public static void quickSortHoare(int arr[],int l, int r){
    if(l<r){
      int p = hoarePartition(arr,l,r);
      quickSortHoare(arr,l,p);
      quickSortHoare(arr,p+1,r);
    }
  }
  
  public static int hoarePartition(int arr[],int l, int r){
    int pivot = arr[l];
    int i = l-1;
    int j = r+1;
    while(true){
      do{
        i++;
      }while(arr[i]<pivot);
      do{
        j--;
      }while(arr[j]>pivot);
      if(i>=j) return j;
      swap(arr,i,j);
    }
  }
}
```

* Quick sort using **Naive** partition
* stable
* needs O(n) auxillary space for sorting
```
import java.util.*;

public class Sorting{

  public static void quickSortNaive(int arr[],int l, int r){
    if(l<r){
      int p = naivePartition(arr,l,r);
      quickSortNaive(arr,l,p-1);
      quickSortNaive(arr,p+1,r);
    }
  }
  
  public static int naivePartition(int arr[],int l, int r){
    int index = -1;
    int temp[] = new int[r-l+1];
    int pivot = arr[r];
    for(int i=l;i<=r;i++){
      if(arr[i]<=pivot){
        temp[++index] = arr[i];
      }
    }
    int returnIndex = l + index;
    for(int i=l;i<=r;i++){
      if(arr[i]>pivot){
        temp[++index] = arr[i];
      }
    }
    for(int i=l;i<=r;i++){
      arr[i]=temp[i-l];
    }
    return returnIndex;
  }
}
```

### Cycle Sort
* O(n2)
* Minimum number of memory writes
```
import java.util.*;

public class Sorting{

  public static int replace(int arr[],int index, int num){
      int temp = arr[index];
      arr[index] = num;
      return temp;
   }
   
  public static void cycleSort(int arr[],int n){
    for(int cs=0;cs<n-1;cs++){
      int pos = cs;
      int temp = arr[pos];
      for(int i=cs+1;i<n;i++){
        if(arr[i]<temp){
          pos++;
        }
      }
      temp = replace(arr,pos,temp);
      while(pos!=cs){
        // this is repeated piece of code
        pos = cs;
        for(int i=cs+1;i<n;i++){
          if(arr[i]<temp){
            pos++;
          }
        }
        temp = replace(arr,pos,temp);
      }
    }
  }
}
```

### Counting Sort
* O(n+k) both time and space complexity
* Stable sort
* Not a comparison based method
```
import java.util.*;

public class Sorting{

  public static void countingSort(int arr[],int n,int k){
    int count[] = new int[k];
    for(int i=0;i<k;i++){
      count[i] = 0;
    }
    for(int i=0;i<n;i++){
      count[arr[i]]++;
    }
  
    for(int i=1;i<k;i++){
      count[i]+=count[i-1];
    }
    int output[] = new int[n];
    // You can also sorting by running the loop from 0 to n-1, but running loop in reverse makes it stable sort
    for(int i=n-1;i>=0;i--){
      output[--count[arr[i]]] = arr[i];
    }
    for(int i=0;i<n;i++){
      arr[i] = output[i];
    }
  }
}
```

### Radix Sort
* Time complexity = O(d*(n+b)) where d=number of digits in max number & b=base of logarithmic
* Space complexity= O(n+b);
* by increasing b, d gets smaller i.e timecomplexity reduces but auxillary space increases.
* It's for positive numbers only
```
import java.util.*;

public class Sorting{

  public static void radixSort(int arr[],int n){
    int max = arr[0];
    for(int i=1;i<n;i++){
      if(arr[i]>max){
        max = arr[i];
      }
    }
    for(int exp = 1;max/exp>0;exp*=10){
      countingSort(arr,n,exp);
    }
  }
  
  public static void countingSort(int arr[],int n, int exp){
    int b = 10;
    int count[] = new int[b];
    for(int i=0;i<b;i++){
      count[i] = 0;
    }
    for(int i=0;i<n;i++){
      count[(arr[i]/exp)%10]++;
    }
    for(int i=1;i<b;i++){
      count[i]+=count[i-1];
    }
    int output[] = new int[n];
    for(int i=n-1;i>=0;i--){
      output[--count[(arr[i]/exp)%10]] = arr[i];
    }
    for(int i=0;i<n;i++){
      arr[i] = output[i];
    }
  }
}
```

### Bucket Sort
* O(n)
* For uniformily distributed positive numbers only
```
import java.util.*;

public class Sorting{

  public static void bucketSort(int arr[],int n,int k){
    int max = 0;
    for(int i=0;i<n;i++){
      if(arr[i]>max){
        max = arr[i];
      }
    }
    max++;
    
    ArrayList<ArrayList<Integer>> bkt = new ArrayList<>();
    for(int i=0;i<k;i++){
        bkt.add(new ArrayList<Integer>());
    }
    for(int i=0;i<n;i++){
      int bi = (k*arr[i])/max;
      bkt.get(bi).add(arr[i]);
    }
    
    for(int i=0;i<k;i++){
      Collections.sort(bkt.get(i));
    }
    
    int index = 0;
    for(int i=0;i<k;i++){
      for(int j=0;j<bkt.get(i).size();j++){
        arr[index++] = bkt.get(i).get(j);
      }
    }
  }
}
```

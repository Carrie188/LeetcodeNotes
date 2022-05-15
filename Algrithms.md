# Recursion

1. Recursion Example: Factorial of a number 

   ```java
   public static int factorial(int n){
     if(n != 0){
       return n * factotial(n-1); // recursive call
     }else{
       return 1;
     }
       
   }
   ```

   

# Sorting Algrithmns

## Insertion sort

- Time complexity:  Best = O(n)  Averdage = O(n^2)  Worst = O(n^2)

- Space complexity: O(1)

- Stability: yes

- Implementation:

  ```java
  // dividing the array into the sorted and unsorted subarrays.
  // assume the fist sorted part is the first element of the array
  // expanding and placing the new element into its proper place within the sorted subarray.
  public static void insertionSort(int[] array){
    for(int i = 1; i < array.length; i++){
      int current = array[i];
      int j = i - 1;
      while(j >= 0 && current < array[j]){
        array[j+1] = arry[j];
        j--;
      }
      // at this point means that j is either -1 or where current >= array[j]
      // so we don't need to swap the current position from j+1 to j
      array[j+1] = current;
    }
    
  }
  
  ```

  

## Bubble sort

- Time complexity:  Best = O(n)  Averdage = O(n^2)  Worst = O(n^2)

- Space complexity: O(1)

- Stability: yes

- Implementation:

  ```java
  // compare two adjacent elements and swap the positions if the condition occurs
  public static void bubbleSort(int[] array){
    //loop to access each element in the array
    for(int i = 0; i < array.length; i++){
      //loop to compare othe elements
      for(int j = 0; j < array.length - 1; j++){
        if(array[j] > array[j+1]){
          //swapping
          int temp = array[j+1];
          array[j+1] = array[j];
          array[j] = temp;
          
        }
      }
    }
  }
  ```

  

## Selection sort

- Time complexity:  Best = O(n^2)  Averdage = O(n^2)  Worst = O(n^2)

- Space complexity: O(1)

- Stability: 

- Implementaion

  ```java
  // assume that the first element is the minimum and iterate through the rest to see if there's a smaller element and then swap
  public static void selectionSort(int[] array){
    for(int i = 0; i < array.length; i++){
      int minValue = array[i];
      int minIndex = i;
      for(int j = i + 1; j < array.length; i++){
        if(array[j] < minValue){
          mainValue = array[j];
          minIndex = j; 
        }
      }
      // find the smallest element from the unsorted part 
      //and swap it with the first element of each iteration
      int temp = array[i];
      array[i] = array[minIndex];
      array[minIndex] = temp;
      
    }
  }
  ```

  

## Merge sort 

- Time complexity:  Best = O(nlog(n))  Averdage = O(nlog(n))  Worst = O(nlog(n)) 

- Space complexity: O(n)

- Stability: yes

- Implementation:

  ```java
  public class TestMain {
      public static void main(String[] args) {
          int[] array = {8,4,2,1,9,7};
          mergeSort(array,0,5);
          for (int a : array ) {
              System.out.println(a);
          }
  
      }
    // Divide and Conquer algorithm
    public static void mergeSort(int[] array, int left, int right){
      if(right <= left) return;
      int mid = (left + right) / 2;
      mergeSort(array, left, mid);
      mergeSort(array, mid+1, right);
      merge(array,left,mid,right);
    }
  
    public static void merge(int[] array, int left, int mid, int right){
      // calculate the legth of two subarrays
      int leftLength = mid - left + 1;
      int rightLength = right - mid;
      // create two temporary subarrays
      int[] leftArray = new int [leftLength];
      int[] rightArray = new int [rightLength];
      // copy the two sorted array into the two temporories
      for(int i = 0; i < leftLength; i++){
        leftArray[i] = array[left+i];
      }
      for(int i = 0; i < rightLength; i++){
        rightArray[i] = array[mid+1+i];
      }
  
      // set the curent index of temp subarrays
      int leftIndex = 0;
      int rightIndex = 0;
  
      // coping from leftArray and rightArray back into array by comparing
      for(int i = left; i < right +1; i++){
        if(leftIndex < leftLength && rightIndex < rightLength){
          if(leftArray[leftIndex] < rightArray[rightIndex]){
            array[i] = leftArray[leftIndex];
            leftIndex++;
          }else{
            array[i] = rightArray[rightIndex];
            rightIndex++;
          }
        }else if(leftIndex < leftLength){
          // comes here means all elements of the rightArray have been copied into the array
          // then just need to copy the rest of the leftArray into the array
          array[i] = leftArray[leftIndex];
          leftIndex++;
        }else if(rightIndex < rightLength){
          // comes here means all elements of the leftArray have been copied into the array
          // then just need to copy the rest of the rightArray into the array
          array[i] = rightArray[rightIndex];
          rightIndex++;
        }
  
      }
  
  
    }
  }
  ```

  

## Quick sort

- Time complexity:  Best = O(nlog(n))  Averdage = O(nlog(n))  Worst = O(n^2)

- Space complexity: O(nlog(n))

- Stability: no

- Implementation

  ```java
  public class TestMain {
      public static void main(String[] args) {
          int[] array = {8,4,2,1,9,7};
          quickSort(array,0,5);
          for (int a : array ) {
              System.out.println(a);
          }
  
      }
    // Divide and Conquer algorithm
    public static void quickSort(int[] array, int begin, int end){
      if(end <= begin) return;
      int pivot = partition(array,begin,end);
      quickSort(array, begin, pivot-1);
      quickSort(array, pivot+1, end);
    }
    public static int partition(int[] array, int begin, int end){
      // pick an element as the pivot from array
      // sometimes the time complexity depends on choosing a good pivot
      int pivot = end;
      int counter = begin;
      // find elements smaller than pivot element and swap the position of the counter value 			//and the smaller value	
      for(int i = begin; i < end +1; i++){
        if(array[i] < array[pivot]){
          int temp = array[counter];
          array[counter] = array[i];
          array[i] = temp;
          counter++;
        }
      }
       // after finishing swaping the smaller elments to left, swap the position of pivot element with the last compared element(the current counter)
      int temp = array[counter];
      array[counter] = array[pivot];
      array[pivot] = temp;
      return counter;
    }
  }
  ```

  

## Heap sort

- Time complexity:  Best = O(nlog(n))  Averdage = O(nlog(n))  Worst = O(nlog(n))

- Space complexity: O(1)

- Stability: no

- Implementation

  ```java
  public static void heapSort(int[] array){
    int length = array.length;
    if(length == 0) return;
    //heapify the array to make a max-heap
    //we're going from the first non-leaf to the root
    for(int i = length / 2 -1; i >= 0; i--){
      heapify(array, length, i);
    }
    //after heapify the array, swaping the root[0] element to the end
    for(int i = length -1; i >= 0; i--){
      int temp = array[i];
      array[i] = array[0];
      array[0] = temp;
      // heapify the root element again after swap
      heapify(array, i, 0);
    }
  }
  // heapify 
  public static void heapify(int[] array, int length, int currentIndex){
    //find the largest element among the currentIndex(root), leftChild and rightChild
    int leftChildIndex = currentIndex * 2 + 1;
    int rightChildIndex = currentIndex * 2 + 2;
    int largestIndex = currentIndex;
    if(leftChildIndex < length && array[leftChildIndex] > array[currentIndex]){
      largestIndex = leftChildIndex;
    }
    if(rightChildIndex < length && array[rightChildIndex] > array[currentIndex]){
      largestIndex = rightChildIndex;
    }
    //swap and continue heapify if the largest one is not the currentIndex(root)
    if(largestIndex != currentIndex){
      int temp = array[currentIndex];
      array[currentIndex] = array[largestIndex];
      array[largestIndex] = temp;
      //continue comparing until put the currentIndex(root) at the right place
      heapify(array, length, largestIndex); 
    }
    
    
  }
  ```

  

# Search Algrithms

## Linear Search

- linear = simple (there is nothing clever but searching one by one)

- Implementation

  ```java
  public static int linearSearch(int array[], int targetValue) {
      for (int index = 0; index < array.length; index++) {
          if (arr[index] == targetValue)
              return index;
      }
      return -1;
  }
  ```

  

## Binary Search

Search a **sorted array** by repeatedly dividing the search interval in half.

1. **Recursive** Implementation

   ```java
   // recursive method
   public static int binarySearch(int[] array, int targetValue, int firstIndex, int lastIndex){
     //
     if(lastIndex >= firstIndex){
       int midIndex = (lastIndex - firstIndex) / 2 + firstIndex;
       // if find the target value at the midIndex, then return the midIndex
       if(array[midIndex] == targetValue){
         return midIndex;
       }
       if(array[midIndex] > targetValue){
         return binarySearch(array, targetValue, firstIndex, midIndex - 1);
       }
       if(array[midIndex] < targetValue){
         return binarySearch(array, targetValue, midIndex + 1, lastIndex);
       }
       // return -1 when the target value is not found in the array
       return -1;
     }
     
     
   }
   ```

   

2. **Iterative** Implementation

   ```java
   // iteritive method
   public static int binarySearch(int[] array, int targetValue){
     int firstIndex = 0;
     int lastIndex = array.length - 1;
     while(firstIndex <= lastIndex){
       int midIndex = (lastIndex - firstIndex) / 2 + firstIndex;
       if(array[midIndex] = targetValue){
         return midIndex;
       }
       if(array[midIndex] > targetValue){
         lastIndex = midIndex - 1;
       }
       if(array[midIndex] < targetValue){
         firstIndex = midIndex + 1;
       }
     }
     //return -1 if the target value was not found
     return -1;
   }
   ```

   

## Depth First Search (DFS) - Graph

The purpose of the algorithm is to mark each vertex as visited while avoiding cycles.

A standard DFS implementation puts each vertex of the graph into one of two categories:

1. Visited list
2. Not Visited stack

- Implementation (Recursive)

  ```java
  import java.util.*;
  class Graph{
    
  }
  ```

  

## Breadth First Search (BFS) - Graph



## String pattern matching



# Two Pointers Technique 

## ( Array, ArrayList, LinkedList, String ) 

1. **Opposite-directional:**

   ```java
   //two pointer technique (Opposite-directional)
   // based on a sorted array 
   public static int[] twoSum(int[] nums, int target){
     int start = 0;
     int end = nums.length -1;
     int result = new int[2];
     while(start < end){
       int sum = nums[start] + nums[end];
       if(sum < target){
        	start++;
       }else if(sum > target){
         end--;
       }else{
         result[0] = nums[start];
         result[1] = nums[end];
         break;
       }
     }
     return result;
   }
   ```

   ```java
   //two pointer technique (Opposite-directional)
   // based on a sorted array with some negative numbers [-4, -3, 0, 2, 3]
   public static int[] sortArrayAfterSquared(int[] nums){
     int right = 0;
     int left = 0;
     int index = 0;
     while(right < nums.length && nums[right] < 0){
       right++;
       left = right - 1;
     }
     while(left >= 0 && right < nums.length){
       if(Math.pow(2, nums[left]) < Math.pow(2, nums[right])){
         nums[index++] = Math.pow(2, nums[left]);
         left--;
       }else{
         nums[index++] = Math.pow(2, nums[right]);
         right++;
       }
     }
     while(left >= 0){
       nums[index++] = Math.pow(2, nums[left]);
       left--;
     }
     while(right < nums.length){
       nums[index++] = Math.pow(2, nums[right]);
       right++;
     }
     return nums;
   }
   ```

   

2. **Equi-directional:**

   ```java
   //two pointer technique (Equi-directional) - sliding window with a window length K
   // based on a sorted array
   public static int getMaxSumSubArrayOfSizeK(int[] nums, int k){
     int windowSum = 0;
     int maxSum = 0;
     int windowStart = 0;
     int windowEnd = 0;
     while(windowEnd < k){
       windowSum += nums[windowEnd++];
     }
     maxSum = windowSum;
     while(windowEnd < nums.length){
       windowSum += nums[windowEnd++] - nums[windowStart++];
       maxSum = Math.max(maxSum, windowSum);
     }
     return maxSum;
   }
   
   ```

   ```java
   //two pointer technique (Equi-directional) - sliding window -Dynamic K
   // find the size of the smalledst contigous subarray with a sum >= target
   
   public static int getSmallestContigousSizeOfSum(int[] nums, int target){
           int minSize = nums.length;
           int start = 0;
           int end = 0;
           int currentSum = 0;
   
           while(end < nums.length){
   
               currentSum += nums[end];
             // check if the current sum >= target, if not, continue adding values
               while(currentSum >= target){
                   int currentSize = end - start +1;
                   minSize = Math.min(minSize, currentSize);
                   currentSum -= nums[start];
                   start++;
               }
               end++;
           }
           return minSize;
       }
   
   ```

   3. Three pointers

   ```java
   publc int[] threeSum(int[] array, int target){
     int[] result = new result[3];
     if(array.length < 3) return result;
     
     
     
   }
   ```



# Dynamic programming








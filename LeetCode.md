## LeetCode Questions:

#### 167. Two Sum II - Input array is sorted

#### Level:  Easy

```java
//using two pointers approach  

class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int[] result = new int[2];
        int left = 0;
        int right = numbers.length -1;
        if( numbers == null || numbers.length < 2) return result;
        while(left < right){
            if(numbers[left] + numbers[right] > target){
                right--;
            }else if(numbers[left] + numbers[right] < target){
                left++;
            }else{
                result[0] = left;
                result[1] = right;
                return result;
            }
        }
        
        return result;
        
    }
}
```

#### 345. Reverse Vowels of a String

```java
class Solution {
    public String reverseVowels(String s) {
        if(s == null && s.length() == 0) return s;
      	String vowels = "aeiouAEIOU";
      	char[] chars = s.toCharArray(); // convert s to an array
        int left = 0;
        int right = chars.length - 1;
        while(left < right){
            if(vowels.contains(chars[left]+"") && vowels.contains(chars[right]+"")){
                char temp = chars[left];
                chars[left] = chars[right];
                chars[right] = temp;
                left++;
                right--;
                
            }else if(vowels.contains(chars[left]+"")){
                right--;
            }else if(vowels.contains(chars[right]+"")){
                left++;
            }else{
                left++;
                right--;
            }
        }
        
        return new String(chars); //convert an array to string using one of String constructor
        
        
    }
}
```



#### 633. Sum of Square Numbers

```java
class Solution {
    public boolean judgeSquareSum(int c) {
        int left = 0;
        long right = (long) Math.sqrt(c);
        while(left <= right){
            long powSum = left * left + right * right;
            if(powSum == c){
                return true;
            }else if(powSum < c){
                left++;
            }else{
                right--;
            }
        }
        
        return false;
    }
}
```



#### 680. Valid Palindrome II

```java
class Solution {
    public boolean validPalindrome(String s) {
        int left = 0;
        int right = s.length() - 1;
        while(left < right){
            if(s.charAt(left) != s.charAt(right)){
                return isPalindrome(s,left+1, right) || isPalindrome(s, left, right-1);
            }
            left++;
            right--;
        }
        return true;
    }
    
    public boolean isPalindrome(String s, int i, int j ){
        while(i < j){
            if(s.charAt(i) != s.charAt(j)){
                return false;
            }
            i++;
            j--;
        }
        return true;
    }
}
```



#### 88. Merge Sorted Array 

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        // sorted fromm rear/end to start so that the unsorted value will not be overrided before comparing 
        int index1 = m-1;
        int index2 = n-1;
        int k = m + n -1;
        while(index1 >= 0 && index2 >= 0){
            
            if(nums1[index1] > nums2[index2]){
                nums1[k] = nums1[index1];
                index1--;
            }else{
                nums1[k] = nums2[index2];
                index2--;
            }
            
            k--;
            
        }
        // if index1 >= 0 left, then we don't need do anything cause it's already sorted
        // if index2 >= 0 left, then 
        while(index2 >= 0){
            nums1[k] = nums2[index2];
            index2--;
            k--; 
        }
        
        
        
    }
}
```



#### 1. Two Sum - Input array is unsorted

```java
// using hashmap 
// iterate/go though the array only once
//	Time Complecity = O(n)

class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        Map<Integer, Integer> countMap = new HashMap<Integer, Integer>();
        for(int i =0; i< nums.length; i++){
            if(countMap.containsKey(target - nums[i])){
                result[1] = i;
                result[0] = countMap.get(target - nums[i]);
                return result;
            }
            countMap.put(nums[i], i);
        }
        return result;
    }
}
```


## [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

### Hints: HashSet,  two pointers

 ```java
 class Solution {
     public int lengthOfLongestSubstring(String s) {
        
         int i = 0, j = 0, max = 0;
         Set<Character> set = new HashSet<>();
         
         while(i < s.length()){
             
             if(!set.contains(s.charAt(i))){
                 set.add(s.charAt(i));
                 max = Math.max(max, set.size());
                 i++;
             }else{
                 set.remove(s.charAt(j));
                 j++;
             }
             
         }
         return max;
 
      
     }
 }
 ```



## [28. Implement strStr()](https://leetcode.com/problems/implement-strstr/)

Given two strings `needle` and `haystack`, return the index of the first occurrence of `needle` in `haystack`, or `-1` if `needle` is not part of `haystack`.

```java
// using substring()
// runtime: 325 ms.  memory: 42.6 MB
class Solution {
    public int strStr(String haystack, String needle) {
        int m = haystack.length();
        int n = needle.length();
        if(n ==0 || n > m){
            return -1;
        }
        if(m == 0){
            return 0;
        }
        
        for(int i = 0; i < m - n +1; i++){
            
            if(haystack.substring(i, i+n).equals(needle)){
                return i;
            }
        }
        
        return -1;
        
    }
}
```



## [14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/description/)

```java
// using indexOf(), substring()
// note: for array, strs.length.  for String, str.length()
// runtime: 0 ms.  memory: 41 MB
public String longestCommonPrefix(String[] strs) {
  if(strs.length() == 0 || strs[0].isEmpty){
    return 0;
  }
  int pre = strs[0];
  
  for(int i = 1; i < strs.length(); i++){
    // set strs[0] as a first prefix and if not match then decrease the length of th prefix 
    while(strs[i].indexof(pre) != 0){
      pre = pre.substring(0, pre.length() - 1);
    }
  }
  return pre;
}
```



## [58. Length of Last Word](https://leetcode.com/problems/length-of-last-word/description/)

```java

// approach 1. using String methods: trim(), split()
// runtime: 2 ms.  memory: 41.7 MB
class Solution {
    public int lengthOfLastWord(String s) {
      String[] strs = s.trim().split(" ");
      if(strs.length == 0){
        return 0;
      }else{
        return strs[strs.length - 1].length();
      }
      	
      
    }
}

// approach 2:
class Solution {
    public int lengthOfLastWord(String s) {
       int lastLength = 0;
      int i = s.length() - 1;
      if(s.length() == 0) return 0;
      while(i >= 0){
          
         if(s.charAt(i)==' ' && lastLength != 0){
            break;
         }
          
        if(s.charAt(i) != ' '){
          lastLength++;
         
        }
        i--;
      }
        return lastLength;
    }
}

// approach 3:
// using loop to check ' '
// note: char is ' ', String is " "
// runtime: 0 ms.  memory: 40.1 MB
class Solution {
     public int lengthOfLastWord(String s) {
       int lastLength = 0;
      int i = s.length() - 1;
      if(s.length() == 0) return 0;
      while(s.charAt(i) == ' '){
        i--;
      }
      while(i >= 0){
        if(s.charAt(i) != ' '){
          lastLength++;
          i--;
        }else{
             break;
        }
       
      }
        return lastLength;
    }
}
```



## [387. First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/description/)

```java

// first try: wrong answer
class Solution {
    public int firstUniqChar(String s) {
        int m = s.length();
        if(m == 0) return -1;
        if(m == 1) return 0;
        
        
        for(int i = 0; i < s.length(); i++){
            boolean d = true;
            int j = i + 1;
            int k = i -1;
           while(j < s.length()){
                if(s.charAt(i) == s.charAt(j)){
                    d = false;
                }
                j++;
            }
            
            while ( k >=0 ){
                if(s.charAt(i) == s.charAt(k)){
                    d = false;
                }
                k--;
            }
            
            if(d == true){
                return i;
            }
           
        }
        
        return -1;
    }
}





// note: HashMap
// runtime: 30 ms.  memory: 48.1 MB
class Solution {
    public int firstUniqChar(String s) {
        int m = s.length();
        if(m == 0) return -1;
        if(m == 1) return 0;
        
        HashMap<Character, Integer> list = new HashMap<>();
        
        for(int i = 0; i < s.length(); i++){
            if(!list.containsKey(s.charAt(i))){
                list.put(s.charAt(i), i);
            }else{
                list.put(s.charAt(i), -1);
            }
        }
        int min = Integer.MAX_VALUE;
        for(Integer c : list.values()){
            if(c != -1){
                min = Math.min(min, c);
            }
        }
        
        return min == Integer.MAX_VALUE ? -1 : min;
    }
}
```



## [383. Ransom Note](https://leetcode.com/problems/ransom-note/)

Given two strings `ransomNote` and `magazine`, return `true` *if* `ransomNote` *can be constructed from* `magazine` *and* `false` *otherwise*.

### ???

```java
// there is a line of the solution that I can not understand
// runtime: 6 ms.  memory: 46.7 MB
if(ransomNote == null || ransomNote.isEmpty()) 
    return true;

if(magazine == null || magazine.isEmpty())
    return false;
    
Map<Character, Integer> charCount = new HashMap();

for(char c : ransomNote.toCharArray()) {
    charCount.put(c, charCount.getOrDefault(c, 0) + 1);
}

for(char c : magazine.toCharArray()) {
    if(charCount.containsKey(c)) {
        int previousCnt = charCount.put(c, charCount.get(c) - 1);
        
      // ??? what is the use of checking previousCnt - 1 == 0
        if(previousCnt - 1 == 0) {s
            charCount.remove(c);
            
            if(charCount.size() == 0) 
                return true;
        }
    }
}
return false;


// toCharArray()
// runtime: 2 ms.  memory: 46.1 MB
public boolean canConstruct(String ransomNote, String magazine) {
       int[] list = new int[26]; // totally 26 letters
        if(ransomNote.length() > magazine.length()) return false; // corner case
        
        for(Character c : ransomNote.toCharArray()){
            list[c - 'a']++;
        }
        
        int remaining = ransomNote.length();
        for(Character s : magazine.toCharArray()){
            if(list[s - 'a'] > 0){
                list[s - 'a']--;
                remaining--;
            }
            if(remaining == 0){
                return true; // quick end if we have finished all characters in ransomNote
            }
        }
        return remaining == 0;
    }
```



## [344. Reverse String](https://leetcode.com/problems/reverse-string/description/)

```java
public void reverseString(char[] s) {
        
        for(int i = 0; i < s.length/2; i++){
            char temp = s[i];
            s[i] = s[s.length - i - 1];
            s[s.length - i - 1] = temp;
            
        }
    }
```



## [151. Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/description/)



```java
// my solution
// runtime: 22 ms.  memory: 54 MB
public String reverseWords(String s) {
        String[] list = s.split(" ");
        for(int i = 0; i < list.length/2; i++){
            String temp = list[i];
            list[i] = list[list.length - i - 1];
            list[list.length - i - 1] = temp;
        }
        
       String newStr = "";
        for(String c : list){
            if(c != ""){
                newStr += c +" ";
            }
            
        }
        
        return newStr.trim();
    }
```



## 

## [345. Reverse Vowels of a String](https://leetcode.com/problems/reverse-vowels-of-a-string/description/) 

```java
class Solution {
    
    public String reverseVowels(String s) {
      // create a hashser for vowels characters
       HashSet<Character> vowels = new HashSet<>(
           Arrays.asList('a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U')); 
        if (s == null) return null;
        int i = 0;
        int j = s.length() - 1;
        char[] result = new char[s.length()];
        while (i <= j) {
            char ci = s.charAt(i);
            char cj = s.charAt(j);
            if (!vowels.contains(ci)) {
                result[i++] = ci;
            } else if (!vowels.contains(cj)) {
                result[j--] = cj;
            } else {
                result[i++] = cj;
                result[j--] = ci;
            }
        }
        return new String(result);

    }
}
```





## [205. Isomorphic Strings](https://leetcode.com/problems/isomorphic-strings/) (Strings have the same format)



```java
public boolean isIsomorphic(String s, String t) {
  // think about corner case first
        if(s == null && t == null) return true;
        if(s == null || t == null) return false;
        if(s.length() != t.length()) return false;
  // ASCII + extend ASCII == (0->127) + (128->255)
  // A->Z: 65->90.  a->z: 97->122
        int[] sIndexArray = new int[256];
        int[] tIndexArray = new int[256];
        Arrays.fill(sIndexArray,-1);
       Arrays.fill(tIndexArray,-1);
        for(int i = 0;i< s.length();i++){
            if(sIndexArray[s.charAt(i)] != tIndexArray[t.charAt(i)]) return false;
        //E.g. s = "aa", t = "bc";
        //When i = 0, s.charAt(i) = 'a', then sIndexArray['a'] = -1; t.charAt(i) = 'b', then tIndexArray['b'] = -1. O.K.
        //When i = 1, s.charAt(i) = 'a', then sIndexArray['a'] = 0; t.charAt(i) = 'c', then tIndexArray['c'] = -1.
        //So, s = a(-1)a(0), and t = b(-1)c(-1). Then return false;
       // Another example can be s = abbcc = a(-1)b(-1)b(1)c(-1)c(3), t = effgg = e(-1)f(-1)f(1)g(-1)g(3);
            sIndexArray[s.charAt(i)] = tIndexArray[t.charAt(i)] = i;
        }
        return true;
    }
```



## [290. Word Pattern](https://leetcode.com/problems/word-pattern/) (match the givens pattern)



```java
 public boolean wordPattern(String pattern, String s) {
        String[] s1 = s.split(" ");
        char[] p1 = pattern.toCharArray();
        if(p1.length != s1.length) return false;
        
        HashMap<Character, String> map = new HashMap<>();
        
        for(int i = 0; i < pattern.length(); i++){
            if(!map.containsKey(p1[i])){
              //key and value should be both unique
                if(map.containsValue(s1[i])) return false;
                map.put(p1[i], s1[i]);
                
            }else{
                
                if(!map.get(p1[i]).equals(s1[i])) return false;
            }
        }
        return true;
    }
```





## [316. Remove Duplicate Letters](https://leetcode.com/problems/remove-duplicate-letters/)



```java
String removeDuplicateLetters(String s) {
    Stack<Character> stk = new Stack<>();

    // 维护一个计数器记录字符串中字符的数量
    // 因为输入为 ASCII 字符，大小 256 够用了, 也可以用26 c - 'a'
    int[] count = new int[256];
    for (int i = 0; i < s.length(); i++) {
        count[s.charAt(i)]++;
    }

    boolean[] inStack = new boolean[256];
    for (char c : s.toCharArray()) {
        // 每遍历过一个字符，都将对应的计数减一
        count[c]--;

        if (inStack[c]) continue;

        while (!stk.isEmpty() && stk.peek() > c) {
            // 若之后不存在栈顶元素了，则停止 pop
            if (count[stk.peek()] == 0) {
                break;
            }
            // 若之后还有，则可以 pop
            inStack[stk.pop()] = false;
        }
        stk.push(c);
        inStack[c] = true;
    }

    StringBuilder sb = new StringBuilder();
    while (!stk.empty()) {
        sb.append(stk.pop());
    }
    return sb.reverse().toString();
}



```


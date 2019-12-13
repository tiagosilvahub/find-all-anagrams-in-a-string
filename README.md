# find-all-anagrams-in-a-string
Given a string s and a non-empty string p, find all the start indices of p's anagrams in s.

https://leetcode.com/problems/find-all-anagrams-in-a-string/

Strings consists of lowercase English letters only and the length of both strings s and p will not be larger than 20,100.

The order of output does not matter.

Example 1:
```
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]
```

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".

Example 2:
```
Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]
```
Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".

```
public List<Integer> findAnagrams(String s, String p) {
  List<Integer> indexes = new LinkedList<>();
  int[] charCounts = new int[256];
  char[] sChars = s.toCharArray();
  char[] pChars = p.toCharArray();

  int left = 0;
  int right = 0;
  int uniqueCharCount = 0;

  if(pChars.length < 1 || pChars.length > sChars.length){
      return indexes;
  }

  for( char c : pChars) {
      if(charCounts[c] == 0){
          uniqueCharCount++;
      }
      charCounts[c]++;
  }

  while(right < s.length()) {
      char rightChar = sChars[right];
      charCounts[rightChar]--;
      if (charCounts[rightChar] == 0) {
          uniqueCharCount--;
      }
      while(uniqueCharCount == 0){
          char leftChar = sChars[left];
          if( right-left == pChars.length -1 ){
              indexes.add(left);
          }
          charCounts[leftChar]++;
          if( charCounts[leftChar] > 0 ){
              uniqueCharCount++;
          }
          left++;
      }
      right++;
  }
  return indexes;
}
```

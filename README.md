# Implement strStr
## https://leetcode.com/problems/implement-strstr

Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Clarification:

What should we return when needle is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when needle is an empty string. This is consistent to C's strstr() and Java's indexOf().

``` 
Example 1:

Input: haystack = "hello", needle = "ll"
Output: 2

Example 2:

Input: haystack = "aaaaa", needle = "bba"
Output: -1

Example 3:

Input: haystack = "", needle = ""
Output: 0
``` 

## Constraints:
```
1. 0 <= haystack.length, needle.length <= 5 * 104
2. haystack and needle consist of only lower-case English characters.
```

# Implementation 1 : KMP Algorithm
```java

class Solution {
    public int strStr(String t, String p) {
        int n = t.length();
        int m = p.length();
        if (m == 0) return 0;

        int[] pi = computePrefix(p);

        int k = -1;
        for (int i = 0; i < n; i++) {
            while (k >= 0 && p.charAt(k + 1) != t.charAt(i)) {
                k = pi[k];
            }

            if (p.charAt(k + 1) == t.charAt(i)) {
                k++;
            }

            if (k == m - 1) {
                return i - m + 1;
            }
        }

        return -1;
    }

    private int[] computePrefix(String p) {
        int m = p.length();
        int[] pi = new int[m];
        pi[0] = -1;
        int k = -1;
    
        for (int i = 1; i < m; i++) {
            while (k >= 0 && p.charAt(k + 1) != p.charAt(i)) {
                k = pi[k];
            }

            if (p.charAt(k + 1) == p.charAt(i)) {
                k++;
            }

            pi[i] = k;
        }
        return pi;
    }
}
         
```

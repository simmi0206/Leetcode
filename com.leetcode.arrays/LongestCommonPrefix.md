# Intuition (Brute-Force)
The common prefix among all strings will always be a prefix of the lexicographically smallest string and also a prefix of the lexicographically largest string.
Therefore, instead of comparing all strings, we can just compare the first and last string after sorting.

# Approach
Sort the array of strings in lexicographical order.

Take the first string (a) and the last string (b) after sorting.

Compare characters of a and b one by one until they differ.

The common prefix up to that point is the answer.

If no characters match, return "".

# Complexity
- Time complexity:
Sorting takes O(n log n) where n is the number of strings.

Comparing first and last string takes at most O(m), where m is the length of the shortest string.

Overall: O(n log n + m)

- Space complexity:
Sorting may use extra space depending on the sort implementation, but typically O(1) additional space (ignoring input storage).


# Code
```java []
class Solution {
    public String longestCommonPrefix(String[] strs) {
        Arrays.sort(strs);
        String a = strs[0];
        String b = strs[strs.length - 1];
        int index = 0;

        while (index < a.length()) {
            if (a.charAt(index) == b.charAt(index)) {
                index++;
            } else {
                break;
            }
        }

        return index == 0 ? "" : a.substring(0, index);
    }
}
```

# Intuition (Optimized)
The longest common prefix of all strings must also be a prefix of the first string.
If we compare this prefix with the rest of the strings and keep shrinking it until all strings share it, we will end up with the correct longest common prefix.

# Approach
Start by assuming the first string (strs[0]) is the prefix.
Iterate over the rest of the strings one by one.
For each string, check if it starts with the current prefix.
If not, shrink the prefix by removing the last character (prefix.substring(0, prefix.length() - 1)).

Repeat until the string starts with prefix or prefix becomes empty.
If prefix becomes empty at any point, return "" (no common prefix).
After checking all strings, return the final prefix.

# Complexity
- Time complexity:
In the worst case, we may shrink the prefix for each string character by character.

Total work across all strings is O(S), where S is the total number of characters in all strings.

- Space complexity:
We only use a few variables and modify the prefix in place.

O(1) extra space (ignoring input).


# Code
```java []
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs.length == 0 || strs == null) {
            return "";
        }
        String prefix = strs[0];
        for (int i = 1; i < strs.length; i++) {
            while (!strs[i].startsWith(prefix)) {
                prefix = prefix.substring(0, prefix.length() - 1);
            }
            if (prefix.length() == 0) {
                return "";
            }
        }
        return prefix;
    }
}
```


Store the frequency of target string into map.

Store as the length of target string as "RequiredCount"

If you find the character in the given string which is there in the target string then  reduce the frequency of hashmap by 1 and also reduce the RequiredCount variable. 

If you did not find the character in the given string then add this character into the map by reducing the frequency by 1 which would become -1.

Once the required count is zero "0" then start shrinking the window by increasing the ith pointer. 

In case of ith pointer, we will be doing opposite like If you come across any character then put this into hashmap by increasing the frequency as 1 and if frequency of character in the hashmap is greater than 0 then increase the required count.  

Remember as the requiredcount is greater then zero hence window should again be expanding. Hence, this shrinking code loop will not work. 

Also when the requiredcount is equal to zero then check the minimumWindowSize and if it is greater than the current window size (j-i+1) then   update it to current window size. 

```
package somepackage.twopointerslidingwindow;

import java.util.HashMap;
import java.util.Map;

public class MinimumWindowSubstringWithSameCharcterAsTarget {

    public String check(String s, String t) {
        int n = s.length();
        if (t.length() > n) {
            return "";
        }
        int windowSize = Integer.MAX_VALUE;
        int startI=0;
        HashMap<Character, Integer> hm = new HashMap<>();
        for (Character c : t.toCharArray()) {
                hm.put(c, hm.getOrDefault(c,0) + 1);
        }

        int requiredCount = t.length();
        int i = 0;
        int j = 0;

        while (j < n) {
            char ch = s.charAt(j);
            if (hm.getOrDefault(ch,0) > 0 && hm.containsKey(ch)) {
                requiredCount--;
            }
            hm.put(ch, hm.getOrDefault(ch,0) - 1);
            while (requiredCount == 0) {
                // start shrinking
                int currentWindowSize = j - i + 1;
                if (windowSize > currentWindowSize) {
                    windowSize = currentWindowSize;
                    startI=i;
                }
                hm.put(s.charAt(i), hm.getOrDefault(s.charAt(i),0) + 1);
                if (hm.get(s.charAt(i)) > 0) {
                    requiredCount++;
                }
                i++;
            }
            j++;
        }
    return windowSize==Integer.MAX_VALUE?"" :s.substring(startI, startI+ windowSize);
    }

    public String minWindow(String s, String t) {
        int n = s.length();

        if (t.length() > n)
            return "";

        Map<Character, Integer> mp = new HashMap<>();

        // store karliya
        for (char ch : t.toCharArray())
            mp.put(ch, mp.getOrDefault(ch, 0) + 1);

        int requiredCount = t.length();
        int i = 0, j = 0;

        int minWindowSize = Integer.MAX_VALUE;
        int start_i = 0;

        // story starts
        while (j < n) {
            char ch = s.charAt(j);

            if (mp.containsKey(ch) && mp.get(ch) > 0)
                requiredCount--;

            mp.put(ch, mp.getOrDefault(ch, 0) - 1);

            while (requiredCount == 0) {
                // start shrinking the window

                int currWindowSize = j - i + 1;

                if (minWindowSize > currWindowSize) {
                    minWindowSize = currWindowSize;
                    start_i = i;
                }

                char startChar = s.charAt(i);
                mp.put(startChar, mp.getOrDefault(startChar, 0) + 1);

                if (mp.containsKey(startChar) && mp.get(startChar) > 0) {
                    requiredCount++;
                }

                i++;
            }

            j++;
        }

        return minWindowSize == Integer.MAX_VALUE ? "" : s.substring(start_i, start_i + minWindowSize);
    }

    public static void main(String[] args) {
        String check = new MinimumWindowSubstringWithSameCharcterAsTarget().check("ACXDBLKWBCWAB", "ABC");
        System.out.println(check);
    }
}

```

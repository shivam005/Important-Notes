We need to find the length of the longest substring without repeating character. It means that whenever we come across any repeating character, we will have to stop there and to manage the count upto it.
1. Create a linkedhashmap, iterate upto the last of the array and add each character with the present index i as the value. Provided, the map does not contain the character as the key.
2. Otherwise fetch the value of repeated character and assign it to the i. This way we will be again starting from the last repeated character.
3. Check if the size of the map is greater then maxLength variable then update the maxlength as size of the map and keymap as substring. 
```
package somepackage.practice;

import java.util.LinkedHashMap;

public class LengthOfLongestSubstringWithoutRepeatingCharacter {
    public int check1(String str){
        char[] chars = str.toCharArray();
        int n =str.length();
        int i=0; int maxLength=0;
        String longestSubstring ="";
        LinkedHashMap<Character, Integer> map = new LinkedHashMap<>();
        while (i<n) {
            if (!map.containsKey(chars[i])) {
                map.put(chars[i], i);
            } else {
                i = map.get(chars[i]);
                map.clear();
            }

            if(map.size()>maxLength){
                maxLength=map.size();
                longestSubstring=map.keySet().toString();
            }
            i++;
        }
        System.out.println(longestSubstring);
        return maxLength;
    }


    public static void main(String[] args) {
    String s = "pwwkefew";
        int i = new LengthOfLongestSubstringWithoutRepeatingCharacter().check1(s);
        System.out.println(i);
    }
}
```

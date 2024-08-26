### Reverse the string
For a string with more than one character, reverse the substring that excludes the first character and then append the first character to the end of the reversed substring.
If there is only one character in the string or it is empty then we can return the same string. 
```
    public  String rev(String string ){
        if(string.length() <= 1  ){
            return string;
        }
        return rev(string.substring(1))+string.charAt(0);
    }
```

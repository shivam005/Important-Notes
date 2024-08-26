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
### Find factorial
For values of n greater than 1, the function calls itself twice: once with n-1 and once with n-2.
This continues until the base cases are reached. Each recursive call further breaks down the problem until it reaches the base cases.
As we know, factorial of 1 or less than 1 is always 1, hence we keep on multiplying the given number with the n-1.
```
    public int fact(int n){
        if(n<=1){
            return 1;
        }
        return n*fact(n-1);
    }

```
### Find nth fibonacci 

```
    public  int find(int n){
        if(n==1 ){
            return 1;
        }  if (n==0) {
            return 0;
        }
        return find(n-1)+find(n-2);
    }
```

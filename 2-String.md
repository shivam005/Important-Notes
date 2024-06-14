|ASCII Value| Description|
|---|---|
|32 to 126| Printable characters, including digits, uppercase and lowercase letters, punctuation, and special symbols|
|32 to 47|space ! " # $ % & ' ( ) * + , - . /|
|48 to 57 |0123456789|
|58 to 64|  :;<=>?@|
|65 to 90| A to Z|
|91 to 96 |[\	]^_`|
|97 to 122|a to z|
|123 to 126 |{}~ |

##  Integer to Roman {Store Value in Array and refer it while traversing}
Herein, we will be checking the divisibling by integer values and will assign the corresponding string in the result string. 
At last using modulus operator will be discarding the digit for which symbol has been assigned. 
```
public String execute(Integer n){
        int[] in={1,4,5,9,10,40,50,90,100,400,500,900, 1000};
        String[] str={"I","IV","V","IX","X","XL","L","XC","C","CD","D","CM","M"};
        String result = "";
        for(int i=in.length-1;i>=0;i--){
            if(n==0){
                break;
            }
            int times = n/in[i];
            while(times>0){
                result+=str[i];
                times--;
            }
           n=n%in[i];
        }

        return result;
    }
```
## Remove the pair of character wherein both upper & lower case char are in consecutive order {Use hashset to refer values using the contains method of set}
Herein, using stack we will be checking if the present element in stack has difference of 
32 with the current element and if It is found that we pop the stack and skip the insertion of the current element 
and go back to the new upcoming element. 
```
 public String check(String str){
       Stack<Character> stack = new Stack<>();
       for(Character ch : str.toCharArray()){
           if(!stack.isEmpty()){
        if(stack.peek()+32==ch || stack.peek()-32==ch ){
            stack.pop();
        }else {
            stack.push(ch);
        }}else{
               stack.push(ch);
           }
       }
       String string="";
        while(!stack.isEmpty()){
            string+=stack.peek();
        }

        return string;

   }

```
## Count and Say { Use recursion and the use logic to return the soltion}
In this program, we will look back to the previous solution and will say, how much time a number has appeared.
Finally, we will write the "count"+"the present number".
In this program, the important part is in processing wherein we are using recursion followed by 
checking the count of any value by the previously derived result of method, at last we print the count followed by the digit.

```
1 -> 1
2 -> 11 (one 1)
3 -> 21 (two 1s)
4 -> 1211 (one 2, then one 1)
5 -> 111221 (one 1, one 2, then two 1s)
6 -> 312211 (three 1s, two 2s, then one 1)

 public String check(int n){
        if(n==1){
            return "1";
        }
        String say=check(n-1);
        char[] chars = say.toCharArray();
        String result ="";
        for(int i=0;i<say.length();i++){
            char ch=chars[i];
            int count=1;
            while(i<say.length() -1&& chars[i]==chars[i+1]){
                count++;
                i++;
            }
            result=result+count+ch;
        }
        return result;
    }
```
##  Check whether the Two String are Close
 Here, we just need to return the boolean result hence, there are some point which would be certain
  As only two operation are allowed either to swap a character or to transform the character
  1. both the string should have same length of string
  2. sum of frequency of the character should be same as if it will not be true then transformation will also not work.
  3. Character at a particular index should be same in both the array.
```
 public boolean check(String str1, String str2){
        if(str2.length()!=str1.length()){
            return false;
        }

        int[] array=new int[26];
        int[] array1= new int[26];

        for(int i=0; i<str1.length();i++){
             char a ='a';
             int index=str1.charAt(i)-a;
             array[index]=array[index]+1;
            int index1=str2.charAt(i)-a;
            array1[index1]=array1[index1]+1;
        }

        for(int i=0; i<26;i++){
            if(array1[i]==0 && array[i]==0){
                continue;
            }if(array1[i]!=0 && array[i]!=0){
                continue;
            }
            return false;
        }

        Arrays.sort(array); Arrays.sort(array1);
        return Arrays.equals(array1, array) ; // Here == will not work as it will check for reference
        // array with same content would be there in the different location.
    }

```

## Detect Capital Letter
We have given three condition to check 1. Whether all letters are in upper case 2. All letter are in lower case 3. First letter of string is in upper case only. Herein, we will be checking If the character in the string is greater than 'z' and lesser than 'a' then it is lower case. If the character in the string is greater than 'Z' and smaller than 'A' then it is not upper case. For checking the last condition, we will be passing the substring of the given string which would be starting from 1. 
```
 public static boolean isSmall(String string){

        char[] chars = string.toCharArray();
        for(int i=0; i<chars.length;i++){
            if(chars[i]< 'a' || chars[i]>'z'){
                return false;
            }
        }
        return true;
    }

    public static boolean isCapital(String string){

        char[] chars = string.toCharArray();
        for(int i=0; i<chars.length;i++){
            if(chars[i]<'A' || chars[i]>'Z'){
                return  false;
            }
        }
        return true;
    }


    public boolean check(String string){

    if(isSmall(string)){
        return true;
    }
    if(isCapital(string)){
        return true;
    }
    String s= string.substring(1);
        if(isSmall(s)){
            return true;
        }

      return false;
    }
```

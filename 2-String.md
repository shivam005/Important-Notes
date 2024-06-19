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
### All Possible Subsequence of String
We can use recursive technique to get it done. All possible subsequence means that we need to deal with all posible combinations
hence, we will call our method twice recursively wherein in the first instance we will not be including the character at the given index
and in the second instance, we will be including the character at the given index. In this way, we will end up considering all possible
subsequences. 
```
static ArrayList<String> al= new ArrayList<>();
public void check(String str, String ans){
        if(str.length()==0){
            al.add(ans);
            return;
        }
// This base case is intended to check If the length of the string has become 0 then add all possible combination into arraylist.
        check(str.substring(1),ans);
      //Here we are excluding the the character
        check(str.substring(1),ans+str.charAt(0));
      // Here we are including the character
        return;
    }
```
```
   public ArrayList<String> execute(String str){
        ArrayList<String> al= new ArrayList<>();
        check(str,"",al);
        return al;
    }
 public void check(String str, String ans, ArrayList<String> al){
        if(str.length()==0){
            al.add(ans);
            return;
        }
        check(str.substring(1),ans, al);
        check(str.substring(1),ans+str.charAt(0), al);
        return;
    }
```
### All Possible Subsequence of String using Dynamic Programming
Here,  after computing each result or answer we will be keep on storing it into a array. Once It has been computed for the given string 
then we will get it stored into the hashmap corresponding to the key which will have combination of given string and answer. 
Further whenever a call will be made to calculate the all possible combination for the given pair of string and answer then we can first
look into the hashmap and if it is there then we can add the combination into the arraylist and can call the return method which would
basically stop the execution for the current flow.
```
 static ArrayList<String> al= new ArrayList<>();
 static HashMap<String, ArrayList<String>> hm= new HashMap<>();
  public   void check(String str, String ans){
        if(str.length()==0){
            al.add(ans);
            return;
        }
        ArrayList<String> currentResult = new ArrayList<>();
        String key = str + "|" + ans;
        if(hm.containsKey(key)){
            al.addAll(hm.get(key));
            return;
        }
        check(str.substring(1),ans);
        currentResult.add(ans);

        check(str.substring(1),ans+str.charAt(0));
        currentResult.add(ans+str.charAt(0));

        hm.put(key,currentResult);

    }

```
### Remove special character from string
This problem can be effectively handled by using ASCII values. Ascii value for capital letters are in between 65 to 90, and small letter is in between 97 to 122 and value of space is 32. Hence, we can put simple check as below.
```
      String[] split = str.split("");
      String str1="";
      for(int i=0;i<split.length;i++){
      if(split[i].charAt(0)==32){
        str1=str1+split[i];
        continue;
      }
        if(split[i].charAt(0)>=65 && split[i].charAt(0)<=121){
          str1=str1+split[i];
        }else {
          continue;
        }
      }
```
### Write the character and their occurence corresponding to each other
```
    String str = "aaaxbbccd";
    String res=""+str.charAt(0);
    int count =1;
    for(int i=1;i<str.length();i++){
      if(str.charAt(i)==str.charAt(i-1)){
        count++;
      }else{
        res=res+count+str.charAt(i);
        count=1;
      }
    }

      System.out.println(res);
// Output: a3x1b2c2d
```

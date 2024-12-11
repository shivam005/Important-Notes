Initialize two pointers as i and j.
Run the loop while j is less that the size of the array.
Check if the element at j index is vowel then increase the count.
If j-i+1 is becoming equal to the k then increase the ith pointer and if the element at the ith index is vowel then reduce the count and since we are now shifting the window hence it is prudent to update the maxVowelCount variable at this moment. 
```
package somepackage.twopointerslidingwindow;

public class MaximumNumberOfVowelsInSubstringOfGivenLength {

    public int check( String str, int k){
        char[] arr=str.toCharArray();
        int i=0,j=0;
        int maxLength =0;
        int count=0;
        while(j<arr.length){
            if(checkVowel(arr[j])){
                count++;
            }
            if(j-i+1==k){
                maxLength= Math.max(maxLength,count);
                if(checkVowel(arr[i])){
                    count--;
                }
                i++;
            }

            j++;
        }
        return maxLength;
    }
    public static boolean checkVowel(char c){
        if(c=='a' || c=='e' || c=='i' || c=='o' || c=='u'){
            return true;
        }
        return false;
    }

    public static void main(String[] args) {
        String str= "aeiou";
        int check = new MaximumNumberOfVowelsInSubstringOfGivenLength().check(str, 2);
        System.out.println(check);
    }
}

```

# AlgoExpert

### Move all Zeros to the end of the array
First, using a loop, we will place the pointer j. If we don’t find any 0, we will not perform the following steps.
After that, we will point i to index j+1 and start moving the pointer using a loop.
While moving the pointer i, we will do the following:
If a[i] != 0 i.e. a[i] is a non-zero element: We will swap a[i] and a[j]. Now, the current j is pointing to the non-zero element a[i]. So, we will shift the pointer j by 1 so that it can again point to the first zero.

```
package Array;

import java.util.Arrays;

public class Shiva {

    public static  int[] check(int[] arr){
        int j=Integer.MIN_VALUE;
        for(int i=0;i< arr.length;i++){
            if(arr[i]==0){
                j=i;
                break;
            }
        }
        for(int i=j+1;i< arr.length;i++){
            if(arr[i]!=0){
                arr[i]=arr[i]+arr[j];
                arr[j]=arr[i]-arr[j];
                arr[i]=arr[i]-arr[j];
                j++;
            }
        }

        return arr;
    }


    public static void main(String[] args) {
        int[] arr={2,1,0,2,1,0,2};


        System.out.println( Arrays.toString(check(arr)));
    }
}

// Time Complexity == O(N)
```
### Move 


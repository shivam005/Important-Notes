Herein, we will be running the loop till j is less than size of the array. We will check two things:
First, if j-i is less than or equal to k and if hashset contains arr[j] then return true else add the element into the hashset. 
Second, if j-i is not less than or equal to k then remove the element at ith index and increment the i. 
If everything goes well then return the false. 
```
package somepackage.twopointerslidingwindow;
import java.util.HashSet;

public class ContainsDuplicateInGivenWindow {

    public boolean check(int[] arr , int k) {
        int i=0,j=0;
        HashSet<Integer> hs = new HashSet<>();
        while (j<arr.length) {
            if (j - i <= k) {
                if (hs.contains(arr[j])) {
                    return true;
                } else {
                    hs.add(arr[j]);
                }
                j++;
            }else {
                hs.remove(arr[i]);
                i++;
            }
        }
        return false;
    }

    public static void main(String[] args) {
        int[] arr ={1,2,3,1,2,3};
        boolean check = new ContainsDuplicateInGivenWindow().check(arr, 2);
        System.out.println(check);
    }
}

```

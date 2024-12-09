It has 4 steps:
1. Keep running the loop as long as j is less than n
2. check if the element at the j index is negative then add this into temp deque.
3. check if the size of the window (j-i+1) is equal to K then get the first element from temp deque and put this into result deque, provided deque is not empty or put zero into result deque.
4. also at same time, check if the element at i index is negative and deque is not empty then remove the element from temp deque (We are doing it as we are moving to a new window, so the temp deque should not have element of previous window) and increment the ith index.
5. Keep on incrementing the jth index as well. 
```
package somepackage.twopointerslidingwindow;

import java.util.ArrayDeque;
import java.util.Deque;

public class FirstNegativeIntegerInEveryWindowOfSizeK {

    public void check(int arr[], int k) {
        int n = arr.length ;
        Deque<Integer> dq = new ArrayDeque<>();
        ArrayDeque<Integer> res = new ArrayDeque<>();
        int i = 0;
        int j = 0;
        while (j < n) {
            if (arr[j] < 0) {
                dq.add(arr[j]);
            }
            if (j - i + 1 == k) {
                if (!dq.isEmpty()) {
                    res.add(dq.getFirst());
                } else {
                    res.add(0);
                }
                if (arr[i] < 0 && !dq.isEmpty()) {
                    dq.removeFirst();
                }
                i++;
            }
            j++;
        }
        System.out.println(res);
    }

    public static void main(String[] args) {
        int[] arr = {12, -1, -7, 8, -15, 30, 16, 28};
        new FirstNegativeIntegerInEveryWindowOfSizeK().check(arr, 3);
    }
}

```

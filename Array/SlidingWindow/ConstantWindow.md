Herein the constant window, we first calculate the sum of first k numbers and then we keep on subtracting the first element and keep on adding the next new element. Further, we store the sum into a variable and
then we make comparison to the maxsum element which has the sum value of first k element. 
#### Given an array and an integer K, return the maximum sum that can be obtained by picking up K elements consecutively.
```
package somepackage.array;

public class ContantWindow {

    public int check1(int[] arr, int k) {
        int l = 0;
        int r = k - 1;
        int n = arr.length;
        int sum = 0;
        int maxSum = 0;
        for (int q = 0; q < k; q++) {
            sum = sum + arr[q];
        }
        maxSum = sum;
        while (r < n - 1) {
            sum = sum - arr[l] + arr[r + 1];
            maxSum = Math.max(maxSum, sum);
            l++;
            r++;
        }
        return maxSum;
    }
 

    public static void main(String[] args) {

        int[] arr = {4, 5, 4, 6, 7, 8, 3};
        int check = new ContantWindow().check1(arr, 3);
        System.out.println(check);
    }
}

```

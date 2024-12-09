Herein, we can initialise two pointers as i and J to 0 and another variable as size as length of the array. We will move the pointer as long as J is not reaching the end. 
1. Keep on adding the array at  the index j untill the sum is not greater than the target sum and keep on incrementing j (Or greater than or equal to in case the equal would also work).
2. If it is greater than target then increase the i pointer and at the same time, subtract the the elemnt at ith index from sum.
3. Since we  have to find the size to keep on updating the size to k-i+1.
```
package somepackage.twopointerslidingwindow;
public class MinimumSizeSubarrayWithSumGreaterThanK {
    public int check(int[] arr, int k){
        int sum =0;
        int i=0;
        int j=0;
        int n=arr.length-1;
        int size=n+1;
        while(j<n){
            sum = sum+arr[j];
            while (sum>=k){
               size= Math.min(size, j-i+1);
                sum=sum-arr[i];
                i++;
            }
            j++;
        }
        return size;
    }

    public static void main(String[] args) {
        int[] arr={1, 4, 45, 6, 0, 19};
        int check = new MinimumSizeSubarrayWithSumGreaterThanK().check(arr, 51);
        System.out.println(check);
    }
}

```

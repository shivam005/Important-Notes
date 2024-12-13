Herein the constant window, we first calculate the sum of first k numbers and then we keep on subtracting the first element and keep on adding the next new element. Further, we store the sum into a variable and
then we make comparison to the maxsum element which has the sum value of first k element. 
#### Given an array and an integer K, return the maximum sum that can be obtained by picking up K elements consecutively.
```
package somepackage.array;

public class ContantWindow {
  public int calculate(int[] arr, int k){
        int j=k; int i=0;
        int n = arr.length;
        int sum =0;
        int maxSum=0;
        for(int q =0; q<k;q++){
            sum =sum+arr[q];
        }
        while (j<n){
            sum = sum -arr[i]+arr[j];
            maxSum = Math.max(maxSum, sum);
            i++;j++;
        }
        return maxSum;
    }
    public static void main(String[] args) {
    int[] arr ={1,2,3,4,5,6,7,8};
        int i = new FindMaxSumofAlltheSubArrayOfSizeK().calculate(arr, 2);
        System.out.println(i);
    }
}
output:: 15

```

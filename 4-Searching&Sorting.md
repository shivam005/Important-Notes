### Merge Sort
It is done in the following steps:
1. create a sort() which would take 3 param; array, left index, right index
2. find the mid point of the array.
3. Recursively call the sort method and pass index from left to mid+1.
4. Again recursively call the sort method and pass index from mid to right.
5. It will be basically continiously splitting it into the shorted possible array.
6. Finally merge it and we have to merge it in such a way that while merging, it should be merged in the sorted order.
7. create merge() which would take param as arr, left index, mid index and right index.
8. now find the length of subarray which we have got post splitting it.
9. We can find the length of left array by subtracting mid index from left index plus 1.
10. We can find the length of right array by subtracting right index from  mid index.
11. Initialize two arrays with the length as computed above.
12. Insert the element from the array into both of this initialized array which can be done by creating a counter which would be traversing the given array.
13. Insert elements into the second array, keep on increasing the counter.
14. Now we have to merge both the arrays.
15. Intiatlize two counters (say i and j ) to traverse both the created arrays and assign the another counter (say k) for traversing the array to left index. Put a loop if the both the counter is less than the size of their respective array then continue, use && operator.
16. inside the loop, check if the current element in the left array is less than the current element in the right array then put this into the kth index of the array else put the element from right array .
17. Its time to fill the remaining elements into the array.
18. Put two seperate loops and check if initialized counter (say i) is less than the size of left array then keep on assigning this into the array at consecutive indices of k.
19. Good job, your array has been sorted.


```
package org.java.searchandsort;

import java.util.Arrays;

public class MergeSort {

    public void sort (int[] arr , int l, int r){
        if(l< r){
            int mid =l+(r-l)/2;
            sort(arr, l, mid);
            sort(arr, mid+1, r);
            merge(arr, l, mid, r);
        }

    }

    public void merge(int[] arr, int l, int mid, int r){
        int n1=mid-l+1;
        int n2= r-mid;
        int[] left = new int[n1];
        int[] right = new int[n2];
        int k=l;
        for(int i=0; i< n1;i++){
          left[i]=arr[k];
          k++;
        }
        for(int i=0; i< n2;i++){
            right[i]=arr[k];
            k++;
        }
        int i=0; int j=0; k=l;
        while(i < n1 && j< n2){
            if(left[i]<right[j]){
                arr[k]=left[i];
                k++;i++;
            } else {
                arr[k]=right[j];
                k++;j++;
            }
        }

        while(i<n1){
            arr[k]=left[i];
            i++;
            k++;
        }
        while(j<n2){
            arr[k]=right[j];
            j++;
            k++;
        }

    }


    public static void main(String[] args) {
        int[] arr = {2,3,1,2,3,1,1,1};
        System.out.println(Arrays.toString(arr));
        new MergeSort().sort(arr, 0, arr.length-1);
        System.out.println(Arrays.toString(arr));

    }
}

```

```
package somepackage.twodarray;

public class SearchElementInMatrix {
// Herein, we will first initialize two pointer from 0 and end of the array. We will check if the element at the current indices is equal
    // then return or else if the element at the indices is greater then reduce the higher pointer or else increase the lower pointer.
    // this is applicable for the sorted matrix only.
    public void search(int[][] arr, int k){
        int n = arr.length;
        int i =0 ; int j =arr.length-1;
        while(i<n && j>0){
            if(arr[i][j]==k){
                System.out.println("found");
                return;
            } else if (arr[i][j]>k) {
                j--;
            }else {
                i++;
            }
        }
        System.out.println("Not Found");
    }

    public static void main(String[] args) {
        int[][] arr = {
                {1, 2, 3},
                {4, 5, 6},
                {7, 8, 9}
        };
new SearchElementInMatrix().search(arr, 5);
    }
}
```

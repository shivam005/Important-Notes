```
package somepackage.twodarray;

public class ZigZagTraversal {
    // Traverse row 0 left-to-right, row 1 right-to-left, and so on.
    // Differentiate on the basis of even-odd

    public void traverse(int[][] arr){
        // 00 01 02
        // 10 11 12
        // 20 21 22
        int r = arr[0].length;
        int c = arr.length;

            for (int i = 0; i < r; i++) {
                if(i%2==0) {
                for (int j = 0; j < c; j++) {
                    System.out.print(arr[i][j]);
                }
            }
        else {
                for (int j = c-1; j >=0; j--) {
                    System.out.print(arr[i][j]);
                }
        }
    }
    }

    public static void main(String[] args) {
        int[][] arr = {{1,2,3},
                {4,5,6},
                {7,8,9}};
        new ZigZagTraversal().traverse(arr);
    }
}
```

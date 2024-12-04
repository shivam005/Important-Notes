```
package somepackage.twodarray;

public class ReverseOrderTraversal {


    public void check(int[][] arr){
        int row = arr[0].length;
        int column = arr.length;
        //22 21 20, 12 11 10, 02 01 00
        for(int i=row-1 ;i>=0;i-- ){
            for(int j=column-1;j>=0;j--){
                System.out.print(arr[i][j]);
            }
        }
    }

    public static void main(String[] args) {
        int[][] arr = {
                {1, 2, 3},
                {4, 5, 6},
                {7, 8, 9}
        };
//        9 8 7
//        6 5 4
//        3 2 1
        new ReverseOrderTraversal().check(arr);

    }
}
```

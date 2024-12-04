```
package somepackage.twodarray;

public class ColumnWiseTraversal {

    public void traverse(int[][] arr){
        // 00 01 02
        // 10 11 12
        // 20 21 22
        int r = arr[0].length;
        int c = arr.length;
        for(int i=0 ; i<r;i++){
            for(int j=0;j<c;j++){
                System.out.print(arr[j][i]);
            }
        }
    }


    public static void main(String[] args) {
        int[][] arr = {{1,2,3},
                       {4,5,6},
                       {7,8,9}};
        new ColumnWiseTraversal().traverse(arr);
    }
}

```
```
147258369
```

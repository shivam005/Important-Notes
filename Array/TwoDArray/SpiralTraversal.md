```
package somepackage.twodarray;

public class SpiralTraversal {

//    In order tp traverse, first define 4 pointers as left, right, top and bottom.
    // initialize it and then traverse until left is less than or equal to right and top is less than or equal to bottom
    // traverse "i" from  left to right wherein you will be having "top" as row and i as column
    // increment top to come one step lower
    // traverse "i" from top to bottom wherein you will have right as column and i as row.
    // decrement right to go one step left to avoid the last attendant element
    // traverse "i" from right to left in decreasing order wherein row will be bottom and column will be i (also  keep check top is less than or equal to bottom)
    // decrement bottom to go one step above
    // traverse "i" from bottom to top in the decreasing order wherein row will be left and column will be i. (check left is less than or equal to right)
    // increment left to go one step rightward.
    // the loop will be keep on going and will be able to traverse whole matrix

    public void exec(int[][] arr){
        int left =0; int right =arr[0].length-1 ;
        int top =0; int bottom = arr.length -1;
        while(left <=right && top<=bottom){
            for(int i =left ; i<=right ;i++){
                System.out.print(arr[top][i]);
            }
            top++;
            for(int i=top ; i<=bottom;i++){
                System.out.print(arr[i][right]);
            }

            right--;
            if(top<=bottom) {
                for (int i = right; i >= left; i--) {
                    System.out.print(arr[bottom][i]);
                }
                bottom--;
            }
            if(left<=right){
                for(int i =bottom; i>=top; i--){
                    System.out.print(arr[i][left]);
                }
                left++;
            }

        }

    }

    public void traverse(int[][] arr){
        int left =0 ; int right = arr[0].length-1;
        int top =0; int bottom = arr.length-1;
        while(left <= right && top <= bottom){
            for(int i =left; i<=right; i++){
                System.out.print(arr[top][i]);
            }
            top++;
            for(int i =top; i<=bottom; i++){
                System.out.print(arr[i][right]);
            }
            right--;
            if(top<=bottom){
               for(int i=right; i>=left;i--){
                   System.out.print(arr[bottom][i]);
               }
               bottom--;
            }
            if(left<=right){
                for(int i =bottom; i>=top;i--){
                    System.out.print(arr[i][left]);
                }
             //   left++;
            }
        }
    }


    public static void main(String[] args) {
        int[][] array = {{9,3,9,3,9,7,9},
                        {9,7,3,9,7,3,7 },
                        {1,2,3,4,1,2,3 }};
        int[][] arr = {
                {1, 2, 3},
                {4, 5, 6},
                {7, 8, 9}
        };
        new SpiralTraversal().traverse(arr);

        // 93939793214321973973
        //  00 01 02 03 04 05 06
        //  16
        //  26 25 24 23 22 21 20
        //  10 11 12 13 14 15 16
        // 0123456 6 6543210 0123456

    }
}
```

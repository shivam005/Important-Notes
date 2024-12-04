```
package somepackage.twodarray;

public class RowWithMaximum1s {

    // Herein, while traversing, since the inner loop would be looking into each row. We can sum up each row and can get it compared
    // with the another variable max and if it is found to be bigger then we can update the max variable while traversing each row 
    // we also will have to maintain the row number in a variable so that post comparison we can maintain the record 
    // of the indices for which the max variable was updated. 

    public void check(int[][] arr){
        int max =0;
        int indice=0;
        for(int i =0; i< arr.length;i++){
            int countRow=0;
            int row =0;
            for(int j =0 ; j< arr[0].length;j++){
                if(arr[i][j]==1){
                    countRow=countRow+1;
                }
                row=i;
            }
            if(max<countRow){
                max=countRow;
                indice=row;
            }
           // Math.max(countRow,max);
        }
        System.out.println(indice);
    }

    public static void main(String[] args) {
        int[][] arr =  { {0, 0, 0, 1},
                {0, 1, 1, 1},
                {1, 1, 1, 1},
                {0, 0, 0, 0}};

        new RowWithMaximum1s().check(arr);
    }
}

```

In the first row (i=0) there are 4 spaces, 1 star, then again 4 spaces. 
In the second row (i=1) there are 3 spaces, 3 stars, then again 3 spaces so we can say that there are N-i-1 spaces, 
2*i+1 stars (Odd number series formula), and then again N-i-1 spaces for each row where i is the row index. We thus simply run 3 inner loops first for printing the spaces, then the stars, and then the spaces again.
```
package somepackage.forloop;

public class DrawTriangle {

    public void draw(){
        int n=5;
         for(int i =0; i<n;i++){
             for(int j=0 ; j<n-i-1;j++ ){
                 System.out.print(" ");
             }
             for(int k=0; k<2*i+1;k++){
                 System.out.print("*");
             }
             for(int l=0; l<n-i-1;l++){
                 System.out.print(" ");
             }
             System.out.println(" ");
         }
    }

    public void draw1() {
        int N = 5;
    for(int i=0; i< N ;i++){

        for(int l=0; l<N-i-1;l++){
            System.out.print(" ");
        }
//        0-> 4 space,1 star,4 space
//        1-> 3 space,3 star,3 space
        for (int j=0;j<2*i+1;j++){
            System.out.print("*");
        }
        for (int k=0;k<N-i-1;k++){
            System.out.print(" ");
        }
        System.out.println("");
    }
    }


    public static void main(String[] args) {
    new DrawTriangle().draw1();
    }
}


```
```
    *    
   ***   
  *****  
 ******* 
*********
```


```
package somepackage.forloop;

public class DiamondStar {

 // Combination of both trinangle and inverted triangle
    public static void main(String[] args) {
        new DrawTriangle().draw();
        new InvertedTriangle().draw();
    }
}

```

```
package somepackage.array;
class Main {

    public void print1(int n){
        for(int i=0; i<=n; i++){
            for(int j =0;j<=i;j++) {
                System.out.print(" ");
            }
                for(int k=0; k<2*n-2*i+1;k++){ // 2n-2i+1 is the reverse odd sequence
                    System.out.print("*");
                }
                System.out.println("");
            }
    }
 
    public void print(int n){
        for(int i=0; i<=n; i++){

            for(int j =n; j>=i;j--){
                System.out.print(" ");
            }
            for(int k=0; k<=2*i+1;k++){
                System.out.print("*");
            }
            System.out.println("");
        }
    }

    public static void drawDiamond(int n) {
        // Upper part of the diamond
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                System.out.print(" ");
            }
            for (int j = 0; j < 2 * i + 1; j++) {
                System.out.print("*");
            }
            System.out.println();
        }
        // Lower part of the diamond
        for (int i = n - 1; i >= 0; i--) {
            for (int j = 0; j < n - i - 1; j++) {
                System.out.print(" ");
            }
            for (int j = 0; j < 2 * i + 1; j++) {
                System.out.print("*");
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
         new Main().print(4);
         new Main().print1(4);
         drawDiamond(5);
    }
}

```

```
    *     
   ***    
  *****   
 *******  
********* 
********* 
 *******  
  *****   
   ***    
    *     

```

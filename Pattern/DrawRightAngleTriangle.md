
```
package somepackage.forloop;

public class DrawRightAngleTriangle {

   public void draw(){
// *
// **
// ***
// ****
// *****
        for(int i=0;i<= 5;i++){
            for(int j=0; j< i ;j++){
                System.out.print("*");
            }
            System.out.println("  ");
        }
    }

    public void drawWithNumber(){
//        1
//        1 2
//        1 2 3
//        1 2 3 4
//        1 2 3 4 5
        for(int i=0; i<=5;i++){
            for(int j=1; j<= i; j++){
                System.out.print(j+" ");
            }
            System.out.println(" ");
        }
    }

    public void drawWithRepeatedNumber(){
//        1
//        22
//        333
//        4444
//        55555
        for(int i=1; i<=5;i++){
           for(int j=1; j<=i;j++){
               System.out.print(i);
           }
           System.out.println(" ");
       }
    }

    public static void main(String[] args) {
        new DrawRightAngleTriangle().drawWithRepeatedNumber();
    }
}
```

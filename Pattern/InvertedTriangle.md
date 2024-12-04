we can clearly observe that for each row there are some spaces that get printed then some stars, and then again some spaces giving it an inverse pyramidal look.
For eg: In the first row (i=0) there are 0 spaces, 9 stars, then again 0 spaces. In the second row (i=1) there is 1 space, 7 stars, then again 1 space so we can say that 
there are i spaces, 2*N - (2*i+1) stars, and then again i space for each row where i is the row index. We thus simply run 3 inner loops, first for printing the spaces, then the stars, and then the spaces again.
```
package somepackage.forloop;

public class InvertedTriangle {

    public void draw(){
//        *********
//         *******
//          *****
//           ***
//            *

        // 9 -> 0 space  0
        // 7 -> 2 space  1
        // 5 -> 4 space  2
        // 3 -> 6 space  3
        int N=5;
        for(int i=0 ; i< N;i++){

            for(int k=0; k<i;k++){
                System.out.print(" ");
            }

            for(int j =0; j<2*N-2*i-1;j++){
                System.out.print("*");
            }
            for(int k=0; k<i;k++){
                System.out.print(" ");
            }
            System.out.println(" ");
        }
    }


    public void draw1(){
        int N =5;
        for(int i=N;i>=0;i--){
            for(int j=0; j< N-i-1;j++){
                System.out.print(" ");
            }
            for(int k =0 ;k<2*i+1;k++){
                System.out.print("*");
            }
            for (int l=0;l<N-i-1;l++){
                System.out.print(" ");
            }
            System.out.println(" ");
        }
    }
    public static void main(String[] args) {
     new InvertedTriangle().draw();
    }
}

```
```
********* 
 *******  
  *****   
   ***    
    * 
```

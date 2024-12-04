As we can observe from the examples for N = 3 we have 5 rows, and for N = 6 we have 11 rows, hence the outer loop will run for 2*N -1 times. 
For the inner loop where we print the stars if row no. is less than or equal to N, then we observe that the stars which are printed in each row are equal to the row index itself. 
But, when i becomes more than N, then the no. of stars decreases by 1 with each increasing row. 
So, therefore the stars printed would be 2*N - i after i becomes greater than N.
```
package somepackage.forloop;

public class HalfDiamondStar {

    public void draw(){
        int N =5;
        for(int i=0; i<2*N ;i++){
            if(i<=5){
            for(int j=0; j<i;j++){
                System.out.print("*");
            }
            System.out.println(" ");
        }else {
                for(int k=N-1;k>i;k--){
                    System.out.print("*");
                }
                System.out.println(" ");
            }
        }
    }

    public void draw1(){
//*
//**
//***
//****
//*****
//****
//***
//**
//*
        int N=5;
        for(int i=0 ; i< 2*N;i++){
            if(i<=5){
            for(int j=0; j<i;j++){
                System.out.print("*");
            }
                System.out.println(" ");
            }else {
               //  6-4, 7-3 , 8-2, 9-1
                for(int k =0 ; k< 2*N-i;k++){
                    System.out.print("*");
                }
                System.out.println(" ");
            }
        }
    }

    public static void main(String[] args) {

       new HalfDiamondStar().draw1();
    }
}
```
```
* 
** 
*** 
**** 
***** 
**** 
*** 
** 
* 
```

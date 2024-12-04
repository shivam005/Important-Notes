
```
package somepackage.forloop;

public class DrawReverseRightAngleTriangle {

    public void draw(){
//*****
//****
//***
//**
//*
        for(int i=1 ;i<=5;i++){
            for(int j=i; j<=5;j++){
                System.out.print("*");
            }
            System.out.println(" ");
        }
    }

    public  void drawWithNumbers(){
//        12345
//        1234
//        123
//        12
//        1
        for(int i=0; i<=5;i++){
            for(int j =1; j<=5-i;j++){
                System.out.print(j);
            }
            System.out.println(" ");
        }
    }

    public static void main(String[] args) {
        new DrawReverseRightAngleTriangle().drawWithNumbers();
    }
}

```

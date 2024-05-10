
### Can we override variables in Java?
No, in Java, you cannot override variables. Variable hiding, also known as shadowing, occurs when a subclass declares a variable 
with the same name as a variable in its superclass. 
However, this does not override the variable in the superclass; instead, it hides it within the scope of the subclass.

### What is method hiding?
Method hiding occurs when a subclass defines a static method with the same signature as a static method in its superclass. 
Unlike method overriding, which is dynamic and based on the runtime type of objects, 
method hiding is resolved at compile time based on the reference type.

```
public class ParentClass {

    int a=9;

    public static void check(){
        System.out.println("Parent");
    }

}
public class ChildClass extends ParentClass {

    int a=8;

    public static void check(){
        System.out.println("child");
    }

}
public class RunnerClass {

    public static void main(String[] args) {

        ParentClass parentClass = new ChildClass();
        System.out.println(parentClass.a);
        parentClass.check();
    }
}

Output -> 
9
Parent
```

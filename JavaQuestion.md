### Comparable and Comparator
You cannot call Collections.sort() method on any object If it does not implement comparable or comparator interface. 

Comparable: Use when a single natural order is sufficient, implemented within the class. (CompareTo)
Comparable interface compares “this” reference with the object specified.
we could just sort by only one attribute, i.e., year.
A comparable object is capable of comparing itself with another object
```
public class Employee implements Comparable<Employee>{

    String name;
    Address address;

    @Override
    public int compareTo(Employee o) {
         return  o.name.compareTo(this.name);
    }

}
// Here on calling this collections.sort(), list will get sorted on the basis of name;
 Collections.sort(list)
```
Comparator: Use for multiple or custom orderings, implemented outside the class.(Compare)
Comparator in Java compares two different class objects provided.
In the comparator, we were able to use different attributes like rating, name, and year as well.
Unlike Comparable, Comparator is external to the element type we are comparing. It’s a separate class. 
We create multiple separate classes (that implement Comparator) to compare by different members.
 ```
public class EmployeeComparatorByAddress implements Comparator<Employee> {
   @Override
    public int compare(Employee o1, Employee o2) {
          if(o1.address.equals(o2.getAddress())){
              return 1;
          }else {
              return 0;
          }
    }

}

// Here, we have used the custom comparator wherein we are sorting based on address.
 Collections.sort(list,  new  EmployeeComparatorByAddress());

 ```


### What is serialVersionUID ?
the automatically-generated UID is generated based on a class name, implemented interfaces, and all public and protected members. 
Changing any of these in any way will change the serialVersionUID. So you don't need to mess with them only if you are certain that no more than one version 
of the class will ever be serialized (either across processes or retrieved from storage at a later time).

### If there is a common default method in two interfaces then when we will implement it in a class then what would be the behaviour which one would be called??
Herein, It would become mandatory to implement default method as well and while implementating it, we will have to mention which method from which interface needs to be called up. 
like "Interface1.super.check()" or "Interface2.super.check().
```
public interface Interface1 { 
    default void check(){
        System.out.println("Interface1");
    }
}
```
```
public interface Interface2 {
    default void check(){
        System.out.println("Interface2");
    }
}
```
```
public class InterfaceRunner implements Interface1, Interface2{
    @Override
    public void check() {
        Interface1.super.check();
    }
    public static void main(String[] args) {
        InterfaceRunner i=new InterfaceRunner();
        i.check();
    }

}
```

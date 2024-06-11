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

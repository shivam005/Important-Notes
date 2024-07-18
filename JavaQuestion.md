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
### Causes of memory leak
JavaVisualVM is package comes with JDK which can be used to check the object creation and the memory usage. We can also analyze the memory and can call GC.
1. Excessive use of static variables. Static members never gc as they are stored in heap and has life equals to the application.
2. Unclosed resources
3. Improper equals and hashcode method implementation
4. Excessive session objects
5. Poorly written custom data structures.

Eden Space >> Survivor space >> Tenured Space >> Metaspace(Expand and shrink size automatically)
When Eden(young gen) space gets filled up then a minor GC runs which cleans up the memory, the objects which survives more GC than threshold are promoted to survivor space(Young gen) and who survives here are further promoted to tenured space (Old Gen Space) when the old gen gets filled up then major GC is called up which considerably releases memory but as heavy as to impact the main thread. 
Metaspace is also there which is used to store metadata about classes, such as class names, method names, field names, and other class-related information. 
"-verbose:gc" It can be used in  the command to have verbose info related to gc. 

### Garbage Collectors

| **Garbage Collector** | **Use Case**                            | **Generational** | **Concurrent** | **Advantages**                | **Disadvantages**                      |
|-----------------------|-----------------------------------------|------------------|----------------|--------------------------------|---------------------------------------|
| Serial GC             | Small/single-threaded applications      | Yes              | No             | Simple, low overhead           | Long pauses, not for large/multi-threaded apps |
| Parallel GC           | Multi-threaded, throughput-focused apps | Yes              | No             | Good throughput                | Longer pauses, less suitable for low-latency apps |
| CMS GC                | Low-pause-time applications             | Yes              | Partly         | Low pause times                | Higher CPU, fragmentation, concurrent mode failures |
| G1 GC                 | Large heap, balanced performance        | Yes              | Partly         | Predictable pause times        | Complex tuning                         |
| ZGC                   | Extremely low-latency, large heap       | Yes              | Fully          | Very low pause times, handles large heaps | Higher CPU/memory overhead             |
| Shenandoah GC         | Low pause times, evolving feature set   | Yes              | Fully          | Low pause times                | Higher CPU/memory overhead, evolving  |
| Epsilon GC            | Performance testing, external memory management | No               | No             | Zero GC overhead               | Memory will eventually run out        |

 

# Java Data Structures Default Initial Sizes

| Data Structure      | Default Initial Size / Capacity | Description                                                                 |
|---------------------|---------------------------------|-----------------------------------------------------------------------------|
| ArrayList           | 10                              | A resizable array implementation of the `List` interface.                   |
| HashMap             | 16 (initial capacity), 0.75 (load factor) | A hash table-based implementation of the `Map` interface.               |
| HashSet             | 16 (initial capacity), 0.75 (load factor) | A hash table implementation of the `Set` interface.                      |
| LinkedHashMap       | 16 (initial capacity), 0.75 (load factor) | A hash table and linked list implementation of the `Map` interface with predictable iteration order. |
| LinkedHashSet       | 16 (initial capacity), 0.75 (load factor) | A hash table and linked list implementation of the `Set` interface with predictable iteration order. |
| LinkedList          | Not fixed (size grows dynamically) | A doubly-linked list implementation of the `List` and `Deque` interfaces. |
| TreeMap             | Not applicable (size grows dynamically) | A Red-Black tree-based implementation of the `NavigableMap` interface. |
| TreeSet             | Not applicable (size grows dynamically) | A NavigableSet implementation based on a TreeMap.                          |
| PriorityQueue       | 11                              | A priority heap-based implementation of the `Queue` interface.             |
| ConcurrentHashMap   | 16 (initial capacity), 0.75 (load factor), 16 (concurrency level) | A hash table supporting full concurrency of retrievals and adjustable expected concurrency for updates. |
| Vector              | 10                              | A synchronized, resizable array implementation of the `List` interface.    |
| Stack               | Not fixed (extends Vector, so initial size is 10) | A last-in, first-out (LIFO) stack of objects.                          |

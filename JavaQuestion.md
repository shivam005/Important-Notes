### Comparable and Comparator
When we have to do natural ordering then we go for comparable. (CompareTo)

If we have to make custom ordering then we go for compartor. (Compare)


### What is serialVersionUID ?
the automatically-generated UID is generated based on a class name, implemented interfaces, and all public and protected members. 
Changing any of these in any way will change the serialVersionUID. So you don't need to mess with them only if you are certain that no more than one version 
of the class will ever be serialized (either across processes or retrieved from storage at a later time).

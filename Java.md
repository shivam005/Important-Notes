# Important-Notes

## why do we not specify new keyword at the time of creating instance variable with wrapper class?

In Java, wrapper classes (such as Integer, Double, Boolean, etc.) are objects that "wrap" a primitive value. When you create an instance variable of a wrapper class, you do not use the "new" keyword because these classes have static factory methods that return instances of the class.
For example, instead of using the "new" keyword to create an Integer object that wraps the value 5, you can use the static factory method Integer.valueOf(5). 
This is equivalent to creating a new Integer object with the "new" keyword:

Additionally, in Java 8 and later versions, autoboxing feature automatically converts primitive types to their corresponding wrapper class objects, so you don't need to use the valueOf() method explicitly. 

It's also worth noting that the static factory methods, such as Integer.valueOf(), are generally preferred over the constructors, such as new Integer(), because they can provide additional performance benefits.

Using static factory method is more efficient because it can return an already-existing instance if one exists (for example, if -128 to 127) or create a new one if not. This can save memory and can be faster than creating a new instance each time.

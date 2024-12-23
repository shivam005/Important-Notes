# Important-Notes

## why do we not specify new keyword at the time of creating instance variable or the empty instance of variable with wrapper class?

In Java, wrapper classes (such as Integer, Double, Boolean, etc.) are objects that "wrap" a primitive value. When you create an instance variable of a wrapper class, you do not use the "new" keyword because these classes have static factory methods that return instances of the class.
For example, instead of using the "new" keyword to create an Integer object that wraps the value 5, you can use the static factory method Integer.valueOf(5). 
This is equivalent to creating a new Integer object with the "new" keyword:

Additionally, in Java 8 and later versions, autoboxing feature automatically converts primitive types to their corresponding wrapper class objects, so you don't need to use the valueOf() method explicitly. 

It's also worth noting that the static factory methods, such as Integer.valueOf(), are generally preferred over the constructors, such as new Integer(), because they can provide additional performance benefits.

Using static factory method is more efficient because it can return an already-existing instance if one exists (for example, if -128 to 127) or create a new one if not. This can save memory and can be faster than creating a new instance each time.

## why this can not be referenced from static context?

"This" cannot be referenced from a static context because "this" refers to the current instance of an object, and a static context refers to a class or method that does not have access to an instance of an object. In other words, "this" refers to an object that has been instantiated, whereas a static context refers to the class or method itself, which does not have access to any specific instance of an object.

## What is CompletableFuture?
It is the way of handling async methods without blocking the main thread. Usually in case of future, main thread gets blocked but here a seperate thread is created which actually processes the async method and the main method keeps on processing rest of the code.

It has below methods:

runAsync() --> It runs in the background and does not return anything.

supplyAsync() --> Run async in the background and will return value from the task.

get() --> It blocks the execution untill the future is completed.

thenApply() --> It will wait for the previous async method to be completed and whatever the output will come from there. It will use it for further processing.

thenAccept() --> It does not return anything, it just accepts the output coming from previous future. 

## What is Map.Entry ?
Map.Entry is a key and its value combined into one class.
## What is <? extends T> and <? super T>?
It is bounded wildcards. A bounded wildcard (<? extends T> or <? super T>) places a restriction on the type by saying that it either has to extend a specific type (<? extends T> is known as an upper bound), or has to be an ancestor of a specific type (<? super T> is known as a lower bound).
## What is difference between map.entry and entryset
Map.Entry is an interface that represents a **single** key-value pair, and it's used when you need to work with individual entries of a map. entrySet() is a method provided by the Map interface that returns a **set of all key-value pairs** in the map, which can be used for iterating over all entries or performing batch operations.

## what is for (;;)?
It is an infinite loop and needs break statement to terminate.

## what is coupling and cohesion?
Cohesion refers to the degree to which elements within a module work together to fulfill a single, well-defined purpose.
High cohesion means that elements are closely related and focused on a single purpose, while low cohesion means that elements are loosely related and serve multiple purposes.
Coupling is the measure of the degree of interdependence between the modules. A good software will have low coupling. 
High cohesion means that elements are closely related and focused on a single purpose, while low cohesion means that elements are loosely related and serve multiple purposes.
High coupling and low cohesion can make a system difficult to change and test, while low coupling and high cohesion make a system easier to maintain and improve.

## How String class works?
String in java is immuatble class which internally points to a shell address which further points to the actual instance. We can not make
any changes in the instance whenever we perform any assignment then we just change the address. Even when we use 'new' keyword then also
it does not make any change in the instance rather it create a new shell address which starts pointing to the same instance which is lying
in the string constant pool. Hence, String instance is immuatable but there reference is mutable. 

## What happends when an instance variable is made final
Whenever we make any instance variable final then it can be only intialized once using either direct assignment or constructor. It would remain unique for an individual object. If we want to make it unique "per class" then it is recommended to make it "static".

##


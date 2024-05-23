# LLD


### Box will have to 3 section
1. Top: Class Name
2. Middle: Instances
3. Bottom: Methods

### Representation of access modifier
1. "+" public
2. "-" private
3. "#" protected

### Association (Can call or uses relationship)
Association means how two things are related to each other like A can call B but B can not call A in case of unidirectional association.
#### Association or bidirectional association 
 Both can call each other
```
A⎯⎯⎯⎯⎯B
A<⎯⎯⎯⎯>B
```
#### Unidirectional association 
A can call B but B can not call A.
```
.
```
#### Multiplicity
Herein, we can also define one to many, many to many or many to one sort of relationship. 
We can also explicitly write the numbers as well. 
```
A-4⎯⎯⎯⎯1->B : four to one
A-1⎯⎯⎯⎯*->B : one to many
A-*⎯⎯⎯⎯*->B : many to many
A-*⎯⎯⎯⎯1->B : many to one
A-n⎯⎯⎯⎯1..2->B : n to (1 to 2)
```

### Aggregation & Composition (It refers to "has an" relationship)
Aggregation: B can exist without A
```
A-◇⎯⎯⎯⎯⎯B
Vehicle⎯⎯⎯Tyre
```
Composition: B cannot exist without A
```
A-◆⎯⎯⎯⎯⎯B
Body-◆⎯⎯⎯⎯Eye
Vehicle⎯⎯⎯⎯Registration-Card
```

### Inheritance (Is an relationship)
It is represented to solid arrow
```
A⎯⎯⎯⎯▶B
Dog⎯⎯⎯⎯▶Animal
Dog is an Animal
```

### Interfaces for & Abstract classes
Interfaces and Abstract classes are represented by dotted line and rest of concrete classes are represented by solid lines.
It is defined  like <<InterfaceName>> or It it writted in itallic letters.
```
A-----B
```

```
 +-----------------+           +-----------------+          +-----------------+
|     User        |           |    << Product >>    |          |     Order       |
+-----------------+           +-----------------+          +-----------------+
| - id: int       |           | - id: int       |          | - id: int       |
| - name: String  |           | - name: String  |          | - date: Date    |
| - email: String |           | - price: double |          | - status: String|
| - password: String|         | - description: String |    +-----------------+
+-----------------+           +-----------------+          |+ addProduct()   |
|+ createOrder()  |           |+ checkAvailability() |     |+ removeProduct()|
+-----------------+           +-----------------+          +-----------------+
         |                             |                              |
         | 1                          | N                            | N
         |                             |                              |
         |                             |                              |
         |                             |                              |
         |                             |                              |
         |                             |                              |
         |                             |                              |
         |                          +-----------------+               |
         +------------------------> |   OrderItem     | <-------------+
                                    +-----------------+
                                    | - quantity: int |
                                    +-----------------+
                                    |+ calculateTotal()|
                                    +-----------------+
                                           |
                                           | N
                                           |
                                           |
                                       +-----------------+
                                       |     Payment     |
                                       +-----------------+
                                       | - id: int       |
                                       | - amount: double|
                                       | - date: Date    |
                                       | - status: String|
                                       +-----------------+
                                       |+ processPayment()|
                                       +-----------------+

```



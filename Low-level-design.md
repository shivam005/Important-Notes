# LLD

### Box will have to 3 section
1. Top: Class Name
2. Middle: Instances
3. Bottom: Methods

### Representation of access modifier
1. "+" public
2. "-" private
3. "#" protected

### Association
Association means how two things are related to each other like A can call B but B can not call A in case of unidirectional association.
#### Association or bidirectional association 
 Both can call each other
```
A----------B
A<-------->B
```
#### Unidirectional association 
A can call B but B can not call A.
```
A---->B
```
#### Multiplicity
Herein, we can also define one to many, many to many or many to one sort of relationship. 
We can also explicitly write the numbers as well. 
```
A-4-----1->B : four to one
A-1-----*->B : one to many
A-*-----*->B : many to many
A-*-----1->B : many to one
A-n-----1..2->B : n to (1 to 2)
```

```

 +-----------------+           +-----------------+          +-----------------+
|     User        |           |     Product     |          |     Order       |
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



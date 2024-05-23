# LLD

### Box will have to 3 section
1. Top: Class Name
2. Middle: Instances
3. Bottom: Methods

### Representation of access modifier
1. "+" public
2. "-" private
3. "#" protected

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

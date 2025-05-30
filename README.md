Actors: Admin, Merchant, Customer

Admin:
 - Manage Users (CRUD)
 - Manage Products (CRUD)
 - View Orders
 - View System Health (via Actuator)
 - Generate Reports

Merchant:
 - Add/Update Products
 - View Inventory
 - Fulfill Orders

Customer:
 - Register/Login
 - Browse Products
 - Place Orders
 - View Order History
 - Make Payments


+------------------+        +------------------+         +------------------+
|     User         |        |      Role        |         |   Product        |
+------------------+        +------------------+         +------------------+
| - id: Long       |        | - id: Long       |         | - id: Long       |
| - username: Str  |<--+    | - name: String   |         | - name: String   |
| - password: Str  |   |    +------------------+         | - price: Decimal |
| - email: String  |   +-------------------------------->| - stock: Integer |
| - enabled: Bool  |        (ManyToMany)                 | - category: Str  |
|                  |                                     | - seller: User   |
+------------------+                                     +------------------+

        ^
        |
        |
+------------------+
|   Customer       |
+------------------+
| - address        |
| - phone          |
+------------------+

        ^
        |
+------------------+
|   Merchant       |
+------------------+
| - companyName    |
| - gstNumber      |
+------------------+

+---------------------+        +--------------------+         +--------------------+
|      Order          |        |    OrderItem       |         |   Payment          |
+---------------------+        +--------------------+         +--------------------+
| - id: Long          |        | - id: Long         |         | - id: Long         |
| - orderDate: Date   |<----+  | - product: Product |         | - order: Order     |
| - status: Enum      |     |  | - quantity: Int    |         | - amount: Decimal  |
| - customer: User    |     |  +--------------------+         | - paymentMode: Str |
| - totalAmount: Dec  |     |       (ManyToOne)              | - paymentDate      |
+---------------------+     +-------------------------------> +--------------------+
                            (OneToMany)

+------------------+
|   Category       |
+------------------+
| - id: Long       |
| - name: String   |
+------------------+

+------------------+
| Inventory        |
+------------------+
| - id: Long       |
| - product: Product
| - stockLevel: Int
| - merchant: User
+------------------+

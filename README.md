# mongo-2

<h1>1. List All Products in the "Electronics" Category: </h1>

  
![image](https://github.com/user-attachments/assets/9ef8b3da-3e62-499e-bd9e-ad5747964e74)

```
aggregationAssignmentDB> db.products.aggregate([
...   { $match: { category: "Electronics" } }
... ])
...
[
  {
    _id: ObjectId('683838d2e2313d318658feaa'),
    name: 'Laptop Pro',
    category: 'Electronics',
    price: 1200,
    quantity: 10,
    tags: [ 'computer', 'portable', 'work' ],
    date_added: ISODate('2023-01-15T10:00:00.000Z'),
    supplier: { name: 'TechGlobe', location: 'USA' }
  },
  {
    _id: ObjectId('683838d2e2313d318658feab'),
    name: 'Wireless Mouse',
    category: 'Electronics',
    price: 25,
    quantity: 100,
    tags: [ 'peripheral', 'computer', 'wireless' ],
    date_added: ISODate('2023-02-01T11:30:00.000Z'),
    supplier: { name: 'GadgetPro', location: 'China' }
  },
  {
    _id: ObjectId('683838d2e2313d318658feac'),
    name: 'Mechanical Keyboard',
    category: 'Electronics',
    price: 75,
    quantity: 50,
    tags: [ 'peripheral', 'computer', 'mechanical' ],
    date_added: ISODate('2023-01-20T14:00:00.000Z'),
    supplier: { name: 'TechGlobe', location: 'USA' }
  },
  {
    _id: ObjectId('683838d2e2313d318658feb0'),
    name: 'Smartwatch',
    category: 'Electronics',
    price: 199,
    quantity: 25,
    tags: [ 'wearable', 'gadget', 'portable' ],
    date_added: ISODate('2023-04-01T12:00:00.000Z'),
    supplier: { name: 'GadgetPro', location: 'China' }
  },
  {
    _id: ObjectId('683838d2e2313d318658feb3'),
    name: 'Bluetooth Speaker',
    category: 'Electronics',
    price: 80,
    quantity: 60,
    tags: [ 'audio', 'portable', 'wireless' ],
    date_added: ISODate('2023-02-25T17:00:00.000Z'),
    supplier: { name: 'SoundWave', location: 'USA' }
  }
]
aggregationAssignmentDB>

```

-----


<h1>2. Count Products per Category: </h1>

![image](https://github.com/user-attachments/assets/70783489-bc7d-4cae-ad9d-ee471dc34348)


```
aggregationAssignmentDB> db.products.aggregate(
... [
... {$group : {_id: "$category" , count : {$sum:1}}}
... ]
... )
[
  { _id: 'Home Goods', count: 1 },
  { _id: 'Accessories', count: 1 },
  { _id: 'Sports', count: 1 },
  { _id: 'Electronics', count: 5 },
  { _id: 'Apparel', count: 2 }
]
aggregationAssignmentDB>
```
--------------------

<h1> 3. Product Names and Prices, Sorted by Price (Descending):   </h1>



![image](https://github.com/user-attachments/assets/a63ece03-f798-4f86-a380-d992444b8d76)

```
aggregationAssignmentDB> db.products.aggregate([
... {$project : {_id:0,name:1,price:1}},
... {$sort: {price:-1}}
... ])
[
  { name: 'Laptop Pro', price: 1200 },
  { name: 'Espresso Machine', price: 250 },
  { name: 'Smartwatch', price: 199 },
  { name: 'Bluetooth Speaker', price: 80 },
  { name: 'Mechanical Keyboard', price: 75 },
  { name: 'Denim Jeans', price: 60 },
  { name: 'Leather Wallet', price: 45 },
  { name: 'Yoga Mat', price: 30 },
  { name: 'Wireless Mouse', price: 25 },
  { name: 'Cotton T-Shirt', price: 20 }
]
aggregationAssignmentDB>
```

# Medium Difficulty
<h1> 1. Total Quantity of Products by Supplier: </h1>

![image](https://github.com/user-attachments/assets/ca0fad80-9075-482e-98a9-2486f81780d5)


```

aggregationAssignmentDB> db.products.aggregate([
... {$group : {_id : "$supplier.name" , totalquantity:{$sum:"$quantity"}}}
... ]
... )
[
  { _id: 'GadgetPro', totalquantity: 125 },
  { _id: 'HomeBest', totalquantity: 30 },
  { _id: 'FashionHub', totalquantity: 280 },
  { _id: 'TechGlobe', totalquantity: 60 },
  { _id: 'StyleCraft', totalquantity: 120 },
  { _id: 'ActiveLife', totalquantity: 90 },
  { _id: 'SoundWave', totalquantity: 60 }
]
aggregationAssignmentDB>
```

------------------------------------------------
<h1>2. Average Price of Products per Tag: </h1>
![image](https://github.com/user-attachments/assets/5ceed1c6-010c-44e6-a767-7bc67d616479)

```
aggregationAssignmentDB> db.products.aggregate([
...   { $unwind: "$tags" },
...   { $group: { _id: "$tags", averagePrice: { $avg: "$price" } } },
...   { $sort: { averagePrice: -1 } }
... ])
...
[
  { _id: 'work', averagePrice: 1200 },
  { _id: 'portable', averagePrice: 493 },
  { _id: 'computer', averagePrice: 433.3333333333333 },
  { _id: 'kitchen', averagePrice: 250 },
  { _id: 'appliance', averagePrice: 250 },
  { _id: 'coffee', averagePrice: 250 },
  { _id: 'wearable', averagePrice: 199 },
  { _id: 'gadget', averagePrice: 199 },
  { _id: 'audio', averagePrice: 80 },
  { _id: 'mechanical', averagePrice: 75 },
  { _id: 'denim', averagePrice: 60 },
  { _id: 'wireless', averagePrice: 52.5 },
  { _id: 'peripheral', averagePrice: 50 },
  { _id: 'leather', averagePrice: 45 },
  { _id: 'fashion', averagePrice: 45 },
  { _id: 'clothing', averagePrice: 40 },
  { _id: 'fitness', averagePrice: 30 },
  { _id: 'exercise', averagePrice: 30 },
  { _id: 'casual', averagePrice: 20 },
  { _id: 'cotton', averagePrice: 20 }
]
aggregationAssignmentDB>
```
-------------------------------------------------------

<h1>3. Products Added in February 2023: </h1>


![image](https://github.com/user-attachments/assets/47a72d2c-5637-4190-b423-35afbb6fc78b)





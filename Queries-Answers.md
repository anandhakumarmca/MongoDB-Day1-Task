# MongoDB Queries and Answers

## 1. Find all the information about each product
    ```javascript
    db.product.find()

## 2. Find the product price which is between 400 to 800
    ```javascript
    db.product.find({product_price: {$lt: 800, $gt: 400}})

## 3. Find the product price which is not between 400 to 600
    ```javascript
    db.product.find({$or: [{product_price: {$lt: 600}}, {product_price: {$gt: 400}}]})

## 4. List the four products which are greater than 500 in price
    ```javascript
    db.product.find({product_price: {$gt: 500}}).limit(4)

## 5. Find the product name and product material of each product
    ```javascript
    db.product.find().forEach(function(myDoc) {
    print(myDoc.product_name + " made up of " + myDoc.product_material);
    });

## 6. Find the product with a row id of 10
    ```javascript
    // Option 1
    db.product.find({id: {$eq: '10'}})

    // Option 2
    db.product.find({id: /10/})

    // Option 3
    db.product.find({id: '10'})

## 7. Find only the product name and product material
    ```javascript
    db.product.find({}, {product_name: 1, product_material: 1})

## 8. Find all products which contain the value "Soft" in product material
    ```javascript
    // Option 1
    db.product.find({product_material: {$eq: "Soft"}})

    // Option 2
    db.product.find({"product_material": /.*Soft.*/})

## 9. Find products which contain product color "indigo" and product price 492.00
    ```javascript
    db.product.find({$or: [{product_color: {$eq: 'indigo'}}, {product_price: {$eq: 492.00}}]})

## 10. Delete the products which have the same product price value
    ```javascript
    db.product.aggregate([
    {$group: {_id: '$product_price', count: {$sum: 1}}},
    {$match: {count: {$gt: 1}}}
    ]).forEach((e) => {
    db.product.deleteMany({product_price: e._id});
    })

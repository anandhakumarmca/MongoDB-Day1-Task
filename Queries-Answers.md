# MongoDB Queries and Answers

## 1. Find all the information about each product
    db.product.find()

![Alt Text]((https://github.com/anandhakumarmca/MongoDB-Day1-Task/blob/d38c66bc18045479f2576313cbe28a3382332d25/ScreenShorts/9.a.1'st-query-answer.png))

## 2. Find the product price which is between 400 to 800
    db.product.find({product_price: {$lt: 800, $gt: 400}})

## 3. Find the product price which is not between 400 to 600
    db.product.find({$or: [{product_price: {$lt: 600}}, {product_price: {$gt: 400}}]})

## 4. List the four products which are greater than 500 in price
    db.product.find({product_price: {$gt: 500}}).limit(4)

## 5. Find the product name and product material of each product
    db.product.find().forEach(function(myDoc) {print(myDoc.product_name + " made up of " + myDoc.product_material);});

## 6. Find the product with a row id of 10
    db.product.find({id: '10'})

## 7. Find only the product name and product material
    db.product.find({}, {product_name: 1, product_material: 1})

## 8. Find all products which contain the value "Soft" in product material
    db.product.find({product_material: {$eq: "Soft"}})

## 9. Find products which contain product color "indigo" and product price 492.00
    db.product.find({$or: [{product_color: {$eq: 'indigo'}}, {product_price: {$eq: 492.00}}]})

## 10. Delete the products which have the same product price value
    db.product.aggregate([{$group: {_id: '$product_price', count: {$sum: 1}}},
    {$match: {count: {$gt: 1}}}]).forEach((e) => 
    {db.product.deleteMany({product_price: e._id});})

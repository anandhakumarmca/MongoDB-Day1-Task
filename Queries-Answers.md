# MongoDB Queries and Answers

## 1. Find all the information about each product
    db.product.find()

![Query1](https://github.com/anandhakumarmca/MongoDB-Day1-Task/blob/d38c66bc18045479f2576313cbe28a3382332d25/ScreenShorts/9.a.1'st-query-answer.png)
![Query1](https://github.com/anandhakumarmca/MongoDB-Day1-Task/blob/88bd55a50dedad91367a9dbbae4229795446f84f/ScreenShorts/9.b.1'st-query-answer.png)


## 2. Find the product price which is between 400 to 800
    db.product.find({product_price: {$lt: 800, $gt: 400}})

![Query2](https://github.com/anandhakumarmca/MongoDB-Day1-Task/blob/88bd55a50dedad91367a9dbbae4229795446f84f/ScreenShorts/10.2'nd-query-answer.png)

## 3. Find the product price which is not between 400 to 600
    db.product.find({$or: [{product_price: {$lt: 600}}, {product_price: {$gt: 400}}]})

![Query3](https://github.com/anandhakumarmca/MongoDB-Day1-Task/blob/88bd55a50dedad91367a9dbbae4229795446f84f/ScreenShorts/11.3'rd-query-answer.png)

## 4. List the four products which are greater than 500 in price
    db.product.find({product_price: {$gt: 500}}).limit(4)
    
![Query4](https://github.com/anandhakumarmca/MongoDB-Day1-Task/blob/88bd55a50dedad91367a9dbbae4229795446f84f/ScreenShorts/12-4'th-query-answer.png)

## 5. Find the product name and product material of each product
    db.product.find().forEach(function(myDoc) {print(myDoc.product_name + " made up of " + myDoc.product_material);});
    
![Query5](https://github.com/anandhakumarmca/MongoDB-Day1-Task/blob/88bd55a50dedad91367a9dbbae4229795446f84f/ScreenShorts/13-5'th-query-answer.png)

## 6. Find the product with a row id of 10
    db.product.find({id: '10'})

![Query6](https://github.com/anandhakumarmca/MongoDB-Day1-Task/blob/88bd55a50dedad91367a9dbbae4229795446f84f/ScreenShorts/14.6'th-query-answer.png)

## 7. Find only the product name and product material
    db.product.find({}, {product_name: 1, product_material: 1})

![Query7](https://github.com/anandhakumarmca/MongoDB-Day1-Task/blob/88bd55a50dedad91367a9dbbae4229795446f84f/ScreenShorts/15.7'th-query-answer.png)

## 8. Find all products which contain the value "Soft" in product material
    db.product.find({product_material: {$eq: "Soft"}})
    
![Query8](https://github.com/anandhakumarmca/MongoDB-Day1-Task/blob/88bd55a50dedad91367a9dbbae4229795446f84f/ScreenShorts/16.8'th-query-answer.png)

## 9. Find products which contain product color "indigo" and product price 492.00
    db.product.find({$or: [{product_color: {$eq: 'indigo'}}, {product_price: {$eq: 492.00}}]})

![Query9](https://github.com/anandhakumarmca/MongoDB-Day1-Task/blob/88bd55a50dedad91367a9dbbae4229795446f84f/ScreenShorts/17.9'th-query-answer.png)

## 10. Delete the products which have the same product price value
    db.product.aggregate([{$group: {_id: '$product_price', count: {$sum: 1}}},
    {$match: {count: {$gt: 1}}}]).forEach((e) => 
    {db.product.deleteMany({product_price: e._id});})

## Before Delete Query DB status
![Query10](https://github.com/anandhakumarmca/MongoDB-Day1-Task/blob/88bd55a50dedad91367a9dbbae4229795446f84f/ScreenShorts/18.a.Before-delete-query.png)

## Delete Query 
![Query10](https://github.com/anandhakumarmca/MongoDB-Day1-Task/blob/88bd55a50dedad91367a9dbbae4229795446f84f/ScreenShorts/19.10'th-Delete-query.png)

## After Delete Query DB status
![Query10](https://github.com/anandhakumarmca/MongoDB-Day1-Task/blob/88bd55a50dedad91367a9dbbae4229795446f84f/ScreenShorts/20-After-delete-query.png)


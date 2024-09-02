# Restful ECommerce

A simple Node E-Commerce application for testing RESTful web services.

# Installation 
1. Clone the repo
1. Navigate into the restful-ecommerce root folder
1. Run npm install
1. Run npm start

APIs are exposed on http://localhost:3004

# API Documentation

## POST Orders

This API will allow adding new orders to the cart.

```bash
curl -X POST http://localhost:3004/addOrder \
-H "Content-Type: application/json" \
-d '{
    "user_id": "12345",
    "product_id": "98765",
    "product_name": "Cool Gadget",
    "product_amount": 100.00,
    "qty": 2,
    "tax_amt": 10.00,
    "total_amt": 220.00
}'
```

### Request Payload should be an array of Objects as below: 

``` JSON
[ { 
    "user_id": "1",
    "product_id": "1",
    "product_name": "iPhone",
    "product_amount": 500.00,
    "qty": 1,
    "tax_amt": 5.99,
    "total_amt": 505.99
},
{
    "user_id": "1",
    "product_id": "2",
    "product_name": "iPad",
    "product_amount": 699.00,
    "qty": 1,
    "tax_amt": 7.99,
    "total_amt": 706.99
},
{
    "user_id": "2",
    "product_id": "2",
    "product_name": "iPhone 15 PRO",
    "product_amount": 999.00,
    "qty": 2,
    "tax_amt": 9.99,
    "total_amt": 1088.99
},
{
    "user_id": "3",
    "product_id": "3",
    "product_name": "Samsung S24 Ultra",
    "product_amount": 4300.00,
    "qty": 1,
    "tax_amt": 5.99,
    "total_amt": 4305.99
}]
```

### Expected Response 
 
**Status Code : 201**

**Body** 

```JSON
{
    "message": "Orders added successfully!",
    "orders": [
        {
            "id": 1,
            "user_id": "1",
            "product_id": "1",
            "product_name": "iPhone",
            "product_amount": 500,
            "qty": 1,
            "tax_amt": 5.99,
            "total_amt": 505.99
        },
        {
            "id": 2,
            "user_id": "1",
            "product_id": "2",
            "product_name": "iPad",
            "product_amount": 699,
            "qty": 1,
            "tax_amt": 7.99,
            "total_amt": 706.99
        },
        {
            "id": 3,
            "user_id": "2",
            "product_id": "2",
            "product_name": "iPhone 15 PRO",
            "product_amount": 999,
            "qty": 2,
            "tax_amt": 9.99,
            "total_amt": 1088.99
        },
        {
            "id": 4,
            "user_id": "3",
            "product_id": "3",
            "product_name": "Samsung S24 Ultra",
            "product_amount": 4300,
            "qty": 1,
            "tax_amt": 5.99,
            "total_amt": 4305.99
        }
    ]
}
```

### Validations
1. Request Payload should be an array of Objects else 400 Bad request will be shown.
2. Request Payload should contain the following fields mandatorily: user_id, product_id, product_name, product_amount, qty, tax_amt, and total_amt else 400 Bad request will be shown.
3. "Id" field should be auto incremented when an order is added.
4. Currently, no check is added for duplicate orders.


## GET All Orders

This API will fetch all the orders available in the system.

```bash
curl -X GET http://localhost:3004/getAllOrders

```
### Expected Response 

This API will fetch all the available orders.
 
**Status Code : 200**

**Body** 
```JSON
{
    "message": "Orders fetched successfully!",
    "orders": [
        {
            "id": 1,
            "user_id": "1",
            "product_id": "1",
            "product_name": "iPhone",
            "product_amount": 500,
            "qty": 1,
            "tax_amt": 5.99,
            "total_amt": 505.99
        },
        {
            "id": 2,
            "user_id": "1",
            "product_id": "2",
            "product_name": "iPad",
            "product_amount": 699,
            "qty": 1,
            "tax_amt": 7.99,
            "total_amt": 706.99
        },
        {
            "id": 3,
            "user_id": "2",
            "product_id": "2",
            "product_name": "iPhone 15 PRO",
            "product_amount": 999,
            "qty": 2,
            "tax_amt": 9.99,
            "total_amt": 1088.99
        },
        {
            "id": 4,
            "user_id": "3",
            "product_id": "3",
            "product_name": "Samsung S24 Ultra",
            "product_amount": 4300,
            "qty": 1,
            "tax_amt": 5.99,
            "total_amt": 4305.99
        }
    ]
}
```
### Validations

1. Response should be a JSON object
1. Two fields should be fetched in the response,  `1. message` and `2. An array of Order Objects`
1. Order object should contain the following fields with values 
```JSON
     {
            "id": 1,
            "user_id": "1",
            "product_id": "1",
            "product_name": "iPhone",
            "product_amount": 500,
            "qty": 1,
            "tax_amt": 5.99,
            "total_amt": 505.99
        }
```
1. If no records are found following response should be displayed

*** Status Code - 404 ***

```JSON
{
    "message": "No Order found!!"
}

```

## GET Orders filtered on Order Id, User Id, Product Id

This API will fetch the orders as per the Query param - id, user_id or product_id 

### Fetch Orders by Order Id
```bash
curl -X GET "http://localhost:3004/getOrder?id=1

```
### Fetch Orders by User Id
```bash
curl -X GET "http://localhost:3004/getOrder?user_id=1

```
### Fetch Orders by Product Id
```bash
curl -X GET "http://localhost:3004/getOrder?product_id=1

```

### Fetch Orders by multiple query parameters
```bash
curl -X GET "http://localhost:3004/getOrder?id=1&product_id=1

```

Query Parameters
1. `id` 
1. `user_id`
1. `product_id`

### Expected Response

Data filtered accordingly to the query parameter supplied in request should be returned in the response as follows: 
**Status Code : 200**

**Body** 
```JSON
{
    "message": "Order found!!",
    "orders": [
        {
            "id": 1,
            "user_id": "1",
            "product_id": "1",
            "product_name": "iPhone",
            "product_amount": 500,
            "qty": 1,
            "tax_amt": 5.99,
            "total_amt": 505.99
        }
    ]
}
```

### Validations
1. Fetch the records based on `id (order id)`, `product_id`, `user_id` individually or clubbing all the three query parameters with AND condition
1. When no records are available for the query parameter, the following response should be displayed: 

**Status Code : 404**

**Response Body**
```JSON
{
    "message": "No Order found with the given parameters!"
}

```

## PUT - Update Order details

This API will update the order details

```bash
curl -X PUT http://localhost:3004/updateOrder/1 \
-H "Content-Type: application/json" \
-d '{
    "user_id": "12345",
    "product_id": "98765",
    "product_name": "Updated Gadget",
    "product_amount": 120.00,
    "qty": 3,
    "tax_amt": 12.00,
    "total_amt": 372.00
}'
```

### Request Payload should be an Object

```JSON
{
    "user_id": "1",
    "product_id": "5",
    "product_name": "Samsung Galaxy S24 Ultra",
    "product_amount": 14337.00,
    "qty": 5,
    "tax_amt": 90.00,
    "total_amt": 14427.00
    }

```

### Expected Response 

**Status Code : 200**

**Body** 


```JSON
{
  "message": "Order updated successfully!",
  "order": {
    "order_id": 1,
    "user_id": "12345",
    "product_id": "98765",
    "product_name": "Updated Gadget",
    "product_amount": 120.00,
    "qty": 3,
    "tax_amt": 12.00,
    "total_amt": 372.00
  }
}
```
### Validations
1. Request Payload should contain the following fields mandatorily: user_id, product_id, product_name, product_amount, qty, tax_amt, and total_amt else 400 Bad request will be shown.
2. If Order Id does not exists, then status code 404 will be shown with message "Order not found!" in the response.

```JSON
{
"message": "Order not found!" 
}
```

3. Currently, no check is added for duplicate orders.

## PATCH - Update Specific Order detail

This API will allow updating specific order detail

```bash
curl -X PATCH http://localhost:3004/partialUpdateOrder/1 \
-H "Content-Type: application/json" \
-d '{"product_name": "iPhone 15 Pro Max"}'
```

### Request Payload should be an Object

Any specific detail of the order can be updated using this API

```JSON
{
 "product_name": "iPhone 15 pro max"
}
```

### Expected Response

**Status Code : 200**

**Body** 

```JSON
{
  "message": "Order updated successfully!",
  "order": {
    "id": 1,
    "user_id": "1",
    "product_id": "98765",
    "product_name": "iPhone 15 Pro Max",
    "product_amount": 120.00,
    "qty": 3,
    "tax_amt": 12.00,
    "total_amt": 372.00
  }
}
```

### Validations
1. Any valid field of the Order can be updated using this API.
2. If Order Id does not exists, then status code 404 will be shown with following message in the response
```JSON 
{
    "message": "Order not found!"
}
```

## DELETE Order

This API will delete the order of the given Order Id

```bash
curl -X DELETE http://localhost:3004/deleteOrder/1
```
### Expected Response

**Status Code : 204**

**No Response Body will be generated**


### Validations
1. Any valid Order id can be deleted.
2. If Order Id does not exists, then status code 404 will be shown with following message in the response
```JSON 
{
    "message": "Order not found!"
}
```

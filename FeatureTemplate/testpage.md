### POST /api/v1/cart/add
Добавление товара в корзину
#### Запрос:


```
 
POST /api/v1/cart/add HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "productid": "m1125",
  "quantity": 1
}

```
                
#### Ответ:

``` 
HTTP/1.1 201 Created
Content-Type: application/json

{
  "uid": "C001",
  "items": [
    {
      "uid": "CI001",
      "productid": "m1125",
      "quantity": 1
    }
  ],
  "total": 75999.0
}

```
                
### POST /api/v1/cart/create
Создание корзины
|Запрос|Ответ|
|------|-----|
|```                
POST /api/v1/cart/create HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "userid": 123
}
```|```
HTTP/1.1 201 Created
Content-Type: application/json

{
  "uid": "C001",
  "items": [],
  "total": 0.0
}

```|


#### Запрос:

```                
POST /api/v1/cart/create HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "userid": 123
}
```
               
#### Ответ:

```
HTTP/1.1 201 Created
Content-Type: application/json

{
  "uid": "C001",
  "items": [],
  "total": 0.0
}

```
                
### Просмотр корзины
#### Запрос:

```
 
GET /api/v1/cart/view HTTP/1.1
Host: example.com
Accept: application/json
                    
GET /api/v1/cart/view HTTP/1.1
Host: example.com
Accept: application/json

                
#### Ответ:
http
```
15
 
HTTP/1.1 200 OK
Content-Type: application/json

{
  "uid": "C001",
  "items": [
    {
      "uid": "CI001",
      "productid": "m1125",
      "quantity": 1
    }
  ],
  "total": 75999.0
}
```

                
### Изменение количества товаров
#### Запрос:

```
PATCH /api/v1/cart/items HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "uid": "CI001",
  "quantity": 2
}
                    
#### Ответ:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "uid": "C001",
  "items": [
    {
      "uid": "CI001",
      "productid": "m1125",
      "quantity": 2
    }
  ],
  "total": 151998.0
}
                
#### Удаление товара
Запрос:

```
DELETE /api/v1/cart/items HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "uid": "CI001"
}
                
#### Ответ:

```
 
HTTP/1.1 204 No Content
             
### Создание заказа из корзины
#### Запрос:

```
POST /api/v1/orders/create HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "userid": 123,
  "paymentmethod": "online",
  "deliverymethod": "delivery",
  "contactname": "Дмитрий",
  "contactphone": "+7-812-509-65-00",
  "email": "example@example.com",
  "adress": "321"
}
                    
```               
### Ответ:

```
HTTP/1.1 201 Created
Content-Type: application/json

{
  "uid": "O001",
  "userid": 123,
  "creationdate": 1749999076,
  "orderstate": "delivered",
  "totalprice": 75999.0,
  "paymentmethod": "online",
  "deliverymethod": "delivery",
  "contactname": "Дмитрий",
  "contactphone": "+7-812-509-65-00",
  "email": "example@example.com",
  "adress": "321",
  "products": ["m1125"]
}
```
                
### Ввод и проверка данных клиента
#### Запрос:

```
POST /api/v1/checkout/validate HTTP/1.1
Host: example.com
Content-Type: application/json
{
  "name": "Дмитрий",
  "phone": "+7-812-509-65-00",
  "email": "example@example.com"
}
               
#### Ответ:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "valid": true
}
               
### Проверка данных пользователя
#### Запрос:

```
POST /api/v1/users/validate HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "userid": 123
}
```                    
                
#### Ответ:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "valid": true
}
```
                
### Запрос данных пользователя
#### Запрос:

```
POST /api/v1/users HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "userid": 123
}
```                    
                
#### Ответ:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "uid": "U001",
  "userid": 123,
  "name": "Дмитрий",
  "phone": "+7-812-509-65-00",
  "email": "example@example.com"
}
```
               
### Обновление статуса заказа

#### Запрос:

```
PATCH /api/v1/orders/update HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "uid": "O001",
  "orderstate": "shipped"
}
```              
#### Ответ:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "uid": "O001",
  "orderstate": "shipped"
}
```
                
### Изменение данных пользователя

#### Запрос:

```
 
PUT /api/v1/users/123 HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "Дмитрий",
  "email": "new.email@example.com"
}
```
                
#### Ответ:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "uid": "U001",
  "userid": 123,
  "name": "Дмитрий",
  "email": "new.email@example.com"
}
```
                
### Оплата заказа
#### Запрос:

```

POST /api/v1/checkout/payment HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "orderid": "O001",
  "amount": 75999.0,
  "paymentmethod": "online"
}
                    
POST /api/v1/checkout/payment HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "orderid": "O001",
  "amount": 75999.0,
  "paymentmethod": "online"
}
```
                
### Ответ:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "status": "paid",
  "orderid": "O001"
}
```
                
### Подтверждение оплаты
#### Запрос:

```
POST /api/v1/payments HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "orderid": "O001",
  "paymentid": "P001"
}
```               
#### Ответ:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "status": "confirmed",
  "paymentid": "P001"
}
```
                
### Обновление корзины
#### Запрос

```
PATCH /api/v1/cart/update HTTP/1.1
Host: example.com
Content-Type: application/json
{
  "uid": "C001",
  "items": [
    {
      "uid": "CI001",
      "quantity": 3
    }
  ]
}
```
              
#### Ответ:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "uid": "C001",
  "total": 227997.0
}
```


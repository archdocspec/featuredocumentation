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
                
### Создание корзины
#### Запрос:
http
```
 
POST /api/v1/cart/create HTTP/1.1
Host: example.com
Content-Type: application/json

{}
                    
POST /api/v1/cart/create HTTP/1.1
Host: example.com
Content-Type: application/json

{}

                
Ответ:
http
```
 
HTTP/1.1 201 Created
Content-Type: application/json

{
  "uid": "C001",
  "items": [],
  "total": 0.0
}
                    
HTTP/1.1 201 Created
Content-Type: application/json

{
  "uid": "C001",
  "items": [],
  "total": 0.0
}

                
Просмотр корзины
Запрос:
http
```
 
GET /api/v1/cart/view HTTP/1.1
Host: example.com
Accept: application/json
                    
GET /api/v1/cart/view HTTP/1.1
Host: example.com
Accept: application/json

                
Ответ:
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

                
Изменение количества товаров
Запрос:
http
```
 
PATCH /api/v1/cart/items HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "uid": "CI001",
  "quantity": 2
}
                    
PATCH /api/v1/cart/items HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "uid": "CI001",
  "quantity": 2
}

                
Ответ:
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
      "quantity": 2
    }
  ],
  "total": 151998.0
}
                    
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

                
Удаление товара
Запрос:
http
```
7
8
 
DELETE /api/v1/cart/items HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "uid": "CI001"
}
                    
DELETE /api/v1/cart/items HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "uid": "CI001"
}

                
Ответ:
http
```
 
HTTP/1.1 204 No Content
                    
HTTP/1.1 204 No Content

                
Создание заказа из корзины
Запрос:
http
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

                
Ответ:
http
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

                
Ввод и проверка данных клиента
Запрос:
http
```
10
 
POST /api/v1/checkout/validate HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "Дмитрий",
  "phone": "+7-812-509-65-00",
  "email": "example@example.com"
}
                    
POST /api/v1/checkout/validate HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "Дмитрий",
  "phone": "+7-812-509-65-00",
  "email": "example@example.com"
}

                
Ответ:
http
```
7
 
HTTP/1.1 200 OK
Content-Type: application/json

{
  "valid": true
}
                    
HTTP/1.1 200 OK
Content-Type: application/json

{
  "valid": true
}

                
Проверка данных пользователя
Запрос:
http
```
7
8
 
POST /api/v1/users/validate HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "userid": 123
}
                    
POST /api/v1/users/validate HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "userid": 123
}

                
Ответ:
http
```
7
 
HTTP/1.1 200 OK
Content-Type: application/json

{
  "valid": true
}
                    
HTTP/1.1 200 OK
Content-Type: application/json

{
  "valid": true
}

                
Запрос данных пользователя
Запрос:
http
```
7
8
 
POST /api/v1/users HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "userid": 123
}
                    
POST /api/v1/users HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "userid": 123
}

                
Ответ:
http
```
10
11
 
HTTP/1.1 200 OK
Content-Type: application/json

{
  "uid": "U001",
  "userid": 123,
  "name": "Дмитрий",
  "phone": "+7-812-509-65-00",
  "email": "example@example.com"
}
                    
HTTP/1.1 200 OK
Content-Type: application/json

{
  "uid": "U001",
  "userid": 123,
  "name": "Дмитрий",
  "phone": "+7-812-509-65-00",
  "email": "example@example.com"
}

                
Обновление статуса заказа
Запрос:
http
```
 
PATCH /api/v1/orders/update HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "uid": "O001",
  "orderstate": "shipped"
}
                    
PATCH /api/v1/orders/update HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "uid": "O001",
  "orderstate": "shipped"
}

                
Ответ:
http
```
7
8
 
HTTP/1.1 200 OK
Content-Type: application/json

{
  "uid": "O001",
  "orderstate": "shipped"
}
                    
HTTP/1.1 200 OK
Content-Type: application/json

{
  "uid": "O001",
  "orderstate": "shipped"
}

                
Изменение данных пользователя
Запрос:
http
```
 
PUT /api/v1/users/123 HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "Дмитрий",
  "email": "new.email@example.com"
}
                    
PUT /api/v1/users/123 HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "Дмитрий",
  "email": "new.email@example.com"
}

                
Ответ:
http
```
10
 
HTTP/1.1 200 OK
Content-Type: application/json

{
  "uid": "U001",
  "userid": 123,
  "name": "Дмитрий",
  "email": "new.email@example.com"
}
                    
HTTP/1.1 200 OK
Content-Type: application/json

{
  "uid": "U001",
  "userid": 123,
  "name": "Дмитрий",
  "email": "new.email@example.com"
}

                
Оплата заказа
Запрос:
http
```
10
 
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

                
Ответ:
http
```
7
8
 
HTTP/1.1 200 OK
Content-Type: application/json

{
  "status": "paid",
  "orderid": "O001"
}
                    
HTTP/1.1 200 OK
Content-Type: application/json

{
  "status": "paid",
  "orderid": "O001"
}

                
Подтверждение оплаты
Запрос:
http
```
 
POST /api/v1/payments HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "orderid": "O001",
  "paymentid": "P001"
}
                    
POST /api/v1/payments HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "orderid": "O001",
  "paymentid": "P001"
}

                
Ответ:
http
```
7
8
 
HTTP/1.1 200 OK
Content-Type: application/json

{
  "status": "confirmed",
  "paymentid": "P001"
}
                    
HTTP/1.1 200 OK
Content-Type: application/json

{
  "status": "confirmed",
  "paymentid": "P001"
}

                
Обновление корзины
Запрос:
http
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

                
Ответ:
http
```
7
8
 
HTTP/1.1 200 OK
Content-Type: application/json

{
  "uid": "C001",
  "total": 227997.0
}
                    
HTTP/1.1 200 OK
Content-Type: application/json

{
  "uid": "C001",
  "total": 227997.0
}

                
Теперь текст структурирован и оформлен в соответствии с вашими требованиями.


## ОПИСАНИЕ МЕТОДОВ API

### POST /api/v1/cart/add
Добавление товара в корзину

#### Запрос

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>

```
POST /api/v1/cart/add HTTP/1.1
Host: example.com
Content-Type: application/json
{
  "productid": "m1125",
  "quantity": 1
}
```
</details>

#### Ответ

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
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
</details>
  
### POST /api/v1/cart/create
Создание корзины

#### Запрос

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
```                
POST /api/v1/cart/create HTTP/1.1
Host: example.com
Content-Type: application/json
{
  "userid": 123
}
```
</details>

#### Ответ

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
```
HTTP/1.1 201 Created
Content-Type: application/json
{
  "uid": "C001",
  "items": [],
  "total": 0.0
}
```
</details>
                
### GET /api/v1/cart/view
Просмотр корзины

#### Запрос

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
```
GET /api/v1/cart/view HTTP/1.1
Host: example.com
Accept: application/json
```
</details>

#### Ответ

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
```
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
</details>
   
### PATCH /api/v1/cart/items
Изменение количества товаров

#### Запрос

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
```
PATCH /api/v1/cart/items HTTP/1.1
Host: example.com
Content-Type: application/json
{
  "uid": "CI001",
  "quantity": 2
}
```
</details>
                   
#### Ответ

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
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
```
</details>
                 
### Удаление товара

#### Запрос

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
```
DELETE /api/v1/cart/items HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "uid": "CI001"
}
```
</details>
                 
#### Ответ

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
```
HTTP/1.1 204 No Content
```
</details>
           
### Создание заказа из корзины

#### Запрос

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
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
</details>
     
#### Ответ

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
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
</details>
                 
### POST /api/v1/checkout/validate
Ввод и проверка данных клиента

#### Запрос

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
```
POST /api/v1/checkout/validate HTTP/1.1
Host: example.com
Content-Type: application/json
{
  "name": "Дмитрий",
  "phone": "+7-812-509-65-00",
  "email": "example@example.com"
}
```
</details>
                
#### Ответ

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
```
HTTP/1.1 200 OK
Content-Type: application/json
{
  "valid": true
}
```
</details>
         
### POST /api/v1/users/validate
Проверка данных пользователя

#### Запрос

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>

```
POST /api/v1/users/validate HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "userid": 123
}
```                    
                
#### Ответ

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
```
HTTP/1.1 200 OK
Content-Type: application/json
{
  "valid": true
}
```
</details>
                 
### POST /api/v1/users
Запрос данных пользователя

#### Запрос

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
```
POST /api/v1/users HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "userid": 123
}
```                    
</details>
                 
#### Ответ

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
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
</details>
                
### PATCH /api/v1/orders/update
Обновление статуса заказа

#### Запрос

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
```
PATCH /api/v1/orders/update HTTP/1.1
Host: example.com
Content-Type: application/json
{
  "uid": "O001",
  "orderstate": "shipped"
}
```
</details>
              
#### Ответ

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
```
HTTP/1.1 200 OK
Content-Type: application/json
{
  "uid": "O001",
  "orderstate": "shipped"
}
```
</details>
                 
### PUT /api/v1/users/userid
Изменение данных пользователя

#### Запрос

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
```
PUT /api/v1/users/123 HTTP/1.1
Host: example.com
Content-Type: application/json
{
  "name": "Дмитрий",
  "email": "new.email@example.com"
}
```
</details>
                 
#### Ответ

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
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
</details>
                 
### POST /api/v1/checkout/payment
Оплата заказа

#### Запрос

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
```
POST /api/v1/checkout/payment HTTP/1.1
Host: example.com
Content-Type: application/json
{
  "orderid": "O001",
  "amount": 75999.0,
  "paymentmethod": "online"
}
```
</details>
                 
### Ответ

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
```
HTTP/1.1 200 OK
Content-Type: application/json
{
  "status": "paid",
  "orderid": "O001"
}
```
</details>
                 
### POST /api/v1/payments
Подтверждение оплаты

#### Запрос

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
```
POST /api/v1/payments HTTP/1.1
Host: example.com
Content-Type: application/json
{
  "orderid": "O001",
  "paymentid": "P001"
}
```
</details>
             
#### Ответ

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "status": "confirmed",
  "paymentid": "P001"
}
```
</details>
                 
### PATCH /api/v1/cart/update
Обновление корзины

#### Запрос

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
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
</details>
        
#### Ответ

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>summary>
```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "uid": "C001",
  "total": 227997.0
}
```
</details>
 

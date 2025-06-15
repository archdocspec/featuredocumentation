# Компоненты и вызовы

== Раздел для описания компонентов, задействованных в создании решения: учет, изменения, использование и т.п. ==

>[!CAUTION]
>Принял решение об упрощении системы. Схлопнул все кроме 2 сервисы бека в CMS. Аналогично - с БД. Надо это здесь указать.
>Причина - это все же на самом деле - образец заполнения ШАБЛОНА, а не полноценное проектирование.
БД
    note right cmdb
         
    end note
Компоненты:


## Компонент диаг

```
@startuml

package "User Interface" {
    component "User GUI" as ugui {
        
  }
  portout HTTP
}

package "Backend" {
  [guiGateway]
  [guiGateway] -- REST_API
  [cmsService] - REST_API
  database "PostgreSQL" {
    [cmdb] -- REST_API
  }
  
}
ugui - HTTP
HTTP -- [guiGateway] : REST API
@enduml
```

## Общий список Компонентов решения
Схлопнуть

| № | Компонент   | Наименование         | Описание                                                      | Технологии    |
|---|-------------|----------------------|-------------------------------------------------------------------------|---------------------------|
| 1 | User GUI    | usergui   | Пользовательский интерфейс. Витрина товаров. Личный кабинет пользователя. Логин процесс. Корзина покупок | React / Vue.js |
| 3 |  | User Interface Gateway  | UGuiGate | Backend Сервис для обеспечения работы пользовательского интерфейса  | Python / Flask |
| 5 | Сервис управления пользователями | userService        | Управляет данными пользователей, включая их профили и настройки. | Python / Flask |
| 6 | Сервис управления контентом (CMS) | cmsService         | Управляет сделками, корзиной, расчетом стоимости и другими связанными функциями.Для упрощения примера  Содержит Платежный шлюз userService + logisticService = cms| Python / Flask |
| 7 | База данных CMS| orderDBService     | Хранит и управляет данными о заказах, их статусах и связанных сделках. Для упрощения примера orderDB + productDB База данных товаров + userDB База данных пользователе + cartDB = cmsdb | PostgreSQL     |



## Интегр взаимод

| Название вызова | Инициатор | Метод | URL | Получатель |
|------------------------------------------|------------------|--------|---------------------------------------|------------------|
| Добавление товара в корзину | User GUI | POST | `/api/v1/cart/add` | guiGateway |
| Создание корзины | cmsService | POST | `/api/v1/cart/create` | cmdb |
| Просмотр корзины | User GUI | GET | `/api/v1/cart/view` | guiGateway |
| Изменение количества товаров | User GUI | PATCH | `/api/v1/cart/items` | guiGateway |
| Удаление товара | User GUI | DELETE | `/api/v1/cart/items` | guiGateway |
| Создание заказа из корзины | User GUI | POST | `/api/v1/orders/create` | guiGateway |
| Создание заказа | guiGateway | POST | `/api/v1/orders/create` | cmsService |
| Ввод и проверка данных клиента | User GUI | POST | `/api/v1/checkout/validate` | guiGateway |
| Проверка данных пользователя | guiGateway | POST | `/api/v1/users/validate` | cmsService |
| Запрос данных пользователя | cmsService | POST | `/api/v1/users` | cmdb |
| Обновление статуса заказа | cmsService | PATCH | `/api/v1/orders/update` | cmdb |
| Изменение данных пользователя | User GUI | PUT | `/api/v1/users` | guiGateway |
| Оплата заказа | User GUI | POST | `/api/v1/checkout/payment` | guiGateway |
| Подтверждение оплаты | guiGateway | POST | `/api/v1/payments` | cmsService |
| Обновление корзины | cmsService | PATCH | `/api/v1/cart/update` | cmdb |


## Список Вызовов

### Добавление товара в корзину
#### Запрос:

POST /api/v1/cart/add 
```
HTTP/1.1


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

                
Ответ:

http
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

### Создание корзины
Запрос:

http

 
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
9

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

 
GET /api/v1/cart/view HTTP/1.1
Host: example.com
Accept: application/json
                    
GET /api/v1/cart/view HTTP/1.1
Host: example.com
Accept: application/json

                
Ответ:

http
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

### Изменение количества товаров
Запрос:

http

9
 
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
HTTP/1.1 204 No Content

HTTP/1.1 204 No Content

Создание заказа из корзины
Запрос:

http

 
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
16
17
18

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

9
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
9
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

9
 
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

9
 
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
9
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

9
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

9
 
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




### Шаблон списка

Образец заполнения согласно указанному набору компонентов в описании сценариев и бизнес-логике:

* [Сценарии](https://github.com/NonameX11/TestPetDocumentationProject/blob/main/Feature%20Template/4%20-%20%D0%A1%D1%86%D0%B5%D0%BD%D0%B0%D1%80%D0%B8%D0%B8.md)

* [Шаблон описания отдельного Сценария](https://github.com/NonameX11/TestPetDocumentationProject/blob/main/Feature%20Template/4.1%20-%20%D0%A8%D0%B0%D0%B1%D0%BB%D0%BE%D0%BD%20%D0%BE%D0%BF%D0%B8%D1%81%D0%B0%D0%BD%D0%B8%D1%8F%20%D0%BE%D1%82%D0%B4%D0%B5%D0%BB%D1%8C%D0%BD%D0%BE%D0%B3%D0%BE%20%D0%A1%D1%86%D0%B5%D0%BD%D0%B0%D1%80%D0%B8%D1%8F.md)


| Имя компонента | Описание | Использование | Статус изменения | Расположение |
|:-----------|:-----------|:-----------|:-----------|:-----------|
| Frontend | UI Решения | Пользовательский UI для ввода и вывода обработанных данных | добавляется форма ui | ms-frontend-host|
| Backend | Data Processing Module | Backend-система валидации и обработки входящих данных согласно бизнес-логике | Добавляется Endpoint для вызовов UI | ms-frontend-host|
| DB | PostgreSQL БД | База данных решения, размещенная в ЦОД | Не изменяется| ЦОД datavault-13 |

### Бланк таблицы списка

<details>
  <summary>Шаблон таблицы</summary>         

| Имя компонента | Описание | Использование | Статус изменения | Расположение |
|:-----------|:-----------|:-----------|:-----------|:-----------|
| Название | Описание назначения | Как, где и зачем применяется | Создается, Изменяется, Не изменяется, Удаляется | Указать сервер/микросервис и т.п. |

</details>


### Запрос Вызова


#### Заголовок (Header) Запроса

> Подробнее : https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/

| Параметр | Описание | Значение |
|:-------------:|:-------------:|:-------------:|
| Host | Хост (сервер) вызова | my-web-server |
| Authorization | Тип авторизации | Basic |
| Date | Дата и время вызова | Wed Jul 4 15:31:53 2024 |
| Connection | Соединение | Keep-alive |
| Content-type | Тип контента | application/json |
| Content-Length | размер сообщения | 304 |


#### Тело (Body) запроса

| Атрибут | Формат | Обязательность	| Описание	| Пример |
| ------------- |:-------------:|:-------------:|:-------------:|:-------------:|
| requestId	| UUID	| Да | Уникальный ID Запроса	| 2Afas124-123 |
| timestamp	| Date-time | Да | Дата, Время и часовой пояс клиента в запросе	| 2020-09-03T11:42:54.190+02.00 |
| userId	| string | Да | Уникальный Id клиента	| 123456789 | 
| inputText | string | Да | Введенный пользователем текст| some random text 915214 | 


#### Пример Сообщения Запроса

```
POST/system/api/v1/apps/dataproc/inputdata/ 
Host : my-web-server
Authorization : Basic
Date : Wed Jul 4 15:31:53 2024
Connection : Keep-alive
Content-type : application/json
Content-Length : 304
	{
 		requestId: Afas124-123
		timestamp: 2020-09-03T11:42:54.190+02.00
		userId: 123456789
		inputText:  some random text 915214
	}
```


### Ответ на Вызов


#### Заголовок (Header) Ответа

> Подробнее : https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/

| Параметр | Описание | Значение |
| ------------- |:-------------:|:-------------:|
| HTTP | Код ответа | 200 (OK) |
| Host | Хост (сервер) ответа | libnhttpd |
| Authorization | Тип авторизации | application/json |
| Date | Дата и время ответа | Wed Jul 4 15:31:53 2012 | 
| Connection | Соединение | Keep-Alive |
| Content-Type | Тип содержимого ответа | application/json | 
| Content-Length | Размер сообщения | 151 |

	
### Тело (Body) ответа

| Атрибут	| Формат | Обязательность	| Описание	| Пример |
| ------------- |:-------------:|:-------------:|:-------------:|:-------------:|
| responseId	| UUID	| Да	| Уникальный ID Ответа	| Afas124-123 | 
| timestamp	| Date-time	| Да	| Дата, Время и часовой пояс клиента в ответе на запрос	| 2020-09-03T11:42:54.190+02.00 | 
| userId	| string	| Да	| Уникальный Id пользователя | 123456789 | 



#### Пример Сообщения Ответа

```
HTTP: 200 (OK)
Host: libnhttpd
Authorization: application/json
Date : Wed Jul 4 15:31:53 2012
Connection : Keep-Alive
Content-Type: application/json 
Content-Length: 151

	{
 		responseId	: Afas124-123523
		timestamp: 2020-09-03T11:42:54.190+03.00
		userId: 123456789
	}
```

### Шаблон описания вызова

Пояснение назначения в заголовке

REST method + url


 == НУЖНО попытаться добавить сваггер ==
 
> Описание добавления https://github.com/peter-evans/swagger-github-pages

#### Описание и назначение вызова


| Имя | Назначение | Тип вызова | Метод | url |
| ------------- |:-------------:|:-------------:|:-------------:|:-------------:|
| Отправка данных в обработку | Отправка введенных пользователем данных с frontend формы на backend. <br>Для валидации и сохранения для последующей обработке согласно бизнес логике | REST API | POST  | /system/api/v1/apps/dataproc/inputdata/ |

#### Запрос Вызова


#### Заголовок (Header) Запроса

> Подробнее : https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/

| Параметр | Описание | Значение |
| ------------- |:-------------:|:-------------:|
| Название параметра | Описание параметра | Значение параметра |


### Тело (Body) запроса


| Атрибут	| Формат | Обязательность	| Описание	| Пример |
| ------------- |:-------------:|:-------------:|:-------------:|:-------------:|
| Имя атрибута | Формат атрибута| Обязательность атрибута | Описание атрибута | Пример атрибута | 


#### Шаблон описания примера сообщения запроса

```
HTTP Method/Endpoint url
Header Запроса
	{
 		Body запроса
	}
```


### Ответ на Вызов


#### Заголовок (Header) Ответа

> Подробнее : https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/

| Параметр | Описание | Значение |
| ------------- |:-------------:|:-------------:|
| Название параметра | Описание параметра | Значение параметра |
	
### Тело (Body) ответа

| Атрибут	| Формат | Обязательность	| Описание	| Пример |
| ------------- |:-------------:|:-------------:|:-------------:|:-------------:|
| Имя атрибута | Формат атрибута| Обязательность атрибута | Описание атрибута | Пример атрибута | 

#### Пример Сообщения Ответа

```
Header parameters

	{
 		Body parameters
	}
```

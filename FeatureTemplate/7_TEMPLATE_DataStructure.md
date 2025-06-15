# ШАБЛОН ОПИСАНИЯ СТРУКТУРЫ БД В РАМКАХ СЦЕНАРИЯ И РЕШЕНИЯ

## БД

### UML Class Diagram

![ClassDiag](https://github.com/archdocspec/featuredocumentation/blob/main/FeatureTemplate/Assets/Database/s1classv2.png)

<details>
  <summary>PlantUML Code</summary>
  
```
@startuml
class product {
    uid : varchar : "P001"
    productid : varchar : "m1125"
    name : varchar : "Смартфон Apple iPhone 13 128GB"
    price : numeric : 75999.0
    prodparams : array : [{productparameters}]
    creationdate : timestamp : 1749999076
    updated  : timestamp : 1749999076
}

class productparameters {
    uid : varchar : "A001"
    screenSize : string : "6.1\"/2532x1170"
    cores : int : 6
    power : string : "20 Вт"
    ram : string : "6 ГБ"
    rom : string : "128 ГБ"
    mainCamera : string : "64/2"
    updated  : timestamp : 1749999076
}

class cart {
    uid : varchar : "C001"
    items :  : [{cartitem}]
    total : numeric : 279978.0
    updated: timestamp : 1749999076
}

class cartitem {
    uid : varchar : "CI001"
    productid : varchar : product.productid
    quantity : int : 1
    updated: timestamp : 1749999076
}

class order {
    uid : varchar : "O001"
    userid : int : 123
    creationdate : timestamp : 1749999076
    updated  : timestamp : 1749999076
    orderstate: string : "delivered"
    totalprice : numeric : 279978.0
    paymentmethod : string : "online"
    deliverymethod : string : "delivery"
    contactname : varchar : user.name
    contactphone : string : user.phone
    email : string : user.email
    adress : string : address.adressid
    products:  : [{product.productid}]
}

class user {
    uid : varchar : "U001"
    userid : int : 123
    name : varchar : "Дмитрий"
    phone : string : "+7-812-509-65-00"
    email : string : "example@example.com"
    address :  :  [{adressid}]
    creationdate : timestamp : 1749999076
    updated : timestamp : 1749999076
}

class address {
    uid : varchar : "A001"
    adressid : string : 321
    street : string : "г. Санкт-Петербург, Невский пр, 21"
    creationdate : timestamp : 1749999076
}

' Связи между классами
product "1" -- "0..*" productparameters : Имеет >
cart "1" -- "0..*" cartitem : Содержит >
cartitem "1" -- "1" product : Отсылает к >
order "1" -- "1" user : Принадлежит >
order "1" -- "0..*" product : Содержит >
order "1" -- "1" address : Использует >
user "1" -- "0..*" address : Имеет >
@enduml

```

</details>

## Описание таблиц БД

### Таблица: `product`
Данные товаров (продуктов) магазина

| Поле | Тип данных | Размерность | Пример значения |
|---------------|------------|-------------|--------------------------------------------|
| uid* | varchar | 10 | “P001” |
| productid | varchar | 10 | “m1125” |
| name | varchar | 255 | “Смартфон Apple iPhone 13 128GB” |
| price | numeric | 10,2 | 75999.00 |
| price | array | нет | [{productparameters}] |
| creationdate | timestamp | - | 1749999076 |
| updated | timestamp | - | 1749999076 |

### Таблица: `productparameters`
Хранение параметров продукта

| Поле | Тип данных | Размерность | Пример значения |
|---------------|------------|-------------|--------------------------------------------|
| uid* | varchar | 10 | “A001” |
| productid | varchar | 10 | “m1125” |
| screenSize | string | 50 | “6.1”/2532x1170" |
| cores | int | - | 6 |
| power | string | 20 | “20 Вт” |
| ram | string | 10 | “6 ГБ” |
| rom | string | 10 | “128 ГБ” |
| mainCamera | string | 10 | “64/2” |
| updated | timestamp | - | 1749999076 |

### Таблица: `cart`
Хранение параметров корзины
| Поле | Тип данных | Размерность | Пример значения |
|---------------|------------|-------------|--------------------------------------------|
| uid* | varchar | 10 | “C001” |
| items | array | нет | [{cartitem}]|
| total | numeric | 10,2 | 279978.00 |
| updated | timestamp | - | 1749999076 |

### Таблица: `cartitem`

| Поле | Тип данных | Размерность | Пример значения |
|---------------|------------|-------------|--------------------------------------------|
| uid* | varchar | 10 | “CI001” |
| cartuid | varchar | 10 | “C001” |
| productid | varchar | 10 | “m1125” |
| quantity | int | - | 1 |
| updated | timestamp | - | 1749999076 |

### Таблица: `order`
Данные заказов

| Поле | Тип данных | Размерность | Пример значения |
|---------------|------------|-------------|--------------------------------------------|
| uid* | varchar | 10 | “O001” |
| userid | int | - | 123 |
| creationdate | timestamp | - | 1749999076 |
| updated | timestamp | - | 1749999076 |
| orderstate | string | 20 | “delivered” |
| totalprice | numeric | 10,2 | 279978.00 |
| paymentmethod | string | 20 | “online” |
| deliverymethod | string | 20 | “delivery” |
| contactname | varchar | 50 | “Дмитрий” |
| contactphone | string | 20 | “+7-812-509-65-00” |
| email | string | 50 | “example@example.com” |
| adressid | string | 10 | “321” |
| products | array | - | [{product.productid}] |

### Таблица: `user`
Данные пользователей

| Поле | Тип данных | Размерность | Пример значения |
|---------------|------------|-------------|--------------------------------------------|
| uid* | varchar | 10 | “U001” |
| userid | int | - | 123 |
| name | varchar | 50 | “Дмитрий” |
| phone | string | 20 | “+7-812-509-65-00” |
| email | string | 50 | “example@example.com” |
| address | array | -  | [{adressid}] |
| creationdate | timestamp | - | 1749999076 |
| updated | timestamp | - | 1749999076 |

### Таблица: `address`
Данные пользовательских адресов

| Поле | Тип данных | Размерность | Пример значения |
|---------------|------------|-------------|--------------------------------------------|
| uid* | varchar | 10 | “A001” |
| adressid | string | 10 | “321” |
| street | string | 255 | “г. Санкт-Петербург, Невский пр, 21” |
| creationdate | timestamp | - | 1749999076 |

### Связи между таблицами
`product` (1) – (0…*) `productparameters`
`cart` (1) – (0…*) `cartitem`
`cartitem` (1) – (1) `product`
`order` (1) – (1) `user`
`order` (1) – (0…*) `product`
`order` (1) – (1) `address`
`user` (1) – (0…*) `address`

# ШАБЛОН ОПИСАНИЯ СТРУКТУРЫ БД В РАМКАХ СЦЕНАРИЯ И РЕШЕНИЯ

>[!TIP]
>Этот раздел предназначен для описания сущностей данных, их структуры и связей в рамках спроектированного [в предыдущем разделе](https://github.com/archdocspec/featuredocumentation/blob/main/FeatureTemplate/5_TEMPLATE_Scenario_INTEGRATION.md) интеграционного сценария.

## Диаграмма Классов базы данных Решения

>[!TIP]
>Для описания структуры данных часто нужна выгрузка таблиц БД, показывающая их содержимое.
>
>Если выгрузку сделать невозможно ИЛИ структура данных не существует и только планируется к созданию, то можно описать данные при помощи [UML-диаграммы классов](https://ru.wikipedia.org/wiki/%D0%94%D0%B8%D0%B0%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B0_%D0%BA%D0%BB%D0%B0%D1%81%D1%81%D0%BE%D0%B2)

>**Шаблон Диаграммы классов**

![ClassDiagramExample](https://github.com/archdocspec/featuredocumentation/blob/main/FeatureTemplate/Assets/Database/classexmpl.png)

>**Образец Диаграммы классов для описания сущностей решения**

![ClassDiagramExample](https://github.com/archdocspec/featuredocumentation/blob/main/FeatureTemplate/Assets/Database/s1classv2.png)

<details>
  <summary>PlantUML Код для рендера образца Диаграммы классов</summary>
  
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

____

## Описание структур данных
>[!TIP]
>Далее рекомендуется детализировать описание таблиц БД в формате, представленном ниже.

>**Шаблон таблицы для структур данных в таблицах БД**

| Поле | Тип данных | Размерность | Пример значения | Описание |
|------|------------|-------------|-----------------|-----------|
| *Имя поля* | *Тип хранимых данных в поле* | *Допустимая размерность поля* | *Пример значения поля* | *Текстовое описание назначения поля* |

>**Образцы заполнения таблиц структур данных**

### Таблица: `product`
Данные товаров (продуктов) магазина

| Поле | Тип данных | Размерность | Пример значения | Описание |
|------------------|------------|-------------|-----------|----------|
| uid* | varchar | 10 | “P001” | Уникальный идентификатор продукта |
| productid | varchar | 10 | “m1125” | Идентификатор продукта в системе |
| name | varchar | 255 | “Смартфон Apple iPhone 13 128GB” | Название продукта |
| price | numeric | 10,2 | 75999.00 | Цена продукта |
| price | array | нет | [{productparameters}] | Массив параметров продукта |
| creationdate | timestamp | - | 1749999076 | Дата и время создания записи |
| updated | timestamp | - | 1749999076 | Дата и время последнего обновления записи |



### Таблица: `productparameters`
Хранение параметров продукта

| Поле | Тип данных | Размерность | Пример значения | Описание |
|---------------|------------|-------------|------------------------|-------------|
| uid* | varchar | 10 | “A001” | Уникальный идентификатор продукта |
| productid | varchar | 10 | “m1125” | Идентификатор продукта в системе |
| screenSize | string | 50 | “6.1”/2532x1170" | Размер экрана устройства |
| cores | int | - | 6 | Количество ядер процессора |
| power | string | 20 | “20 Вт” | Мощность зарядного устройства |
| ram | string | 10 | “6 ГБ” | Объем оперативной памяти |
| rom | string | 10 | “128 ГБ” | Объем встроенной памяти |
| mainCamera | string | 10 | “64/2” | Основная камера (разрешение) |
| updated | timestamp | - | 1749999076 | Дата и время последнего обновления записи |



### Таблица: `cart`

Хранение параметров корзины

| Поле | Тип данных | Размерность | Пример значения | Описание |
|---------------|------------|-------------|------------------------|-------|
| uid* | varchar | 10 | “C001” | Уникальный идентификатор корзины |
| items | array | нет | [{cartitem}] | Массив элементов в корзине |
| total | numeric | 10,2 | 279978.00 | Общая стоимость товаров в корзине |
| updated | timestamp | - | 1749999076 | Дата и время последнего обновления корзины |

### Таблица: `cartitem`

| Поле | Тип данных | Размерность | Пример значения | Описание |
|---------------|------------|-------------|------------------------|------------------------|
| uid* | varchar | 10 | “CI001” | Уникальный идентификатор элемента корзины |
| cartuid | varchar | 10 | “C001” | Идентификатор корзины, к которой принадлежит элемент |
| productid | varchar | 10 | “m1125” | Идентификатор продукта |
| quantity | int | - | 1 | Количество данного продукта в корзине |
| updated | timestamp | - | 1749999076 | Дата и время последнего обновления элемента корзины |

### Таблица: `order`

Данные заказов

| Поле | Тип данных | Размерность | Пример значения | Описание |
|------------------|------------|--------|---------|----------------|
| uid* | varchar | 10 | “O001” | Уникальный идентификатор заказа |
| userid | int | - | 123 | Идентификатор пользователя, сделавшего заказ |
| creationdate | timestamp | - | 1749999076 | Дата и время создания заказа |
| updated | timestamp | - | 1749999076 | Дата и время последнего обновления заказа |
| orderstate | string | 20 | “delivered” | Текущий статус заказа |
| totalprice | numeric | 10,2 | 279978.00 | Общая стоимость заказа |
| paymentmethod | string | 20 | “online” | Метод оплаты за заказ |
| deliverymethod | string | 20 | “delivery” | Метод доставки заказа |
| contactname | varchar | 50 | “Дмитрий” | Имя контактного лица |
| contactphone | string | 20 | “+7-812-509-65-00” | Телефон контактного лица |
| email | string | 50 | “example@example.com” | Электронная почта контактного лица |
| adressid | string | 10 | “321” | Идентификатор адреса доставки |
| products | array | - | [{product.productid}] | Массив идентификаторов продуктов в заказе |

### Таблица: `user`
Данные пользователей



### Таблица: `address`
Данные пользовательских адресов

| Поле | Тип данных | Размерность | Пример значения | Описание |
|------------------|--------------|-----------------|-----------|-----------|
| uid* | varchar | 10 | “A001” | Уникальный идентификатор адреса |
| adressid | string | 10 | “321” | Идентификатор адреса в системе |
| street | string | 255 | “г. Санкт-Петербург, Невский пр, 21” | Полный адрес, включая город и улицу |
| creationdate | timestamp | - | 1749999076 | Дата и время создания записи адреса |

### Связи между таблицами

`product` (1) – (0…*) `productparameters`
`cart` (1) – (0…*) `cartitem`
`cartitem` (1) – (1) `product`
`order` (1) – (1) `user`
`order` (1) – (0…*) `product`
`order` (1) – (1) `address`
`user` (1) – (0…*) `address`

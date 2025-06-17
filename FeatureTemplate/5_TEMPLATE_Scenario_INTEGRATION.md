#  Шаблон для описания интеграционного взаимодействия по выведенному сценарию и проектирования API

>[!NOTE]
>Этот раздел шаблона предназаначен для проработки выведенного сценария в детализированное **описание интеграционного взаимодействия компонентов решения при помощи API**
>
>Такой формат ведения документации обеспечивает бесшовный переход от **Бизнес-требований** к **Системным требованиям**

>[!TIP]
> Раздел шаблона состоит из следующих важных для сценария элементов
> 1. Описание используемых компонентов решения.
> 2. Описание интеграционного взаимодействия по API.
> 3. Спецификация используемого API.

_____

## Компоненты решения

>[!TIP]
> Для проектирования интеграционного взаимодействия важно определить список компонентов для решения поставленной задачи в рамках сценария.
>
>Компонент - это любая отдельная часть сложной системы, которая выполняет определенную функцию или предоставляет определенный сервис.

### Список компонентов

>**Шаблон списка компонентов в виде таблицы**

| № | Компонент   | Наименование         | Описание | Технологии |
|---|-------------|----------------------|----------|---------------|
| *Укажите порядковый номер* | *Укажите название компонента* | *Укажите системное имя (алиас) компонента* | *Опишите назначение и особенности компонента* | *Кратко укажите технический стек компонента и/или дайте ссылку на документ с ним* |

>**Образец заполнения списка компонентов**

>[!TIP]
> Образец заполнен на основе выведенного в [предыдущем разделе](https://github.com/archdocspec/featuredocumentation/blob/main/FeatureTemplate/4.1_TEMPLATE_USE_CASE_Scenario_Description.md) сценария.

| № | Компонент   | Наименование         | Описание                                                      | Технологии    |
|---|-------------|----------------------|-------------------------------------------------------------------------|---------------------------|
| 1 | User GUI    | usergui   | Пользовательский интерфейс. Витрина товаров. Личный кабинет пользователя. Логин процесс. Корзина покупок | React / Vue.js |
| 2 |  User Interface Gateway  | UGuiGate | Backend Сервис для обеспечения работы пользовательского интерфейса  | Python / Flask |
| 3 | Сервис управления пользователями | userService        | Управляет данными пользователей, включая их профили и настройки. | Python / Flask |
| 4 | Сервис управления контентом (CMS) | cmsService         | Управляет сделками, корзиной, расчетом стоимости и другими связанными функциями.Для упрощения примера  Содержит Платежный шлюз userService + logisticService = cms| Python / Flask |
| 5 | База данных CMS| orderDBService     | Хранит и управляет данными о заказах, их статусах и связанных сделках. Для упрощения примера orderDB + productDB База данных товаров + userDB База данных пользователе + cartDB = cmsdb | PostgreSQL |


### Диаграмма компонентов

>[!TIP]
>Далее рекомендуется создать и приложить [UML](https://ru.wikipedia.org/wiki/UML) - диаграмму компонентов для визуализации списка выше.


>**Шаблон Диаграммы компонентов c кодом для рендера PlantUML**

![Component Diagram](https://github.com/archdocspec/featuredocumentation/blob/main/FeatureTemplate/Assets/S1/comptemplate1.png)

>**Образец Диаграммы компонентов на основе ранее созданного списка**

![UMLCompDiag](https://github.com/archdocspec/featuredocumentation/blob/main/FeatureTemplate/Assets/Components/s1compv1.png)

>**Код Диаграммы компонентов для рендера PlantUML**

<details>
    <summary><br>PlantUML код Диаграммы</br></summary>

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
 
</details>

________

## Интеграционное взаимодействие компонентов в рамках сценария

>[!TIP]
> Эта часть шаблона предназначена для описания интеграционного взаимодействия компонентов решения при помощи API.
>
>Основной её элемент - диаграмма последовательности, на которой показано взаимодействие выбранных компонентов по API, в рамках вариантов использования (Use Case) выведенного сценария/

>[!NOTE]
>Для примера описания API выбран REST API как наиболее популярный и наглядный.


### Sequence Diagram


>**Шаблон диаграммы последовательности с описанием интеграционного сценария на основе REST API**

![UMLSequence_Diagram](https://github.com/archdocspec/featuredocumentation/blob/main/FeatureTemplate/Assets/S1/restseqexample.png)

<details>
    <summary><br>PlantUML код для рендера этого шаблона диаграммы</br></summary>

```

@startuml
testinganuragactor Users #Yellow
activate frontend #LightBlue
activate APIGateway #LightCoral
activate Lambda #LightSalmonUsers -> frontend : interact
frontend -> APIGateway : GET /user
APIGateway-> Lambda : getUsers()
Lambda -> DynamoDB : fetch user from\n users table
DynamoDB -[#Gray]-> Lambda: Return
APIGateway <-[#Gray]- Lambda : return
APIGateway -[#Gray]-> frontend : return the response
frontend -[#Gray]-> Users : Response
@enduml

```
</details>

>**Цветовой код для обозначения компонентов**

https://plantuml.com/ru/color

> [!TIP]
> Использование цветового кода помогает качественно улучшить читаемость диаграммы, добавив при этом больше информативности.

Ниже предлагается один из возможных вариантов такого кода:

![ЦВЕТОВОЙ КОД](https://github.com/archdocspec/featuredocumentation/blob/main/FeatureTemplate/Assets/UC/COLORCODE.png)

| Код | Назначение |
|:------:|:------:|
| Application | Приложение |
| Business | Бизнес-элемент |
| Implementation| Внедрение (Применение) |
| Motivation | Мотивация (Действия) |
| Physical | Физический объект или процесс (инфраструктуры) |
| Strategy | Стратегия |
| Technology | Технология |

<details>
    <summary><br>PlantUML код для рендера этого справочника цветов</br></summary>

```
@startuml
skinparam minClassWidth 125
skinparam nodesep 10
skinparam ranksep 10

rectangle Application    #Application
rectangle Business       #Business
rectangle Implementation #Implementation
rectangle Motivation     #Motivation
rectangle Physical       #Physical
rectangle Strategy       #Strategy
rectangle Technology     #Technology
@enduml

```
</details>

>**Образец диаграммы последовательности с описанием интеграционного сценария на основе REST API**

>[!TIP]
>Эта интеграция спроектирована на основе всех предыдущих образцов материалов

![UMLSequence_Diagram](https://github.com/archdocspec/featuredocumentation/blob/main/FeatureTemplate/Assets/API/s1apiv5.png)

<details>
    <summary><br>PlantUML код Диаграммы</br></summary>

```

@startuml

skinparam MaxMessageSize 150
actor "Пользователь" as user #Business
box frontend #Application
    participant "User GUI" as ugui #TECHNOLOGY
end box
box backend #Application
    participant "guiGateway" as ugate #TECHNOLOGY
    participant "cmsService" as cms #TECHNOLOGY
    database "cmsDB" as cmdb
    participant "cmsService" as cms #TECHNOLOGY
end box
actor "Доставка" as del #PHYSICAL

ref over user: UC1 Просмотр товаров

 == UC2.1 Добавление товара в корзину  ==
    autonumber 1
    
    
    user -> ugui : Добавление выбранных товаров в корзину
    activate ugui
    activate ugate
    ugui -> ugate : POST /api/v1/cart/add{productid, quantity}
    
    activate cms
    ugate -> cms : POST /api/v1/cart/add
    alt Если это первый товар в корзине для пользователя
        activate cmdb
        cms -> cmdb : POST /api/v1/cart/create{uid} Создать корзину
        cmdb -> cms : 200 OK
        deactivate cmdb
    end
    cms -> cmdb : POST /api/v1/cart/add{productid, quantity}
    cmdb -> cms : 200 OK
    cms -> ugate : 200 ОК товары добавлены
    deactivate cms
    ugate -> ugui : 200 OK (Корзина обновлена)
    deactivate ugate
    
    


 == UC2.2 Действия с параметрами списка товаров в корзине  ==
    
    user -> ugui : Переход в корзину
    
    ugui -> ugate : GET /api/v1/cart/view{uid}
    activate ugate
    activate cms
    ugate -> cms : GET /api/v1/cart/view{uid}
    activate cmdb
    cms -> cmdb : GET /api/v1/cart/view{uid}
    cmdb -> cms : 200 OK (Данные корзины)
    deactivate cmdb
    cms -> ugate : 200 OK (Данные о товарах в корзине)
    deactivate cms
    ugate -> ugui : 200 OK (Данные корзины)
    deactivate ugate
    user -> ugui : Выбор чекбоксами нужных товаров для оформления заказа
    alt Просмотр карточки добавленного товара
        user -> ugui : Нажатие на карточку товара
        ref over ugui: UC1.4 Просмотр карточки товара
        ref over ugui : UC2.1 Шаг 10 Переход в корзину
    end
    alt Изменение количества товаров
        user -> ugui : Изменение количества товаров
        ugui -> ugate : PATCH /api/v1/cart/items/{itemId}
        activate ugate
        ugate -> cms : PATCH /api/v1/cart/items/{itemId}
        activate cms
        cms -> cmdb : PATCH /api/v1/cart/items/{itemId}{quantity}
        cmdb -> cms : 200 OK (Товар обновлен)
        deactivate cmdb
        cms -> ugate : 200 OK (Товар обновлен)
        deactivate cms
        ugate -> ugui : 200 OK (Товар обновлен)
        deactivate ugate
    end
    alt Удаление товара
        user -> ugui : Удаление товара
        ugui -> ugate : DELETE /api/v1/cart/items/{itemId}
        activate ugate
        ugate -> cms : DELETE /api/v1/cart/items/{itemId}
        activate cms
        cms -> cmdb : DELETE /api/v1/cart/items/{itemId}
        cmdb -> cms : 200 OK (Товар удален)
        deactivate cmdb
        cms -> ugate : 200 OK (Товар удален)
        deactivate cms
        ugate -> ugui : 200 OK (Товар удален)
        deactivate ugate
    end
    alt Выбор всех товаров
        user -> ugui : Выбор всех товаров
        ugui -> ugate : PATCH /api/v1/cart/items/{Все itemId}
        activate ugate
        ugate -> cms : PATCH /api/v1/cart/items/{Все itemId}
        activate cms
        cms -> cmdb : PATCH /api/v1/cart/items/{Все itemId}
        cmdb -> cms : 200 OK (Все товары в корзине)
        deactivate cmdb
        cms -> ugate : 200 OK (Все товары в корзине)
        deactivate cms
        ugate -> ugui : 200 OK (Все товары в корзине)
        deactivate ugate
    end
    
    

== UC2 Заказ товара ==
    
    
    user -> ugui : Проверка итоговой суммы и нажатие кнопки Оформления заказа
    
    ugui -> ugate : POST /api/v1/orders/create{itemId Из корзины}
    activate ugate
    ugate -> ugate : Сопоставление itemId и productid
    ugate -> cms : POST /api/v1/orders/create{данные пользователя + данные товаров}
    activate cms
    cms -> cmdb : POST /api/v1/orders/create
    cmdb -> cms : 200 OK (Заказ создан)
    deactivate cmdb
    cms -> ugate : 200 OK (Заказ создан)
    ugate -> ugui : 200 OK (Заказ создан)
    deactivate ugate
    cms -> cmdb : PATCH /api/v1/cart/update/{id} Убрать из корзины заказанные товары
    deactivate cms
    

 == UC2.3 Ввод и проверка данных клиента  ==
    
    
    user -> ugui : Ввод и проверка данных клиента
    activate ugate
    ugui -> ugate : POST /api/v1/checkout/validate{userid}

    ugate -> cms : POST /api/v1/users/validate{userid}
    activate cms
    cms -> cmdb : POST /api/v1/users/{userid} // Запрос данных пользователя
    cmdb -> cms : 200 OK (Данные пользователя)
    deactivate cmdb
    cms -> cmdb : PATCH /api/v1/orders/update{orderid, orderstate} // Обновить статус заказа
    cmdb -> cms  : 200 OK (стаус обновлен)
    deactivate cmdb
    deactivate cms
    deactivate ugate
    
    alt Изменение данных пользователя
        user -> ugui : Изменение данных пользователя
        ugui -> ugate : PUT /api/v1/users/{userId}
        activate ugate
        ugate -> cms : PUT /api/v1/users/{userId}{name, phone, email}
        activate cms
        cms -> cmdb : PUT /api/v1/users/{userId}
        cmdb -> cms : 200 OK (Данные обновлены)
        deactivate cmdb
        cms -> ugate : 200 OK (Данные обновлены)
        deactivate cms
        ugate -> ugui : 200 OK (Результат обновления)
        deactivate ugate
    else
        ugate -> ugui : 200 OK (Результат проверки)
        deactivate ugate
    end
    
 == UC2.4 Оплата заказа  ==
    
    activate ugui
    user -> ugui : Оплата заказа
    activate ugate
    ugui -> ugate : POST /api/v1/checkout/payment
    activate cms
    ugate -> cms : POST /api/v1/payments{orderId, paymentMethod}
    ref over cms : Работа платежного шлюза
    ref over user : Подтверждение оплаты на стороне пользователя (sms)
    cms -> ugate : 200 OK (Подтверждение оплаты)
    ugate -> ugui : 200 OK (Подтверждение оформления заказа)
    cms -> cmdb : PATCH /api/v1/orders/update{orderid, orderstate} // Обновить статус заказа
    cmdb -> cms  : 200 OK (стаус обновлен)
    deactivate cmdb
    cms  -> ugate : PATCH /api/v1/orders/update{orderid, orderstate} // Заказ доставляется
    deactivate cms
    ugate -> ugui : Экран подтверждения выполнения заказа
    deactivate ugate

 ==  UC2.5 Доставка  == 
    activate cms
    cms -> del : Передать заказ
    deactivate cms
    activate del
    del -> user : Доставить товар
    deactivate del
    activate cms
    del -> cms : Подтвердить доставку
    cms -> cmdb : PATCH /api/v1/orders/update{orderid, orderstate} // Обновить статус заказа
    cmdb -> cms  : 200 OK (стаус обновлен)
    deactivate cmdb
    cms  -> ugate : PATCH /api/v1/orders/update{orderid, orderstate} // Заказ завершен
    deactivate cms
    activate ugate
    ugate -> ugui : Экран завершения заказа
    deactivate ugui
    deactivate ugate
    
autonumber stop
@enduml

```
 
</details>

_____

### Список интеграционных взаимодействий компонентов

>[!TIP]
>Здесь надо зафиксировать спроектированные выше методы API и соответствующие им компоненты в качестве инициаторов и получателей.
>
>В целях создания удобночитаемого справочника.
>
>Для этого подойдет шаблон таблицы ниже.

>**Шаблон списка интеграционных взаимодействий компонентов**

| Название вызова | Инициатор | Метод | URL | Получатель |
|-----------------------------|----------|------|--------------------|------------|
| *Имя API-вызова* | *Компонент, от которого идет вызов получателю* | *API-метод вызова* | *URL-адрес или какой то другой адрес в зависимости от типа API* | *Компонент, получающий вызов инициатора* |


>**Образец заполнения шаблона списка интеграционных взаимодействий компонентов**

| Название вызова | Инициатор | Метод | URL | Получатель |
|-----------------------------|----------|------|--------------------|------------|
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


_____


## ОПИСАНИЕ МЕТОДОВ API

>[!TIP]
>
> Этот раздел шаблона предназначен для описания спецификации используемого API.
>
>В идеале, тут надо разместить [Swagger](https://editor.swagger.io/), который является оптимальным для REST API.

>**Шаблон описания REST API**

Шаблон вызовов вместе с пояснением сути и назначения REST API можно найти в связанной статье [Что такое REST API](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/What_is_REST_API.md).

>**Образец описания спецификации API**

### POST /api/v1/cart/add
Добавление товара в корзину

#### Запрос

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>
  

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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>
  
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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>
  
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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>
  
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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>
  
```
GET /api/v1/cart/view HTTP/1.1
Host: example.com
Accept: application/json
```
  
</details>

#### Ответ

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>
  
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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>
  
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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>
  
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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>
  
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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>

```
HTTP/1.1 204 No Content
```

</details>
           
### Создание заказа из корзины

#### Запрос

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>

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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>

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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>

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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>

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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>

```
POST /api/v1/users/validate HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "userid": 123
}
```
            
</details>
       
#### Ответ

<details>
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>

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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>

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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>

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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>

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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>

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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>

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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>

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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>

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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>

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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>

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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>

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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>

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
  <summary><br>РАЗВЕРНУТЬ ОПИСАНИЕ</br></summary>

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "uid": "C001",
  "total": 227997.0
}
```

</details>
 
____

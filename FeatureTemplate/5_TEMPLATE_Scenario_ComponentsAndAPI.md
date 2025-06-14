# Компоненты и вызовы

== Раздел для описания компонентов, задействованных в создании решения: учет, изменения, использование и т.п. ==

TEST

| Назначение (описание) | Вызов | Ответ | Пример запроса | Пример ответа |

|-----------------------------------------------------------|--------------------------------|--------------------------------|----------------------------------------------------|---------------------------------------------------|

| Получение списка товаров для отображения в пользовательском интерфейсе. | GET /products | 200 OK (список товаров) | `GET /products` | `[{ “id”: 1, “name”: “Товар 1”, “price”: 100 }, { “id”: 2, “name”: “Товар 2”, “price”: 200 }]` |

| Добавление выбранных товаров в корзину. | POST /cart/add | 200 OK | `POST /cart/add`
`{ “productId”: 1, “quantity”: 2 }` | `{“message”: “Товар добавлен в корзину”}` |

| Получение данных о товарах в корзине. | GET /cart | 200 OK (данные о корзине) | `GET /cart` | `[{ “productId”: 1, “quantity”: 2 }, { “productId”: 2, “quantity”: 1 }]` |

| Обновление количества товаров в корзине. | PATCH /cart/update | 200 OK | `PATCH /cart/update`
`{ “productId”: 1, “quantity”: 3 }` | `{“message”: “Количество товара обновлено”}` |

| Удаление товара из корзины. | DELETE /cart/remove | 200 OK | `DELETE /cart/remove`
`{ “productId”: 1 }` | `{“message”: “Товар удален из корзины”}` |

| Выбор всех товаров в корзине. | POST /cart/select-all | 200 OK | `POST /cart/select-all` | `{“message”: “Все товары выбраны”}` |

| Получение итоговой суммы заказа в корзине. | GET /cart/total | 200 OK (итоговая сумма) | `GET /cart/total` | `{“total”: 400}` |

| Создание нового заказа и запись его в историю. | POST /order | 200 OK | `POST /order`
`{ “cartId”: 1, “userId”: 123 }` | `{“message”: “Заказ создан”, “orderId”: 456}` |

| Валидация данных клиента перед оформлением заказа. | POST /order/validate | 200 OK | `POST /order/validate`
`{ “userId”: 123 }` | `{“valid”: true}` |

| Обработка платежа за заказ. | POST /api/payment | 200 OK (подтверждение оплаты) | `POST /api/payment`
`{ “orderId”: 456, “amount”: 400 }` | `{“message”: “Оплата подтверждена”}` |

| Запуск процесса доставки заказа. | POST /order/dispatch | 200 OK | `POST /order/dispatch`
`{ “orderId”: 456 }` | `{“message”: “Заказ передан на доставку”}` |

| Получение информации о статусе доставки заказа. | GET /order/receive | 200 OK | `GET /order/receive` | `{“status”: “Доставлено”}` |

## Общий список Компонентов решения
| № | Компонент   | Наименование         | Описание                                                      | Технологии    |
|---|-------------|----------------------|-------------------------------------------------------------------------|---------------------------|
| 1 | User GUI    | usergui   | Пользовательский интерфейс. Витрина товаров. Личный кабинет пользователя. Логин процесс. Корзина покупок | React / Vue.js |
| 3 | База данных товаров | productDBService   | Хранит и управляет данными о товарах, их характеристиках и категориях. | PostgreSQL     |
| 4 | База данных пользователей | userDBService      | Хранит и управляет данными о пользователях, их профилями и аутентификацией. | PostgreSQL     |
| 5 | Сервис управления пользователями | userService        | Управляет данными пользователей, включая их профили и настройки. | Python / Flask |
| 6 | Сервис управления контентом (CMS) | cmsService         | Управляет сделками, корзиной, расчетом стоимости и другими связанными функциями. Содержит Платежный шлюз| Python / Flask |
| 7 | База данных заказов | orderDBService     | Хранит и управляет данными о заказах, их статусах и связанных сделках. | PostgreSQL     |
| 8 | Сервис логистики | logisticsService    | Управляет процессами доставки, отслеживания заказов и взаимодействия с курьерскими службами. | Python / Flask |

API draft

```
@startuml




actor "Пользователь" as User #Application
note over User  : Кафку и редис убрать, т.к. это ШАБЛОН, надо проще
participant "User GUI" as userGui #Business
participant "Сервис управления пользователями" as userService #Business
database "База данных пользователей" as userDBService
participant "Сервис управления контентом (CMS)" as cmsService #Business

note over cmsService : В него встроен фин. модуль

database "База данных заказов" as orderDBService
database "База данных товаров" as productDBService

participant "Сервис логистики и Доставка" as logisticsService #Business
note over logisticsService : БД Логистики убрать, достаточно бд заказов

group UC1 Просмотр товаров
    User -> userGui : GET /products
    activate userGui
    userGui -> cmsService  : GET /api/products
    activate cmsService 
    cmsService  -> productDBService : GET /products
    activate productDBService
    productDBService -> cmsService  : 200 OK (список товаров)
    deactivate productDBService
    cmsService  -> userGui : 200 OK (список товаров)
    deactivate cmsService 
end

group UC2.1 Добавление товара в корзину
    autonumber 1
    User -> userGui : POST /cart/add
    userGui -> cmsService : POST /api/cart/add
    activate cmsService
    cmsService -> cmsService  : Кэширование информации о корзине
    cmsService -> cmsService : SEND /cart/update
    deactivate cmsService
    User -> userGui : GET /cart
    activate userGui
end

group UC2.2 Действия с параметрами списка товаров
    alt Варианты действий с параметрами списка товаров
        User -> userGui : GET /cart
        userGui -> cmsService  : GET /api/cart
    else
        User -> userGui : PATCH /cart/update
        userGui -> cmsService : PATCH /api/cart/update
        cmsService -> cmsService : SEND /cart/update
    else
        User -> userGui : DELETE /cart/remove
        userGui -> cmsService : DELETE /api/cart/remove
        cmsService -> cmsService : SEND /cart/remove
    else
        User -> userGui : POST /cart/select-all
        userGui -> cmsService : POST /api/cart/select-all
        cmsService -> cmsService : SEND /cart/select-all
    end
end

group UC2 Заказ товара
    User -> userGui : GET /cart/total
    User -> userGui : POST /order
    userGui -> cmsService : rpc(New order)
    cmsService -> userService : записать заказ в историю
    cmsService -> orderDBService : CREATE /order
    cmsService -> cmsService : SEND /order/create
end

group UC2.3 Ввод и проверка данных клиента
    User -> userGui : POST /order/validate
    userGui -> userService : POST /api/user/validate
    userService -> userDBService : GET /user
end

group UC2.4 Оплата заказа
    User -> userGui : POST /order/pay
    userGui -> cmsService : POST /api/payment
    cmsService -> userGui : 200 OK (подтверждение оплаты)
    userGui -> User : Подтверждение оформления заказа
end

group UC2.5 Доставка
    deactivate userGui
    userGui -> logisticsService : POST /order/dispatch
    logisticsService -> orderDBService : UPDATE /order/status
    logisticsService -> cmsService : SEND /order/dispatch
end

autonumber stop
logisticsService -X User : GET /order/receive
deactivate logisticsService

@enduml
```

# ПРЕДЫДУЩЕЕ
__________________

Список компонентов, задействованных в создании решения.

* Service Frontend
* Service Backend
* db Database

### Комп диаграмма

5.1.	Схема
 = Компоненты + DFD с RPS на стрелках + Легенда
https://plantuml.com/ru/component-diagram

образцы

https://real-world-plantuml.com/?type=component

https://www.google.com/search?q=plantuml+component+examples&sca_esv=976475d81eac0872&ei=JEgRZ-SAIsm4wPAPkrf_SA&ved=0ahUKEwjkor-Y95WJAxVJHBAIHZLbHwkQ4dUDCA8&uact=5&oq=plantuml+component+examples&gs_lp=Egxnd3Mtd2l6LXNlcnAiG3BsYW50dW1sIGNvbXBvbmVudCBleGFtcGxlczIGEAAYFhgeMgsQABiABBiGAxiKBTILEAAYgAQYhgMYigUyCBAAGIAEGKIEMggQABiABBiiBDIIEAAYgAQYogRI-w5Q2AFYrw1wAngBkAEAmAFvoAG2AaoBAzEuMbgBA8gBAPgBAZgCBKACvwHCAgoQABiwAxjWBBhHmAMAiAYBkAYIkgcDMy4xoAfSBw&sclient=gws-wiz-serp

Прототип
![изображение](https://github.com/user-attachments/assets/62315e95-c4d8-4e63-9fc1-a063fb48949d)


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


## Описание компонентов

### Шаблон


#### Подробное описание

Сервис создан так то нужен для такого то такой то стек делала команда Х подразделения У

Мок ссылка на стр базы знаний

#### Зависимости

мМб не нужно это все

| Внешние Зависимости	 | Имя сервиса |
|:-----------|:-----------|
| Потребитель	 | Потребитель	 |
| Хранение данных	| PostgreSQL (тип БД) |


#### Компонент использует вызовы

##### Вызов - 1 

для такого то метод такой то, версия апи такая то

##### Вызов - 2 

для такого то метод такой то, версия апи такая то
описаны в сценарии

##### Вызов - 3 

для такого то метод такой то, версия апи такая то

##### Вызов - 4 

для такого то метод такой то, версия апи такая то

#### Компонент использует Таблицы БД

* Таблица 1 - набор данных для A
  Ссылка на справочник БД
* Таблица 2 - набор данных для B
  Ссылка на справочник БД

---

### Примеры по шаблону


#### Компонент Backend

Для бека

##### Подробное описание

Мок ссылка на стр базы знаний

##### Зависимости

| Внешние Зависимости	 | Имя сервиса |
|:-----------|:-----------|
| Потребитель	 | Потребитель	 |
| Хранение данных	| PostgreSQL (тип БД) |

##### Компонент использует вызовы


##### Вызов - 1 

для такого то метод такой то, версия апи такая то

POST/system/api/v1/apps/dataproc/inputdata/ 
v1
Тут сценарий https://github.com/NonameX11/TestPetDocumentationProject/blob/main/Feature%20Template/4%20-%20%D0%A1%D1%86%D0%B5%D0%BD%D0%B0%D1%80%D0%B8%D0%B8.md

##### Вызов - 2 
для такого то метод такой то, версия апи такая то
описаны в сценарии

##### Вызов - 3 
для такого то метод такой то, версия апи такая то

##### Вызов - 4 

для такого то метод такой то, версия апи такая то

#### Компонент использует Таблицы БД

* Таблица 1 - набор данных для A
  Ссылка на справочник БД
* Таблица 2 - набор данных для B
  Ссылка на справочник БД
_______
# API
  
## Пример описания вызова - Вызов 2 - Отправка введенных данных

== Что такое REST API: ==

> Описание https://github.com/NonameX11/TestPetDocumentationProject/blob/main/Feature%20Template/4.2%20-%20REST%20API.md

### Вызов и Endpoint url 

POST/system/api/v1/apps/dataproc/inputdata/{dataset}

 == НУЖНО попытаться добавить сваггер ==
 
> Описание добавления https://github.com/peter-evans/swagger-github-pages

### Описание и назначение вызова


| Имя | Назначение | Тип вызова | Метод | url |
| ------------- |:-------------:|:-------------:|:-------------:|:-------------:|
| Отправка данных в обработку | Отправка введенных пользователем данных с frontend формы на backend. <br>Для валидации и сохранения для последующей обработке согласно бизнес логике | REST API | POST  | /system/api/v1/apps/dataproc/inputdata/ |

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

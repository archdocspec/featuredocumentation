# Гайд по REST API


____________________________________

## Введение
>[!TIP]
>REST API (**R**epresentational **S**tate **T**ransfer **A**pplication **P**rogramming **I**nterface) — это архитектурный стиль, который использует HTTP-методы (`GET`, `POST`, `PUT`, `PATCH`, `DELETE`) для выполнения операций CRUD (создание, чтение, обновление и удаление) над ресурсами. 
Он описывает, как разработчику следует спроектировать интерфейс для взаимодействия своего приложения с другими. Если продолжить аналогию с естественным языком, то REST API описывает грамматику.

>**Описание работы REST API**
Здесь изображена связь между Клиентом и Сервером по API при помощи Вызовов и Ответов^
![RESTVisual](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/rest-api-1.png)


>[!NOTE]
> * Основные плюсы REST API -это простота изучения и применения, масштабируемость, возможности работы с различными форматами данных, такими как JSON и XML.
> * Главная особенность REST API — обмен сообщениями без сохранения состояния.
>  * Каждое сообщение самодостаточное и содержит всю информацию, необходимую для его обработки.
>  * Сервер не хранит результаты предыдущих сессий с клиентскими приложениями.
>  * Это обеспечивает гибкость и масштабируемость серверной части, позволяет поддерживать асинхронные взаимодействия и реализовывать алгоритмы обработки любой сложности.
>  * Кроме того, такой формат взаимодействия является универсальным — он не зависит от технологий, используемых на клиенте и на сервере, и не привязывает разработчиков к определенному провайдеру.

>[!CAUTION]
> Из-за того, что приходится каждый раз заново передавать все данные для обработки запроса, объем сообщений увеличивается. Чтобы сохранить при этом высокую скорость обмена, данные передаются в максимально сжатом формате. Чаще всего REST API использует формат JSON, более лаконичный чем XML.

____________________________________

## Основные принципы REST

1. **Клиент-серверная архитектура (Client/Server Architecture)**: Разделение некоторых зон. Клиент реализует только функциональное взаимодействие с сервером. Сервер реализует в себе логику хранения данных, сложные взаимодействия со смежными системами.
2. **Не хранить состояние (Stateless)**: Cервер не должен хранить у себя информацию о сессии с клиентом.Он должен в каждом запросе получать всю информацию для обработки.
3. **Кэширование (Cache)**: Каждый ответ сервера должен иметь пометку, можно ли его кэшировать
4. **Единообразие интерфейса (Uniform Interface)**: Сервер возвращает не только ресурс, но и его связи с другими ресурсами.
5. **Слоистая архитектура (Layered Architecture)**: Ни клиент, ни сервер не должны знать о том, как происходит цепочка вызовов дальше своих прямых соседей.
6. **Код по требованию (Code On Demand)**: Возможность передачи исполняемого кода от сервера клиенту.

>Визуализация связи принципов REST
>![RESTArc](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/RESTArch.jpg)

____________________________________

## Структура вызовов и ответов REST

>[!TIP]
> REST API работает по следующией схеме:
> 1. Клиент отправляет запрос (Request) на сервер.
> 2. Сервер аутентифицирует клиента и проверяет его права.
> 3. Затем, обрабатывает запрос и возвращает ответ (Response) клиенту.

>Пояснение: Вызов REST - прохождение вызова и получение ответа
>![RESTReqResp](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/RESTdescr.jpg)

### Вызов

>[!TIP]
> Каждый вызов REST состоит из определенных частей:

|Часть Вызова REST| Описание |
|:--:|:--|
| Конечная точка (endpoint) | Адрес, по которому отправляется запрос |
| Параметры | Делятся на параметры пути и параметры запроса. |
| Заголовки (headers) | В заголовках определяется формат передаваемых данных, спецификация и версия протокола обмена и другая информация, необходимая для корректной обработки запроса |
| Тело запроса (body) | Данные для обработки, как правило в формате JSON |

>Пояснение: Изображение структуры вызова REST
>![RESTRequest](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/HTTP%20Request.jpeg)

### Ответ
>[!TIP]
> Каждый ответ REST  также состоит из определенных частей, логически связанных с частями предшествующего вызова:

| Часть Ответа | Описание |
| :--: |:-- |
| Код ответа  | HTTP Код, признак успешности выполнения запроса. Для унификации используются стандартные коды ответа. |
| Заголовки (headers) | Заголовках определяется формат передаваемых данных, спецификация и версия протокола обмена и другая информация, необходимая для корректной обработки запроса |
| Тело запроса (body) | Информация, которую запрашивал клиент. Ответ тоже чаще всего передается в формате JSON. Но тело ответа может быть и пустым |

>Пояснение: Изображение структуры ответа REST
>![RESTResponse](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/HTTP%20Response.jpeg)

#### HTTP Коды ответов

>[!TIP]
> Здесь указано описание групп кодов ответа и основных используемых кодов.
> Расширенное описание кодов можно найти в конце статьи

| Код группы | Назначение группы | Пример |
| :----: | :---- | :---- |
| 2хх | Успешное выполнение запроса | 200 – ОК|
| 3хх | Перенаправление запроса или необходимость уточнения | 300 — на отправленный запрос есть несколько вариантов ответа. |
| 4хх | Ошибка при выполнении запроса | 400 – Bad Request. Запрос некорректный. |
| 5хх | Ошибки на стороне сервера | 500 - Internal Server Error. Ошибка на стороне сервера. |
____________________________________

##  Основные методы REST API

В REST API часто выделяются основные* методы, соответствующие стандартным операциям, которые выполняются над ресурсами для выполнения CRUD** - операций.



>![RESTMethods.jpg](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/RESTMethods.png)

>[!TIP]
>Это следующие методы:

| Метод | Описание | Пример использования | 
| :--: | :-- | :-- |
| `GET` | Адрес, по которому отправляется запрос | Проверка данных личного кабинета или открытие страницы меню | 
| `POST` | Создание нового объекта (ресурса) | Передать в службу доставки информацию о новом заказе | 
| `PUT` | Полная замена объекта (ресурса) на обновленную версию | Обновить данные оформленного и собранного заказа | 
| `PATCH` | Частичное изменение объекта (ресурса) | Обновление статуса и данных доставки заказа | 
| `DELETE` | Удаление информации об объекте (ресурсе) | Полное удаление всех данных отмененного заказа |

> (*) *Реже используются методы HEAD (для получения заголовка объекта или ресурса) и OPTIONS (возвращает список доступных методов)*
>
> (**) *Операции Create (создание), Read (чтение), Update (обновление), Delete (удаление)*

____________________________________

## Разбор основных методов REST API

### GET 

Метод для получения информации об объекте (ресурсе).
Метод удобен  и одновременно ограничем тем, что все данные запрашиваются в header запроса.

**(+) Правильное применение**
Запрашивать содержимое страниц каталогов, магазинов, WEB UI

**(-) Неправильное применение**
не рекомендуется передавать в вызове GET конфиденциальные данные, логины, и так далее.

> Структура Метода

```
GET <request-target>["?"<query>] HTTP/1.1
```

**Пример вызова**

<details>
  <summary><br>Пример Запроса</br></summary>

```
GET /api/users/1 HTTP/1.1
Host: example.com
Accept: application/json

```
</details>

<details>
  <summary><br>Пример Ответа</br></summary			   

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "name": "John Doe",
  "email": "john.doe@example.com"
}
                    
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "name": "John Doe",
  "email": "john.doe@example.com"
}

```

</details>

____________________________________

###  POST

POST-запросы используются для отправки данных на сервер, включая создания новых сущностей
В отличие от GET-запросов, которые используются для запроса данных.
POST-запросы часто применяются для отправки форм, загрузки файлов, взаимодействия с API и передачи конфиденциальных данных, поскольку данные передаются в теле запроса, а не в URL

> Структура Метода

```
POST <request-target>["?"<query>] HTTP/1.1
```

<details>
  <summary><br>Пример Запроса</br></summary>
	
```
POST /api/users HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "Jane Smith",
  "email": "jane.smith@example.com"
}
                    
POST /api/users HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "Jane Smith",
  "email": "jane.smith@example.com"
}

```

</details>

<details>
  <summary><br>Пример Ответа</br></summary
			  
```
HTTP/1.1 201 Created
Location: /api/users/2
Content-Type: application/json

{
  "id": 2,
  "name": "Jane Smith",
  "email": "jane.smith@example.com"
}
                    
HTTP/1.1 201 Created
Location: /api/users/2
Content-Type: application/json

{
  "id": 2,
  "name": "Jane Smith",
  "email": "jane.smith@example.com"
}


```

</details>

____________________________________

###  PUT

PUT-запросы в основном используются для обновления или замены существующего ресурса на сервере. 
Они также могут использоваться для создания нового ресурса, если он еще не существует на сервере. 
В отличие от POST-запросов, которые обычно используются для создания новых ресурсов, PUT-запросы заменяют существующий ресурс целиком, а не добавляют новые данные. 

> Структура Метода
```
PUT <request-target>["?"<query>] HTTP/1.1
```

<details>
  <summary><br>Пример Запроса</br></summary>	  
  
```
PUT /api/users/1 HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john.doe@newdomain.com"
}
                    
PUT /api/users/1 HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john.doe@newdomain.com"
}
```

</details>

<details>
  <summary><br>Пример Ответа</br></summary>
	  
```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "name": "John Doe",
  "email": "john.doe@newdomain.com"
}
                    
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "name": "John Doe",
  "email": "john.doe@newdomain.com"
}

```
</details>

____________________________________

### PATCH

PATCH-запросы в HTTP используются для частичного обновления ресурса, в отличие от PUT, который заменяет весь ресурс. PATCH-запросы отправляют только изменения, а не весь объект, что делает их более эффективными при необходимости обновить лишь отдельные части данных. 

> Структура Метода
 
```
PATCH <request-target>["?"<query>] HTTP/1.1
```

<details>
  <summary><br>Пример Запроса</br></summary>

```
PATCH /api/users/1 HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "email": "john.doe@updateddomain.com"
}
                    
PATCH /api/users/1 HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "email": "john.doe@updateddomain.com"
}
```

</details>



<details>
  <summary><br>Пример Ответа</br></summary>

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "name": "John Doe",
  "email": "john.doe@updateddomain.com"
}
                    
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "name": "John Doe",
  "email": "john.doe@updateddomain.com"
}

```
</details>

____________________________________

#### DELETE

Метод DELETE в REST используется для удаления конкретного ресурса на сервере.
Он отправляется на URL ресурса, который нужно удалить, и, если ресурс существует, он будет удален. 

> Структура Метода
```
DELETE <request-target>["?"<query>] HTTP/1.1
```

<details>
  <summary><br>Пример Запроса</br></summary>

```
DELETE /api/users/1 HTTP/1.1
Host: example.com
```
</details>


<details>
  <summary><br>Пример Ответа</br></summary>
	
```
DELETE /api/users/1 HTTP/1.1
Host: example.com
```
</details>

____________________________________

## Справочник по HTTP Кодам ответов

Расширенный список HTTP кодов ответов.

### Успешные ответы (200)

| Код  | Статус               | Описание                                     |
|-----|-----------------------|----------------------------------------------|
| 200 | OK                    | Запрос успешно выполнен.                     |
| 201 | Created               | Запрос успешно выполнен, ресурс создан.      |
| 204 | No Content            | Запрос успешно выполнен, но нет содержимого. |
| 206 | Partial Content       | Запрос выполнен частично.                    |

### Сообщения о перенаправлении (300)

| Код  | Статус                | Описание                                      		|
|-----|-----------------------|---------------------------------------------------------|
| 300 | Multiple Choices        | Запрос имеет несколько возможных ответов.     	|
| 301 | Moved Permanently       | Запрашиваемый ресурс был перемещен навсегда.  	|
| 303 | See Other               | Для получения ответа следует использовать другой URL. |
| 304 | Not Modified            | Ресурс не был изменен с последнего запроса.  		|
| 307 | Temporary Redirect      | Временный редирект на другой URL.            		|

### Ошибки клиента (400)

| Код   | Статус                  | Описание                                      		     |
|-------|-------------------------|-------------------------------------------------------	     |
| 400 | Bad Request             | Сервер не может обработать запрос из-за неверного синтаксиса.      |
| 401 | Unauthorized            | Запрос требует аутентификации.                		     |
| 403 | Forbidden               | Сервер понял запрос, но отказывается его выполнять. 		     |
| 404 | Not Found               | Запрашиваемый ресурс не найден.               		     |
| 405 | Method Not Allowed      | Метод, указанный в запросе, не поддерживается для данного ресурса. |
| 408 | Request Timeout         | Время ожидания запроса истекло.               |

### Ошибки сервера (500)

| Код   | Статус                  | Описание                                      |
|-------|-------------------------|-----------------------------------------------|
| 500 | Internal Server Error   | Внутренняя ошибка сервера.                    |
| 501 | Not Implemented         | Сервер не поддерживает функциональность, необходимую для выполнения запроса. |
| 502 | Bad Gateway             | Сервер, действующий как шлюз, получил недопустимый ответ от вышестоящего сервера. |
| 503 | Service Unavailable     | Сервер временно недоступен (например, из-за перегрузки или обслуживания). |
| 504 | Gateway Timeout         | Время ожидания ответа от вышестоящего сервера истекло. |

-------
                
## Заключение

REST API является мощным инструментом для взаимодействия между клиентом и сервером. 
Его принципы и методы позволяют создавать гибкие и масштабируемые приложения. 
Для более подробной информации о REST API и его методах, вы можете ознакомиться с документацией.
https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods

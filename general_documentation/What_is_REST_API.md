# Гайд по REST API

![RESTVisual](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/rest-api-1.png)

____________________________________

## Введение

REST API (**R**epresentational **S**tate **T**ransfer **A**pplication **P**rogramming **I**nterface) — это архитектурный стиль, который использует HTTP-методы для выполнения операций CRUD (создание, чтение, обновление и удаление) над ресурсами. 


REST API стал популярным благодаря своей простоте, масштабируемости и возможности работы с различными форматами данных, такими как JSON и XML.

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

## Структура вызова REST


Каждый вызов REST состоит из:

* HTTP Method: Метод (GET, POST, PUT, PATCH, DELETE)
* Endpoint: URL ресурса
* Header: Дополнительная информация о запросе (например, формат данных, аутентификация)
* Body: Параметры запроса (обычно в формате JSON или XML)
* Структура вызова REST

>Пояснение: Вызов REST - прохождение вызова
>![RESTCall](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/RESTdescr.jpg)

>Пояснение: Вызов REST - структура вызова
>![RESTCall](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/RESTSTRUCTUREDETAILED.png)

____________________________________

## Методы REST API

В REST API часто выделяются основные методы, соответствующие стандартным операциям, которые выполняются над ресурсами для выполнения CRUD операций.
>[!TIP]
>Это следующие методы:
>* GET
>* PUT
>* POST
>* PATCH
>* DELETE

>![RESTMethods.jpg](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/RESTMethods.png)

____________________________________

## Описание основных методов REST API

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
  <summary> Пример Запроса </summary>
```
GET /contact HTTP/1.1
Host: example.com
User-Agent: curl/8.6.0
Accept: */*
```
</details>

<details>
  <summary><br>Пример Ответа</br></summary			   
```
HTTP/1.1 200 OK
Content-Type: text/html; charset=UTF-8
Date: Fri, 21 Jun 2024 14:18:33 GMT
Last-Modified: Thu, 17 Oct 2019 07:18:26 GMT
Content-Length: 1234
<!doctype html>
<!-- HTML content follows -->
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
POST /test HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 27
field1=value1&field2=value2
```
</details>

<details>
  <summary><br>Пример Ответа</br></summary
			  
  
```
POST /test HTTP/1.1
Host: example.com
Content-Type: multipart/form-data;boundary="delimiter12345"

--delimiter12345
Content-Disposition: form-data; name="field1"

value1
--delimiter12345
Content-Disposition: form-data; name="field2"; filename="example.txt"

value2
--delimiter12345--
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
PUT /new.html HTTP/1.1
Host: example.com
Content-type: text/html
Content-length: 16

<p>New File</p>
```

</details>

<details>
  <summary><br>Пример Ответа</br></summary>
	  
```
HTTP/1.1 201 Created
Content-Location: /new.html
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
PATCH /users/123 HTTP/1.1
Host: example.com
Content-Type: application/json
Content-Length: 27
Authorization: Bearer ABC123

{
  "status": "suspended"
}
```

</details>



<details>
  <summary><br>Пример Ответа</br></summary>

```
HTTP/1.1 204 No Content
Content-Location: /users/123
ETag: "e0023aa4f"
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
DELETE /file.html HTTP/1.1
Host: example.com
```
</details>


<details>
  <summary><br>Пример Ответа</br></summary	    
```
HTTP/1.1 204 No Content
Date: Wed, 04 Sep 2024 10:16:04 GMT
```

</details>

____________________________________

## Справочник по HTTP Кодам ответов

Справочный материал по HTTP кодам, приходящим в ответах на REST запросы

### Успешные ответы (200)

| Код   | Статус                  | Описание                                      |
|-------|-------------------------|-----------------------------------------------|
| 200 | OK                      | Запрос успешно выполнен.                     |
| 201 | Created                 | Запрос успешно выполнен, ресурс создан.      |
| 204 | No Content              | Запрос успешно выполнен, но нет содержимого. |
| 206 | Partial Content         | Запрос выполнен частично.                     |

### Сообщения о перенаправлении (300)

| Код   | Статус                  | Описание                                      |
| 300 | Multiple Choices        | Запрос имеет несколько возможных ответов.    |
| 301 | Moved Permanently       | Запрашиваемый ресурс был перемещен навсегда. |
| 302 | Found                   | Запрашиваемый ресурс временно доступен по другому URL. |
| 303 | See Other               | Для получения ответа следует использовать другой URL. |
| 304 | Not Modified            | Ресурс не был изменен с последнего запроса.  |
| 307 | Temporary Redirect      | Временный редирект на другой URL.            |

### Ошибки клиента (400)

| Код   | Статус                  | Описание                                      |
| 400 | Bad Request             | Сервер не может обработать запрос из-за неверного синтаксиса. |
| 401 | Unauthorized            | Запрос требует аутентификации.                |
| 403 | Forbidden               | Сервер понял запрос, но отказывается его выполнять. |
| 404 | Not Found               | Запрашиваемый ресурс не найден.               |
| 405 | Method Not Allowed      | Метод, указанный в запросе, не поддерживается для данного ресурса. |
| 408 | Request Timeout         | Время ожидания запроса истекло.               |

### Ошибки сервера (500)

| Код   | Статус                  | Описание                                      |
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

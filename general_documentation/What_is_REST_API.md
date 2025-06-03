# REST API

## Введение

REST API (**R**epresentational **S**tate **T**ransfer **A**pplication Programming Interface) — это архитектурный стиль, который использует HTTP-методы для выполнения операций CRUD (создание, чтение, обновление и удаление) над ресурсами. 


REST API стал популярным благодаря своей простоте, масштабируемости и возможности работы с различными форматами данных, такими как JSON и XML.

## Основные принципы REST

1. **Клиент-серверная архитектура (Client/Server Architecture)**: Разделение некоторых зон. Клиент реализует только функциональное взаимодействие с сервером. Сервер реализует в себе логику хранения данных, сложные взаимодействия со смежными системами.
2. **Не хранить состояние (Stateless)**: Cервер не должен хранить у себя информацию о сессии с клиентом.Он должен в каждом запросе получать всю информацию для обработки.
3. **Кэширование (Cache)**: Каждый ответ сервера должен иметь пометку, можно ли его кэшировать
4. **Единообразие интерфейса (Uniform Interface)**: Сервер возвращает не только ресурс, но и его связи с другими ресурсами.
5. **Слоистая архитектура (Layered Architecture)**: Ни клиент, ни сервер не должны знать о том, как происходит цепочка вызовов дальше своих прямых соседей.
6. **Код по требованию (Code On Demand)**: Возможность передачи исполняемого кода от сервера клиенту.

>Визуализация связи принципов REST
>![RESTArc](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/RESTArch.jpg)

## Структура вызова REST


Каждый вызов REST состоит из:

* HTTP Method: Метод (GET, POST, PUT, PATCH, DELETE)
* Endpoint: URL ресурса
* Header: Дополнительная информация о запросе (например, формат данных, аутентификация)
* Body: Параметры запроса (обычно в формате JSON или XML)
* Структура вызова REST

>Изображение 1 Вызов REST - прохождение вызова
>![RESTCall](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/RESTdescr.jpg)

>Изображение 1 Вызов REST - структура вызова
>![RESTCall](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/RESTStructure.jpg)

## Основные методы REST API

В REST API особенно выделяются основные методы, соответствующие стандартным операциям, которые выполняются над ресурсами. 

>Описание основых методов
>![RESTMethods.jpg](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/RESTMethods.png)

### 1. GET
Метод для получения данных.

Запрос:
``` 
GET /objectserver/restapi/alerts/status HTTP/1.1
Accept: application/json
Authorization: Basic dGVzdHVzZXIwMTpuZXRjb29s
Host: localhost
Connection: keep-alive
```
            
Ответ:

```
HTTP/1.1 200 OK
{
  "rowset": {
    "osname": "NCOMS",
    ...
  }
}
```                   

                
### 2. POST
Метод для создания нового объекта.

Запрос:

```
POST /objectserver/restapi/alerts/status HTTP/1.1
Content-Type: application/json
...
{
  "rowset": {
    "rows": [
      {
        "Identifier": "JunitEventTestInstance####1",
        ...
      }
    ]
  }
}
```                    
POST /objectserver/restapi/alerts/status HTTP/1.1
Content-Type: application/json
...
{
  "rowset": {
    "rows": [
      {
        "Identifier": "JunitEventTestInstance####1",
        ...
      }
    ]
  }
}
```

Ответ:
``` 
HTTP/1.1 201 Created
{
  "entry": {
    "affectedRows": 1,
    "uri": "http://localhost/objectserver/restapi/alerts/status/kf/12481%3ANCOMS"
  }
}
```                    


                
### 3. PUT

Метод для полной замены объекта.
>[!TIP]
> Применяется для ????

Запрос:
``` 
 
PUT /objectserver/restapi/alerts/status/1 HTTP/1.1
Content-Type: application/json
...
{
  "Identifier": "UpdatedIdentifier",
  ...
}
                    
PUT /objectserver/restapi/alerts/status/1 HTTP/1.1
Content-Type: application/json
...
{
  "Identifier": "UpdatedIdentifier",
  ...
}

                
Ответ:

```
 
HTTP/1.1 200 OK
{
  "entry": {
    "affectedRows": 1
  }
}
                    
HTTP/1.1 200 OK
{
  "entry": {
    "affectedRows": 1
  }
}

```                
### 4. PATCH
Метод для частичного обновления объекта.


``` 
Запрос:
 
PATCH /objectserver/restapi/alerts/status/1 HTTP/1.1
Content-Type: application/json
...
{
  "LastOccurrence": 1341412235
}
                    
PATCH /objectserver/restapi/alerts/status/1 HTTP/1.1
Content-Type: application/json
...
{
  "LastOccurrence": 1341412235
}
``` 
                
Ответ:
``` 
 
HTTP/1.1 200 OK
{
  "entry": {
    "affectedRows": 1
  }
}
                    
HTTP/1.1 200 OK
{
  "entry": {
    "affectedRows": 1
  }
}
``` 
                
### 5. DELETE
Метод для удаления объекта.

Запрос:

``` 
DELETE /objectserver/restapi/alerts/status/1 HTTP/1.1
``` 
                
Ответ:

``` 
HTTP/1.1 200 OK
{
  "entry": {
    "affectedRows": 1
  }
}
``` 
                
## Заключение

REST API является мощным инструментом для взаимодействия между клиентом и сервером. 
Его принципы и методы позволяют создавать гибкие и масштабируемые приложения. 
Для более подробной информации о REST API и его методах, вы можете ознакомиться с документацией.
https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods

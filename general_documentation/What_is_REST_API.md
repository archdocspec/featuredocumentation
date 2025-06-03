
# REST API

## Введение

REST API (Representational State Transfer Application Programming Interface) — это архитектурный стиль, который использует HTTP-методы для выполнения операций CRUD (создание, чтение, обновление и удаление) над ресурсами. REST API стал популярным благодаря своей простоте, масштабируемости и возможности работы с различными форматами данных, такими как JSON и XML.

![REST API](https://github.com/user-attachments/assets/0036331f-c8fe-4eb3-b8d3-5b0757825896)

## Основные принципы REST

1. Клиент-серверная архитектура: Разделение функций клиента и сервера.
2. Stateless: Сервер не хранит информацию о сессии с клиентом.
3. Кэширование: Ответы сервера могут быть кэшированы.
4. Единообразие интерфейса: Сервер возвращает не только ресурс, но и его связи с другими ресурсами.
5. Слоистая архитектура: Клиент и сервер не знают о цепочке вызовов за пределами своих непосредственных соседей.
6. Код по требованию: Возможность передачи исполняемого кода от сервера клиенту.

## Структура вызова REST

Каждый вызов REST состоит из:

- HTTP Method: Метод (GET, POST, PUT, PATCH, DELETE)
- Endpoint: URL ресурса
- Header: Дополнительная информация о запросе (например, формат данных, аутентификация)
- Body: Параметры запроса (обычно в формате JSON или XML)

![Структура вызова REST](https://github.com/user-attachments/assets/ad19e5d9-518f-48d8-bf84-1e6bf3898670)

## Основные методы REST API

### 1. GET

Метод для получения данных.

Запрос:
                    
# REST API

## Введение

REST API (Representational State Transfer Application Programming Interface) — это архитектурный стиль, который использует HTTP-методы для выполнения операций CRUD (создание, чтение, обновление и удаление) над ресурсами. REST API стал популярным благодаря своей простоте, масштабируемости и возможности работы с различными форматами данных, такими как JSON и XML.

![REST API](https://github.com/user-attachments/assets/0036331f-c8fe-4eb3-b8d3-5b0757825896)

## Основные принципы REST

1. Клиент-серверная архитектура: Разделение функций клиента и сервера.
2. Stateless: Сервер не хранит информацию о сессии с клиентом.
3. Кэширование: Ответы сервера могут быть кэшированы.
4. Единообразие интерфейса: Сервер возвращает не только ресурс, но и его связи с другими ресурсами.
5. Слоистая архитектура: Клиент и сервер не знают о цепочке вызовов за пределами своих непосредственных соседей.
6. Код по требованию: Возможность передачи исполняемого кода от сервера клиенту.

## Структура вызова REST

Каждый вызов REST состоит из:

- HTTP Method: Метод (GET, POST, PUT, PATCH, DELETE)
- Endpoint: URL ресурса
- Header: Дополнительная информация о запросе (например, формат данных, аутентификация)
- Body: Параметры запроса (обычно в формате JSON или XML)

![Структура вызова REST](https://github.com/user-attachments/assets/ad19e5d9-518f-48d8-bf84-1e6bf3898670)

## Основные методы REST API

### 1. GET

Метод для получения данных.

Запрос:

                
GET /objectserver/restapi/alerts/status HTTP/1.1

Accept: application/json

Authorization: Basic dGVzdHVzZXIwMTpuZXRjb29s

Host: localhost

Connection: keep-alive

1
2
3
4
5
6
 
Ответ:
                    
Ответ:

                
HTTP/1.1 200 OK

{

“rowset”: {

“osname”: “NCOMS”,

…

}

}

1
2
3
4
5
6
 
### 2. POST

Метод для создания нового объекта.

Запрос:
                    
### 2. POST

Метод для создания нового объекта.

Запрос:

                
POST /objectserver/restapi/alerts/status HTTP/1.1

Content-Type: application/json

…

{

“rowset”: {

“rows”: [

{

“Identifier”: “JunitEventTestInstance####1”,

…

}

]

}

}

1
2
3
4
5
6
 
Ответ:
                    
Ответ:

                
HTTP/1.1 201 Created

{

“entry”: {

“affectedRows”: 1,

“uri”: “http://localhost/objectserver/restapi/alerts/status/kf/12481%3ANCOMS”

}

}

1
2
3
4
5
6
 
### 3. PUT

Метод для полной замены объекта.

Запрос:
                    
### 3. PUT

Метод для полной замены объекта.

Запрос:

AA13, [04.06.2025 0:02]
PUT /objectserver/restapi/alerts/status/1 HTTP/1.1

Content-Type: application/json

…

{

“Identifier”: “UpdatedIdentifier”,

…

}

1
2
3
4
5
6
 
Ответ:
                    
Ответ:

                
HTTP/1.1 200 OK

{

“entry”: {

“affectedRows”: 1

}

}

1
2
3
4
5
6
 
### 4. PATCH

Метод для частичного обновления объекта.

Запрос:
                    
### 4. PATCH

Метод для частичного обновления объекта.

Запрос:

                
PATCH /objectserver/restapi/alerts/status/1 HTTP/1.1

Content-Type: application/json

…

{

“LastOccurrence”: 1341412235

}

1
2
3
4
5
6
 
Ответ:
                    
Ответ:

                
HTTP/1.1 200 OK

{

“entry”: {

“affectedRows”: 1

}

}

1
2
3
4
5
6
 
### 5. DELETE

Метод для удаления объекта.

Запрос:
                    
### 5. DELETE

Метод для удаления объекта.

Запрос:

                
DELETE /objectserver/restapi/alerts/status/1 HTTP/1.1

…

1
2
3
4
5
6
 
Ответ:
                    
Ответ:

                
HTTP/1.1 200 OK

{

“entry”: {

“affectedRows”: 1

}

}

1
2
3
4
5
6
 
## Заключение

REST API является мощным инструментом для взаимодействия между клиентом и сервером. Его принципы и методы позволяют создавать гибкие и масштабируемые приложения. Для более подробной информации о REST API и его методах, вы можете ознакомиться с [документацией](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods).

![Структура сообщения вызова REST](https://github.com/user-attachments/assets/94893027-7033-4a47-95db-08b1c79a2d1b)
                    
## Заключение

REST API является мощным инструментом для взаимодействия между клиентом и сервером. Его принципы и методы позволяют создавать гибкие и масштабируемые приложения. Для более подробной информации о REST API и его методах, вы можете ознакомиться с [документацией](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods).

![Структура сообщения вызова REST](https://github.com/user-attachments/assets/94893027-7033-4a47-95db-08b1c79a2d1b)

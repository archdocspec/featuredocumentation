AA13, [03.06.2025 23:57]
REST API
Введение
REST API (Representational State Transfer Application Programming Interface) — это архитектурный стиль, который использует HTTP-методы для выполнения операций CRUD (создание, чтение, обновление и удаление) над ресурсами. REST API стал популярным благодаря своей простоте, масштабируемости и возможности работы с различными форматами данных, такими как JSON и XML.

REST API

Основные принципы REST
Клиент-серверная архитектура: Разделение функций клиента и сервера.
Stateless: Сервер не хранит информацию о сессии с клиентом.
Кэширование: Ответы сервера могут быть кэшированы.
Единообразие интерфейса: Сервер возвращает не только ресурс, но и его связи с другими ресурсами.
Слоистая архитектура: Клиент и сервер не знают о цепочке вызовов за пределами своих непосредственных соседей.
Код по требованию: Возможность передачи исполняемого кода от сервера клиенту.
Структура вызова REST
Каждый вызов REST состоит из:

HTTP Method: Метод (GET, POST, PUT, PATCH, DELETE)
Endpoint: URL ресурса
Header: Дополнительная информация о запросе (например, формат данных, аутентификация)
Body: Параметры запроса (обычно в формате JSON или XML)
Структура вызова REST

Основные методы REST API
1. GET
Метод для получения данных.

Запрос:

http
1
2
3
4
5
6
 
GET /objectserver/restapi/alerts/status HTTP/1.1
Accept: application/json
Authorization: Basic dGVzdHVzZXIwMTpuZXRjb29s
Host: localhost
Connection: keep-alive
                    
GET /objectserver/restapi/alerts/status HTTP/1.1
Accept: application/json
Authorization: Basic dGVzdHVzZXIwMTpuZXRjb29s
Host: localhost
Connection: keep-alive

                
Ответ:

json
1
2
3
4
5
6
7
8
 
HTTP/1.1 200 OK
{
  "rowset": {
    "osname": "NCOMS",
    ...
  }
}
                    
HTTP/1.1 200 OK
{
  "rowset": {
    "osname": "NCOMS",
    ...
  }
}

                
2. POST
Метод для создания нового объекта.

Запрос:

http
1
2
3
4
5
6
7
8
9
10
11
12
13
14
 
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

                
Ответ:

json
1
2
3
4
5
6
7
8
 
HTTP/1.1 201 Created
{
  "entry": {
    "affectedRows": 1,
    "uri": "http://localhost/objectserver/restapi/alerts/status/kf/12481%3ANCOMS"
  }
}
                    
HTTP/1.1 201 Created
{
  "entry": {
    "affectedRows": 1,
    "uri": "http://localhost/objectserver/restapi/alerts/status/kf/12481%3ANCOMS"
  }
}

                
3. PUT
Метод для полной замены объекта.

Запрос:

http
1
2
3
4
5
6
7
8
 
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

json
1
2
3
4
5
6
7
 
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

                
4. PATCH
Метод для частичного обновления объекта.

Запрос:

http
1
2
3
4
5
6
7
 
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

                
Ответ:

json
1
2
3
4
5
6
7
 
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

                
5. DELETE
Метод для удаления объекта.

Запрос:

http
1
2
3
4
5
6
 
DELETE /objectserver/restapi/alerts/status/1 HTTP/1.1
...
                    
DELETE /objectserver/restapi/alerts/status/1 HTTP/1.1
...

                
Ответ:

AA13, [03.06.2025 23:57]
json
1
2
3
4
5
6
7
 
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

                
Заключение
REST API является мощным инструментом для взаимодействия между клиентом и сервером. Его принципы и методы позволяют создавать гибкие и масштабируемые приложения. Для более подробной информации о REST API и его методах, вы можете ознакомиться с документацией.

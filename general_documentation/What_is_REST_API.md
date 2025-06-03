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

>Пояснение: Вызов REST - прохождение вызова
>![RESTCall](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/RESTdescr.jpg)

>Пояснение: Вызов REST - структура вызова
>![RESTCall](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/RESTStructure.jpg)

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

## Описание основных методов REST API

### GET 

Метод для получения информации об объекте (ресурсе).
Удобен  и одновременно ограничем тем, что все данные запрашиваются в header запроса.
(+) МОЖНО
Запрашивать содержимое страниц каталогов, магазинов, WEB UI
(-) НЕ НУЖНО
Передавать конфиденциальные данные, логины+пароли и т.п.

> Подробное описание:  https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET | 


<details>
  <summary> Запрос </summary
			  
  
```
GET /objectserver/restapi/alerts/status HTTP/1.1
Accept: application/json
Authorization: Basic dGVzdHVzZXIwMTpuZXRjb29s
Host: localhost
Connection: keep-alive
```

</details>


<details>
  <summary> Ответ  </summary
			  
  
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Server: libnhttpd
Date: Wed Jul 4 15:32:03 2012
Connection: Keep-Alive:
Content-Type: application/rdf+xml
Content-Length: 24860
	{
"rowset":	{
		"osname":	"NCOMS",
		"dbname":	"alerts",
		"tblname":	"status",
		"coldesc":	[{
				"name":	"Identifier",
				"type":	"string",
				"size":	255
			}, {
				"name": "Serial",
				"type": "integer",
				"size": 4
			}, {
				"name": "Node",
				"type": "string",
				"size": 64
			}, {
				"name": "NodeAlias",
				"type": "string",
				"size": 64
			}, {
				"name": "AlertKey",
				"type": "string",
				"size": 255
			}, {
				"name": "Severity",
				"type": "integer",
				"size": 4
			}, {
				"name": "Summary",
				"type": "string",
				"size": 255
			}, {
				"name": "StateChange",
				"type": "utc",
				"size": 4
			}, {
				"name": "FirstOccurrence",
				"type": "utc",
				"size": 4
			}, {
				"name": "LastOccurrence",
				"type": "utc",
				"size": 4
			}, {
				"name": "RowSerial",
				"type": "integer",
				"size": 4
			}],
		"rows":		[{
				"Identifier": "Startup@sol9-build1",
				"Serial": 12469,
				"Node": "sol9-build1",
				"NodeAlias": "",
				"AlertKey": "",
				"Severity": 0,
				"Summary": "ObjectServer NCOMS on sol9-build1 started at Wed Jul 04 15:27:57 2012",
				"StateChange": 1341412082,
				"FirstOccurrence": 1341411978,
				"LastOccurrence": 1341412077,
				"RowSerial": 12469
			}, {
				"Identifier": "ProfilerEnableToggle@NCOMS:sol9-build1",
				"Serial": 12468,
				"Node": "sol9-build1",
				"NodeAlias": "",
				"AlertKey": "",
				"Severity": 0,
				"Summary": "ObjectServer NCOMS Profiler enabled at Wed Jul 04 15:27:56 2012",
				"StateChange": 1341412077,
				"FirstOccurrence": 1341411976,
				"LastOccurrence": 1341412076,
				"RowSerial": 12468
			}, {
				"Identifier": "JUnitEventTestInstance####0",
				"Serial": 12469,
				"Node": "sol9-build1",
				"NodeAlias": "",
				"AlertKey": "JUnitEventInstance",
				"Severity": 0,
				"Summary": "This is a test event generated by the JUnit REST Event Tests. (0)",
				"StateChange": 1341412184,
				"FirstOccurrence": 1341411772,
				"LastOccurrence": 1341412074,
				"RowSerial": 12468
			}, {
				"Identifier": "Shutdown@sol9-build1",
******* TRUNCATED ********
				"RowSerial": 12519
			}],
		"affectedRows": 12
	}
}
```

</details>
___

###  POST

Метод для создания нового объекта (ресурса) 

> Подробное описание:  https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST


<details>
  <summary> Запрос </summary
			    
```
Accept: application/json
Authorization: Basic dGVzdHVzZXIwMTpuZXRjb29s
Content-Type: application/json
Host: localhost
Connection: keep-alive
Content-Length: 984

{
	"rowset":	{
			"coldesc": [ {
					"type": "string",
					"name": "Identifier"
			}, {
					"type": "string",
					"name": "Node"
			}, {
					"type": "string",
					"name": "AlertKey"
			}, {
					"type": "integer",
					"name": "Severity"
			}, {
					"type": "string",
					"name": "Summary"
			}, {
					"type": "utc",
					"name": "FirstOccurrence"
			}, {
					"type": "utc",
					"name": "LastOccurrence"
			}, {
					"type": "integer",
					"name": "OwnerUID"
			}, {
					"type": "integer",
					"name": "OwnerGID"
			}],
			"rows":	[ {
					"FirstOccurrence": 1341412087,
					"Node": "localhost",
					"AlertKey": "JUnitEventInstance",
					"Summary": "This is a test event generated by the JUnit REST Event Tests.(1)",
					"LastOccurrence": 1341412087,
					"Identifier": "JunitEventTestInstance####1",
					"OwnerGID": 0,
					"Severity": 4,
					"OwnerUID": 0
		}]
	}
}
```

</details>


<details>
  <summary> Ответ  </summary
			  
  
```
HTTP/1.1 201 Created
Location: http://localhost/objectserver/restapi/alerts/status/kf/12481%3ANCOMS
Cache-Control: no-cache
Server: libnhttpd
Date: Wed Jul 4 15:31:53 2012
Connection: Keep-Alive
Content-Type: application/json;charset=UTF-8
Content-Length: 304
{
	"entry":	{
		"affectedRows": 1,
		"keyField": "12481%3ANCOMS",
		"uri": "http://localhost/objectserver/restapi/alerts/status/kf/12481%3ANCOMS"
	}
}
```

</details>
___

###  PUT

Метод для полной замены объекта (ресурса) на обновленную версию 

> Подробное описание:  https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PUT

Пример структуры:

<details>
  <summary>Запрос </summary
			  
  
```

```

</details>

<details>
  <summary> Ответ </summary
			  
  
```

```

</details>
___

### PATCH

Метод для частичного изменения объекта (ресурса) 

> Подробное описание: https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PATCH


<details>
  <summary>Запрос </summary
			  
  
```
PATCH /objectserver/restapi/alerts/status HTTP/1.1
Accept: application/json
Authorization: Basic dGVzdHVzZXIwMTpuZXRjb29s
Content-Type: application/json
Host: localhost
Connection: keep-alive
Content-Length: 1092
{
	"rowset": {
		"coldesc": [
			{
				"type": "integer",
				"name": "Acknowledged"
			},
			{
				"type": "string",
				"name": "Location"
			},
			{
				"type": "integer",
				"name": "OwnerUID"
			},
			{
				"type": "integer",
				"name": "OwnerGID"
			},
			{
				"type": "utc",
				"name": "LastOccurrence"
			}
		],
		"rows": [
			{
				"Location": "UPDATED",
				"LastOccurrence": 1341412235,
				"Acknowledged": 1,
				"OwnerUID": 65534,
				"OwnerGID": 1
			}
		]
	}
}
```

</details>



<details>
  <summary> Ответ  </summary
			  
  
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Server: libnhttpd
Date: Wed Jul 4 15:32:03 2012
Connection: Keep-Alive:
Content-Type: application/json;charset=UTF-8
Content-Length: 158
{
	"entry":	{
		"affectedRows": 10,
		"uri": "http://localhost/objectserver/restapi/alerts/status"
	}
}
```

</details>
___

#### DELETE

Метод для удаления информации об объекте (ресурсе) 

> Подробное описание: https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/DELETE

<details>
  <summary>Запрос </summary
			  
  
```
DELETE /objectserver/restapi/alerts/status HTTP/1.1
Accept: application/json
Authorization: Basic dGVzdHVzZXIwMTpuZXRjb29s
Host: localhost
Connection: keep-alive
```

</details>


<details>
  <summary> Ответ  </summary
			  
  
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Server: libnhttpd
Date: Wed Jul 4 15:38:53 2012
Connection: Keep-Alive:
Content-Type: application/json;charset=UTF-8
Content-Length: 157
{
	"entry":	{
		"affectedRows": 10,
		"uri": "http://localhost/objectserver/restapi/alerts/status"
	}
}
```

</details>


_____________
_____________
_____________
## КРИВОЕ

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

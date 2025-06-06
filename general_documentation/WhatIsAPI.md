# Что такое API

## API

API (**A**pplication **P**rogramming **I**nterface) — это набор правил и протоколов, которые позволяют разным программам и сервисам взаимодействовать друг с другом.
API Различаются по области применения, архитектурным стилям, быстродействию, допустимым форматам данных и прочим подобным параметрам.

## Назначение и типы API

![изображение](https://github.com/user-attachments/assets/30a5e487-1af4-45de-8505-160cb332055d)


### Для чего нужны API

Они обеспечивают обмен данными между различными системами и упрощают разработку приложений. 
Это позволяет разработчикам создавать новые продукты и услуги, интегрируя их с существующими сервисами.

### Типы API

Основные типы API — это REST, SOAP, GraphQL, WebSocket и RPC, каждый из которых имеет свои особенности и предназначен для определённых задач.

> [!TIP]
> **REST** (**Re**presentational **S**tate **T**ransfer) — архитектурный стиль взаимодействия компонентов распределённого приложения, использующий HTTP-запросы для получения данных с сервера. 
    Он позволяет создавать масштабируемые и гибкие системы, которые легко интегрируются с другими сервисами.
    
>Графическое описание REST    
>![REST](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/RESTdescr.jpg "REST API")

> [!TIP]
> **SOAP** (**S**imple **O**bject **A**ccess **P**rotocol) — протокол обмена структурированными данными в виде XML-сообщений, обеспечивающий безопасность и надёжность передачи информации между приложениями. 
    SOAP используется для создания веб-сервисов, которые могут взаимодействовать друг с другом.

>Графическое описание SOAP    
>![SOAP](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/soap.png "SOAP")


> [!TIP]
> **GraphQL** — язык запросов, который позволяет клиентам запрашивать только необходимые данные с сервера. 
    Что ускоряет работу приложений и снижает нагрузку на сервер. В нем структура данных представлена в виде графа, где узлы графа представляют собой объекты, а рёбра - связи между этими объектами.
GraphQL подходит для сложных систем, где требуется гибкая настройка запросов.

>**Графическое описание GraphQL**
>
>![GraphQL](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/graphql.png "GraphQL")

> [!TIP]
> **WebSocket** — технология, которая обеспечивает полнодуплексное общение между клиентом и сервером через постоянное соединение. 
Она позволяет передавать данные в реальном времени, что делает её идеальной для игр, чатов и других приложений, требующих мгновенной реакции.

> **Графическое описание WebSocket**
>
>![WebSocket](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/http_websocket.png "GraphQL")

> [!TIP]
> **RPC** (**R**emote **P**rocedure **C**all) — механизм вызова процедур или функций на удалённом сервере, как если бы они были локальными. 
RPC обеспечивает взаимодействие между компонентами системы и позволяет им обмениваться данными и выполнять задачи используя буфер протокола (ProtoBuff).

> **Графическое описание RPC**
> 
>![rpc](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/RPC.jpg "RPC")

>**Графическое описание protobuff**
> 
>![protobuff](https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/protobuff.jpg "protobuff")

### Выбор API

Выбор подходящего API зависит от требований проекта и используемых технологий. 
Необходимо определить требования к взаимодействию систем, учесть особенности данных и выбрать наиболее подходящий тип API.

#### Критерии выбора API

Это основные факторы, важные для конкретного проекта.

* Совместимость
* Безопасность
* Производительностьw
* Стоимость
  
#### Сводная таблица критериев API

В таблице собраны характеристики популярных типов API, включая области применения.



| СВОЙСТВА / ТИПЫ | **REST API** | **(g)RPC** | **SOAP** | **GraphQL** | **WebSocket** |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| **Что это?** | API, спроектированное в архитектурном стиле REST | фреймворк удаленного вызова процедур (RPC) для общения клиента и серверам друг с другом  | Протокол для создания API | Язык запросов и серверная среда для API | Одновременные двусторонние каналы связи по одному TCP |
| **Ключевые свойства** | Без состояния, ориентированный на ресурсы, управляемый данными, гибкий | Потоковая передача, высокая производительность, ориентированный на действия | Стандартизированный, высокозащищенный, ориентированный на предприятия | Одна конечная точка, строго типизированные запросы, отсутствие избыточной передачи данных, самодокументируемый | Соединение в реальное времени, двунаправленные сообщения |
| **Форматы данных** | JSON, XML, YAML, HTML, простой текст  | JSON, XML, Thrift, Protobuf, FlatBuffers | **только XML**  | **JSON** | Фреймы 6 типов: текст, бинарный, ping, pong, закрытие и продолжение |
| **Кривая обучения** | Легкая | Легкая | **Сложная** | Средняя | Средняя |
| **Сообщество** | Большое | Большое | **Малое** | Растущее | Большое |
| **Сценарии использования** | все виды веб-приложений, облачные приложения, облачные вычислительные услуги | сложные микросервисные системы, IoT-приложения | Финансовые услуги, CRM-программное обеспечение, управление идентификацией, интеграция устаревших систем | Высокопроизводительные мобильные приложения, сложные системы и архитектуры на основе микросервисов | Онлайн-чаты, доски для рисования, онлайн-игры, панели мониторинга в реальном времени, финансовая торговля |
| **Протокол** | HTTP | ITTP / 2 | На основе XML | HTTP, одна конечная точка | TCP, начальная рукопожатие HTTP |    

>**Ориганальное изображение таблицы**

![Сводная таблица критериев API]            (https://github.com/archdocspec/featuredocumentation/blob/main/general_documentation/assets/main_api_types.jpg "Сводная таблица критериев API")

----

## Дополнительные материалы

https://newsletter.techworld-with-milan.com/p/what-are-the-main-api-architecture

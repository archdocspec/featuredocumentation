# Шаблон для описания целей и сущностей решения

> [!NOTE]
> Этот раздел шаблона предназначен для фиксации общих черт описываемого решения.
Содержимое включать в себя различные обобщенные описания, глоссарии, диаграммы, ссылки, относящиеся ко всему запланированному далее.

> [!CAUTION]
> Достаточно подробное описание изначального смысла и целей создания решения позволит **ЗНАЧИТЕЛЬНО** упростить дальнейшую работу с ним, а также - избежать разногласий при обсуждениях.

>**Образец**

Целевое решение представляет собой интегрированную платформу, предназначенную для оптимизации бизнес-процессов и повышения эффективности работы пользователей.
Оно включает в себя автоматизацию ключевых операций, улучшение взаимодействия между различными системами и упрощение доступа к необходимой информации. Основные цели решения заключаются в снижении временных затрат на выполнение задач, повышении точности данных и улучшении пользовательского опыта.
В результате внедрения данного решения ожидается значительное увеличение производительности, сокращение издержек и улучшение качества обслуживания клиентов.

## 1. Описание решения

> [!TIP]
> Добавьте краткое общее описание целевого решения. Это должно быть сжатое и ясное представление сути вашего проекта, доработки или существующего решения

>**Образец**

Основная цель данного решения заключается в автоматизации процесса обработки информации, что позволит сократить время выполнения задач на 30% в течение следующих 6 месяцев.

## 2. Главная цель решения
> [!TIP]
> Определите основную цель, которой посвещено решение. Укажите бизнес-задачу, которую оно решает. Формулировка должна быть четкой и измеримой, чтобы можно было оценить успешность выполнения задачи. И, по возможности, содержащее целеполагание и основы функциональных и нефункциональных требований.

>**Образец**

**Цель**

Главная цель решения - устранение узких мест в текущем процессе работы с системой, автоматизация обработки данных и принятия решений.

**Бизнес-задача**

* Снижение временных затрат
* Уход от бюрократии, излишних согласований
* Повышению общей эффективности работы команды и улучшению клиентского опыта.


## 3. Связанные объекты
> [!TIP]
> Сюда рекомендуется добавить отсылки на различные артефакты, документы и другие важные объекты, имеющие отношения к работе с решением. Это может быть список ссылок на связанную документацию, задачи в трекере (например, Jira), каталоги инфраструктуры, ссылки на Frontend стенды продакшена и т.п.

> **Образец**

* https://jira.companyname.com/browse/ISSUE-999 - Ссылка на задачу по внедрению решения
* https://сonfluence.companyname.com/pages/viewpage.action?pageId=123456790 - Ссылка на описание концепта
* https://companyname.com/products/producui - интерфейс для доработки

## 4. Глоссарий
> [!TIP]
> Создайте таблицу с терминами и их значениями для упорядочивания смыслов, понятий и терминов

> **Пример таблицы глоссария**

| Термин                | Значение                                                        |
|:------------| --------------------------------------------------------------------------|
|Решение| Набор программного обеспечения, систем и технологий, направленный на решение конкретной задачи в области информационных технологий. Это могут быть как готовые или разрабатываемые самостоятельно продукты, так и *отдельные доработки в рамках продуктов** |
| Требования к Решению (разработке)** | Совокупность запросов/утверждений относительно атрибутов, свойств или качеств программной системы, подлежащей реализации. |

(*) *В шаблоне рассматривается именно отдельная доработка*

(**) Подробнее о требованиях и разнице между ними можно прочить здесь [Требования](https://ru.wikipedia.org/wiki/%D0%A2%D1%80%D0%B5%D0%B1%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F_%D0%BA_%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%BD%D0%BE%D0%BC%D1%83_%D0%BE%D0%B1%D0%B5%D1%81%D0%BF%D0%B5%D1%87%D0%B5%D0%BD%D0%B8%D1%8E "Требования к программному обеспечению")

## 5. Сущности решения

> [!TIP]
>Составьте список всех сущностей, которые участвуют в данном решении. Это могут быть объекты, пользователи, системы и другие элементы, которые имеют отношение к вашему проекту. Лучше, если они будут напрямую соотноситься с глоссарием.
> [!NOTE]
> Если необходимо, добавьте диаграммы для визуализации связей между терминами и сущностями. Это поможет лучше понять структуру и взаимодействие элементов. Ниже представленны примеры подходящих типов диаграмм. Для удобства переноса между различными артефактами документации, диаграммы рекомендуется выполнять в редакторе [PlantUML](https://plantuml.com/en "Официальный сайт PlantUML")

### 5.1 Mindmap (Ментальная карта)

> [!TIP]
>Mindmap или интеллект-карта — это визуальный инструмент, который помогает структурировать и организовать информацию, идеи, знания и планы. Он представляет собой древовидную схему, где центральная идея окружена связанными с ней мыслями и концепциями. Это более простой, быстрый и наглядный способ сделать описание связи сущностей решения

> **Образец Mindmap**

![Mindmap](https://github.com/archdocspec/featuredocumentation/blob/main/FeatureTemplate/Assets/Mindmap.png "Образец Mindmap")

**Код диаграммы в формате PlantUML:**
<details>
  <summary>код диаграммы в PlantUML</summary>
	  
```
@startmindmap
* Сущности заказа
	* Пользователь
		* ID
		* ФИО
		* Контакты
		* Список заказов
	* Заказ
		* ID
		* Дата
		* Сумма
		* Список товаров
	* Товар
		* ID
		* Название
		* Цена
@endmindmap

```
</details>



### 5.2 ERD Diagram (Нотация Chen)

> [!TIP]
>Используйте нотацию ERD (Entity-Relationship Diagram) для представления сущностей и их взаимосвязей. Это более подробный, но при этом и сложночитаемый способ описать соотношение данных сущности.

> Подробнее о нотации https://plantuml.com/ru/er-diagram

#### 5.2.1 Связи данных в ERD

Связи данных в ERD отображаются при помощи графических символов соотношения.
Они указаны в таблице ниже

| Тип Соединения | Обозначение |
|:------------|:------------:|
|Один| |-- |
|Много| }-- |
|Один и только один| ||-- |
|Ноль и только один| |o-- |
|Один или много| }|-- |
|Ноль или много| }o-- |

> **Образец ERD Diagram (Chen)** 

![ERD CHEN](https://github.com/archdocspec/featuredocumentation/blob/main/FeatureTemplate/Assets/1-5-2-ERD-Chen.png "Образец ERD")

**Код диаграммы в формате PlantUML:**

<details>
	
  <summary>код диаграммы в PlantUML</summary>
	  
	```	  
	@startuml
	entity "Пользователь" {
  	+ID
  	+Имя
  	+Email
  	+Список заказов
	}

	entity "Заказ" {
  	+ID: int
  	+Дата: date
  	+Сумма: float
   	+Список товаров
	}
 
	entity "Заказ" {
  	+ID
  	+Название
  	+Цена
	}
 
	Пользователь  Заказ : делает
 	Пользователь -N- Заказ : делает
	@enduml
 
	```
</details>


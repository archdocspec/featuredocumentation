# Сценарии

Раздел для работы со сценариями предполагаемого решения, согласно бизнес-логике

>[!NOTE]
>Страница для шаблона списка сценариев. Представлено от 1 до N

# Макеты

>[!TIP]
>взять сценарий покупки с предусловиями - уже все зарегано, залогинено и т.п.
указать все на юз кейсе

* https://www.figma.com/design/wP2kIzn9TvjDtnS8oQztyb/E-commerce-Shop-Mobile-Wireframe-Flows--Community-?node-id=521-7861&p=f&t=9I0WhMCDbiJLhEsX-0 - EN, исчерпывающий
* https://www.figma.com/design/ZfelEWXGR73MtJ0mRy2CZK/%D0%98%D0%BD%D1%82%D0%B5%D1%80%D0%BD%D0%B5%D1%82-%D0%BC%D0%B0%D0%B3%D0%B0%D0%B7%D0%B8%D0%BD-DKY--Community-?node-id=0-1&p=f&t=ZfOovu9NwlKTputO-0 - RU, простой

## Общий USE CASE Сценариев

1
N
Все остальные

## Список сценариев

Подраздел, где будут содержаться общие данные по всем сценариям

### Список с кратким описанием

Пример списка сценариев

| Сценарии в решении | Описание сценариев |
| ----------- | ----------- |
| Сценарий 1 | Исполнение определенной логики таких-то частей бизнес-процесса, для достижения определенного результата |
| Сценарий N | Следующий по списку |
| Еще какие-то сценарии по списку | ... |

### Общая схема сценариев

Activity diagram с примером отображения всех сценариев в фиче

![image](https://github.com/user-attachments/assets/390ebe31-4bbd-4e8f-943a-937c4e3dfe8e)

### Общая sequence-диаграмма сценариев

Добавить диаграмму с общей последовательностью выполнения сценариев.
В обобщенном формате, с вербальными формулировками ИЛИ только с главными вызовами/интеграциями (если главные можно выделить).

![изображение](https://github.com/user-attachments/assets/8b048027-b8d0-496d-93ee-ba9bb428567c)

<details>
  <summary>PlantUML Code</summary>
  
  ```
  @startuml
skinparam MaxMessageSize 150

actor user
participant frontend #ivory
participant backend #azure

== Сценарий 1 ==

autonumber "<b>[Шаг ]"
user -> frontend: Ввести данные

frontend -> backend : Передать данные
backend -> frontend : OK

alt#LightSalmon Ошибка

backend -> frontend : Error

end

== Сценарий N ==

autonumber "<b>[Шаг ]"

backend -> backend: Обработка данных

alt#LightSalmon Ошибка

backend -> frontend : Ошибка
frontend -> frontend : Возникла ошибка

end

backend -> frontend : Успешно
frontend -> frontend : Данные обработаны
user -> frontend: Нажать "Ок"

== Остальные возможные сценарии ==

@enduml

  ```

</details>


### Общий макет 

Добавить ссылку/разместить макет решения с обозначением на нем сценариев.

<details>
  <summary>Источник макета</summary>
  https://www.figma.com/design/IOsJzqY4c6VPfJDN2WeeXf/Home-Interior-Design-Website-    Wireframe-(Community)?node-id=0-1&node-type=canvas&t=st3jI6blsbLjIY6x-0
https://github.com/NonameX11/TestPetDocumentationProject/blob/main/Feature%20Template/9%20-%20%D0%B4%D0%BE%D0%BF.%20%D0%BC%D0%B0%D1%82%D0%B5%D1%80%D0%B8%D0%B0%D0%BB%D1%8B.md больше ссылок на источники - тут
</details>

![изображение](https://github.com/user-attachments/assets/41e74aa6-2c19-4f05-9cc6-771332527ed5)

***


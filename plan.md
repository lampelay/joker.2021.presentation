

Доклад будет полезе для тех, кто хочет безопасно управлять зависимостями, 
а также для тех, кто разрабатывает свою библиотеку и хочет сделать её удобной и предсказуемой для пользователей.

## Тесты
  
Писать тесты обязательно. В том числе без мокирования сторонних библиотек.

## Общий BOM
  
Чтобы собрать номерки версий в одном месте для всех модулей.

- Как устроен
- Как работает `<dependencyManagement />`
- parent-модуль
- Упомянуть Spring-Boot: у них тоже есть spring-boot-starter-parent и есть BOM.

## Проверка обратной совместимости контрактов

### Java API

#### Типы совместимости

- binary

  Совместимо, когда можно в папке lib заменить стороннюю либу на новую и всё заработает.

- sources

  Совместимо, когда код компилируется при обновлении зависимости на новую.
  
Пара примеров одного и второго.
  
Ссылка на доклад [Михаил Ершов — Разработка совместимого API](https://www.youtube.com/watch?v=EgOZSr-Uc3w).

#### Инструменты

- japi-compliance-checker

  Написано на perl.
  Последний релиз в начале 2018 года. Разработка продолжается.
  В нашей практике не отследил обновления, связанные с параметризованными классами (Generics).

- revapi

  Написан на java, вызывается из Java.
  Может анализировать не только Java.
  Последние обновления очень свежие.

- japicmp

  Написано на Java.
  Последние обновления 

- sigtest // TODO описать возможности, удобство и развитие

### Spring context

// TODO какие проблемы при поднятии контекста бывают, какие мы встречали
- xsd (для чистого spring)

  [SOA Model (predic8)](https://github.com/membrane/soa-model)

- spring-configuration-metadata.json (для Spring-Boot)

  Файл генерируется при подключении плагина **spring-boot-configuration-processor**
  и подсказывает IDE, какие свойства вносить в **application.properties**.
  // TODO перечислить правила, по которым проверяем

Ссылка на доклады:
- [Руслан Черемин — Тестирование конфигурации для Java-разработчиков: практический опыт](https://www.youtube.com/watch?v=Tk_nmV-mWOA)
- [Андрей Сатарин — Как проверить систему, не запуская её](https://www.youtube.com/watch?v=SLZNVSb5vfY)

## Как ещё обезопасить себя

- завязываться только на API-части (интерфейсы) библиотек
  - API пакет внутри либы
  - отдельный API jar
  - то, что автор библиотеки обозначил как API в документации

- смотреть на semver (Semantic Versioning), но полностью на него не полагаться. 

  В пример привести номер версий Java и TypeScript, у которого на первый взгляд semver, но на самом деле нет.

- Последняя версия – не всегда самая лучшая. Пример – macOS (на Catalina перестал работать git) или Windows.

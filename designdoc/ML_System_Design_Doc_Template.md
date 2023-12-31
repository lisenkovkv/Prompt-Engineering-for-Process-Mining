
## Дизайн ML системы - PE4PM (Prompt Engineering for Process Mining)

*Шаблон ML System Design Doc от телеграм-канала [Reliable ML](https://t.me/reliable_ml)*   

- Рекомендации по процессу заполнения документа (workflow) - [здесь](https://github.com/IrinaGoloshchapova/ml_system_design_doc_ru/blob/main/ML_System_Design_Doc_Workflow.md).  
- Детальный доклад о том, что такое ML System Design Doc и о том, как, когда и зачем его составлять - [тут](https://www.youtube.com/watch?v=PW9TGNr1Vqk).
    
> ## Термины и пояснения
> - Итерация - это все работы, которые совершаются до старта очередного пилота  
> - БТ - бизнес-требования 
> - EDA - Exploratory Data Analysis - исследовательский анализ данных  
> - `Product Owner`,  `Data Scientist`, `Process Mining Analyst` - роли, которые заполняют соответствующие разделы 
> - Бизнес-процесс - многократно повторяющаяся, логически связанная последовательность действий, направленная на создание ценности и формирование результата.
> - Process mining - интеллектуальный анализ бизнес-процессов, направленный на построение исчерпывающего и объективного видения процессов на основе фактических данных, который позволяет изучать фактическое протекание отдельных процессов, чтобы получить представление о том, как работает система в целом.
> - Экземпляр процесса (кейс) - бизнес-сущность, которая проходит через все этапы процесса и однозначнео определяет выполняемсый процесс.
> - Шаг процесса (активность) - одно из однозначно определяемых действий в цепочке, относящейся к экземпляру процесса.
> - Путь процесса - полная совокупность последовательных действий, относящихся к одному экземпляру процесса, имеющая начало и конец.
> - Метрики процесса - некторые вычисляемые характеристики, позволяющие делать вывод о протекании процесса и (или) сравнивать различные экземпляры процесса между собой.

### 1. Цели и предпосылки 
#### 1.1. Зачем идем в разработку продукта?  

- <b>Бизнес-цель</b>

  В настоящее время, для проведения Process Mining исследований требуется глубокое знание методологии, опыт работы с инструментами и большое количество времени и ресурсов. В связи с этим, одной из основных бизнес-целей создания помощника Process Mining исследователя является <b>снижение порога входа в область Process Mining и повышение эффективности проведения исследований</b>. Разрабатываемый помощник должен стать инструментом, который поможет как профессионалам, так и новичкам без технических навыков в проведении исследований и уменьшении трудозатрат на данную деятельность.

- <b>Почему станет лучше, чем сейчас, от использования ML</b>

    Использование ML в разработке позволит значительно улучшить процесс проведения исследований. ML алгоритмы могут способствовать автоматическому обнаружению шаблонов в анализируемых процессах, выявлению возможных проблем и нарушений, а также автоматически определять эффективность процесса и потенциальные области оптимизации. Это позволит исследователям сосредоточиться на более высокоуровневых задачах и ускорит процесс исследования.
  
- <b>Что будем считать успехом итерации с точки зрения бизнеса</b>

    Успешной итерацией с точки зрения бизнеса будет считаться достижение следующих результатов:

    - <b>Снижение времени и ресурсов, затрачиваемых на проведение Process Mining исследования.</b> Уменьшение порога входа и упрощение процесса исследований должны привести к сокращению времени, необходимого для получения ценной информации и анализа процессов.

    - <b>Улучшение точности и надежности исследований.</b> Помощник должен обеспечивать высокую точность в определении шаблонов, прогнозировании проблем и нарушений, а также в оценке процессов. Это позволит своевременно обнаруживать неэффективности и проблемы в процессах.

    - <b>Увеличение доступности Process Mining исследований.</b> Помощник должен быть доступен и прост в использовании для широкого круга пользователей, включая новичков и лиц без технических навыков. Это позволит привлечь больше людей к исследованию и оптимизации процессов и обеспечит более широкое использование инструментов Process Mining.

    Общим успехом всех итераций помощника Process Mining исследователя будет улучшение эффективности, точности и доступности процесса исследований, а также повышение уровня понимания и оптимизации процессов для бизнеса.

#### 1.2. Бизнес-требования и ограничения  

- Краткое описание БТ и ссылки на детальные документы с бизнес-требованиями `Product Owner`  
- Бизнес-ограничения `Product Owner`  
- Что мы ожидаем от конкретной итерации `Product Owner`. 
- Описание бизнес-процесса пилота, насколько это возможно - как именно мы будем использовать модель в существующем бизнес-процессе? `Product Owner`

- Пилотный проект будет включать в себя следующие этапы:

    - <b>Сбор и предварительная обработка данных</b>:
    Первым шагом будет сбор данных о ходе выполнения бизнес-процесса. Эти данные могут включать в себя логи действий пользователей, временные метки, результаты выполнения задач и другую сопутствующую информацию. Для предварительной обработки данных будут применены методы для удаления шума, объединения и агрегации данных.
    
    
        Ограничением на данном этапе является использование данных о процессе, взятых из открытых источников <i>(соревнование BPIC..., ссылка)</i>. В этом случае в сборе данных нет необходимости, однако, остается задача их предварительной обработки.

    - <b>Тренировка и создание ML-моделей</b>:
    На основе предобработанных данных будут созданы и обучены ML-модели с целью обнаружения шаблонов в процессах, предсказания возможных проблем и нарушений, а также оценки эффективности процессов. Модели могут включать в себя алгоритмы классификации, регрессии и кластеризации, а также нейронные сети или другие подходящие модели для данной задачи.
    
    
        Ограничением на данном этапе является отсутствие временных и аппаратных ресурсов для дообучения модели на собственном датасете. В связи с этим для реализации пилотного проекта будет использоваться существующяя большая языковоаяй модель <i>(LLM - название модели и ссылка)</i>.

    - <b>Интеграция ML-моделей в бизнес-процесс</b>:
    После создания ML-моделей они будут интегрированы в существующий бизнес-процесс. Например, модель может автоматически анализировать логи действий пользователей в реальном времени, определять возможные нарушения и предлагать рекомендации по оптимизации процесса. Модель также может генерировать отчёты и визуализации для более наглядного представления результатов анализа.
    
    
        Ограничением на данном этапе является использование инструмента в "пассивном" режиме - в обработку будут подаваться заранее подготовленые датасеты в формате csv или xlsx, либо специальным образом подготовленные prompt-тексты, содержащие в себе некоторую агрегированную информацию об анализируемом процессе.

    - <b>Оценка эффективности и оптимизация процесса</b>:
    В рамках пилотного проекта будет проведена оценка эффективности ML-моделей и их воздействия на бизнес-процесс. Будут учтены показатели, такие как снижение времени выполнения задач, обнаружение и предотвращение нарушений, улучшение качества выполнения процесса и снижение затрат. Полученные результаты будут использованы для оптимизации и улучшения ML-моделей и стратегии их применения.
    
    
        Ограничением на данном этапе является получение некоторого понятного и качественного описания бизнес-процесса на основе исходных данных. Полученные при помощи модели предложения по оптимизации процесса в рамках пилотного проекта будут рассматриваться, скорее, как некоторый бонус, а не метрика успешности проекта.

Таким образом, пилотный проект будет основан на использовании большой языковой модели для автоматического описания бизнес-процесса и, по возможности, получения предложений по оптимизации его эффективности. Целью проекта будет улучшение производительности, сокращение затрат и повышение качества выполнения анализа бизнес-процесса путем разработки соответствующего программного инструмента.

    - <b>Что считаем успешным пилотом? Критерии успеха и возможные пути развития проекта `Product Owner`<b>:
    
    
    Успех пилотного проекта можно определить по следующим критериям:

    1. <b><i>Автоматическое описание и анализ бизнес-процесса:</i></b> ML-модель должна успешно анализировать предоставленные данные и верно описывать основные этапы и ход выполнения процесса.

    2. <b><i>Предложения по оптимизации процесса:</i></b> В идеале, модель должна предлагать реалистичные и эффективные рекомендации по оптимизации процесса на основе полученных данных.

    3. <b><i>Улучшение производительности:</i></b> Пилотный проект должен снижать время выполнения задач, находить и предотвращать возможные нарушения, а также улучшать качество выполнения процесса.

    4. <b><i>Снижение затрат:</i></b> Модель должна помочь снизить затраты на выполнение бизнес-процесса путем идентификации эффективных стратегий и рекомендаций.

    5. <b><i>Положительная обратная связь от пользователей:</i></b> Отзывы пользователей о пилотном проекте должны быть положительными и отражать удовлетворенность результатами работы модели.
    
    
    Возможные пути развития проекта:

    1. <b><i>Расширение датасета:</i></b> Для улучшения точности модели и ее способности предсказывать возможные нарушения и оптимизационные решения, можно расширить собранные данные, добавив новые сценарии выполнения процессов и их вариации.

    2. <b><i>Оптимизация модели:</i></b> С использованием большей вычислительной мощности и больших датасетов можно дообучить или улучшить модель для лучшего понимания и описания бизнес-процесса.

    3. <b><i>Интеграция с существующей системой управления процессами:</i></b> После успешного завершения пилотного проекта можно интегрировать разработанный программный инструмент с существующими системами управления бизнес-процессами для автоматической оптимизации и анализа процессов.

    4. <b><i>Масштабирование и применение на других бизнес-процессах:</i></b> Если пилотный проект будет успешным, его инструменты и подходы могут быть применены на других бизнес-процессах в организации, что поможет повысить эффективность работы и снизить общие затраты.

    5. <b><i>Дальнейшая оптимизация и улучшение результатов:</i></b> Результаты пилотного проекта и обратная связь пользователей могут помочь идентифицировать дополнительные улучшения и оптимизации для более успешной реализации проекта в будущем.

#### 1.3. Что входит в скоуп проекта/итерации, что не входит   

- На закрытие каких БТ подписываемся в данной итерации `Data Scientist`   
- Что не будет закрыто `Data Scientist`  
- Описание результата с точки зрения качества кода и воспроизводимости решения `Data Scientist`  
- Описание планируемого технического долга (что оставляем для дальнейшей продуктивизации) `Data Scientist`  

#### 1.4. Предпосылки решения  

- Описание всех общих предпосылок решения, используемых в системе – с обоснованием от запроса бизнеса: какие блоки данных используем, горизонт прогноза, гранулярность модели, и др. `Data Scientist`  

### 2. Методология `Data Scientist`     

#### 2.1. Постановка задачи  

- Что делаем с технической точки зрения: рекомендательная система, поиск аномалий, прогноз, оптимизация, и др. `Data Scientist` 

Основной задачей с технической точки зрения является разработка и реализация алгоритмов дообучения модели LLM и её внедрение в систему для создания разговорного агента, способного обрабатывать запросы пользователей в области Process Mining. В рамках проекта также можно выделить несколько подклассов задач для разработки:

1. **Чат-бот и вопросно-ответная система:** Помощник, обученный на основе LLM, обрабатывает запросы пользователя на естественном языке и предоставляет соответствующие ответы.

2. **Извлечение информации (Information Extraction):** Когда помощник анализирует запросы и логи событий, он извлекает информацию и детали, которые необходимы для формулирования SQL-запросов.

3. **Языковая модель (Language Modeling):** В данном случае, дообучение LLM с открытым исходным кодом на специфических данных для области Process Mining.

4. **Обработка последовательностей:** Помощник анализирует последовательности запросов и событий, чтобы понимать порядок и взаимосвязь между ними.

5. **Автоматическое формирование запросов (Query Generation):** Помощник формирует SQL-запросы автоматически на основе запросов пользователя.

6. **Диалоговая система (Dialog System):** Помощник взаимодействует с пользователями в режиме диалога, обрабатывая их запросы и предоставляя ответы, что является ключевой частью диалоговых систем.


#### 2.2. Блок-схема решения  

![img.jpg](https://github.com/lisenkovkv/Prompt-Engineering-for-Process-Mining/blob/lebedkova_designdoc/designdoc/img.jpg)

#### 2.3. Этапы решения задачи `Data Scientist`  

1. **Подготовка данных (Data Preparation):**
   - На данном этапе должно быть следующее:
       - Данные содержат обязательные атрибуты, необходимые для проведения Process Mining исследования (экземпляр, операция, временная метка начала/конца операции). Данные должны содержать как можно больше разнообразных кейсов неэффективности, поиск которых осуществляется в рамках такого исследования. (На этапе Baseline предполагается использование открытого датасета BPIC 2019).
   - Результаты:
       - Исходные данные для анализа и обучения LLM модели в формате, пригодном для обработки.

2. **Анализ данных (Data Analysis):**
   - На данном этапе должно быть следующее:
       - Анализ данных с целью выявления основных шаблонов запросов пользователей, а также SQL-запросов, отвечающих на запросы пользователей.
       - Проведение интерпретации результатов выполнения SQL-запросов в виде щаблона возможных ответов модели на запрос пользователя.
   - Результаты:
       - Сформирован перечень шаблонов SQL-запросов и запросов пользователей.
       - Для каждого шаблона SQL сформулирована интрепретация и возможный корректный ответ модели на её основе.
   - Метрики успешности этапа:
       - Выборка шаблонных запросов и ответов модели охватывает большую часть классических кейсов неэффективности процесса.

3. **Подготовка обучающих данных (Training Data Preparation):**
   - На данном этапе должно быть следующее:
       - **Baseline:**
       - Обучающая выборка, содержащая запросы пользователей и соответствующие SQL-запросы для базовой модели. `Здесь же должно быть определение горизонта и гранулярности данных`

       - **MVP:**
       - Расширенная обучающая выборка, включающая разнообразные запросы и SQL-запросы.
       - База данных с запросами и ответами, полученными от Baseline модели, с оценкой качества ответов.
   - Результат:
       - Сформированная выборка для обучения. Целевая переменная - ответ модели на запрос пользователя.

4. **Обучение базовой LLM модели (Baseline LLM Training):**
   - На данном этапе должно быть следующее:
       - Загрузка предварительно обученной модели LLM и выполнение дообучения модели на данных для понимания запросов в терминах Process Mining `необходимо подробно описать технику обучения`.
   - Результат:
       - Обученная LLM модель.

5. **Тестирование и валидация (Testing and Validation):**
    - На данном этапе должно быть следующее:
       - **Baseline:**
       - Оценка качества модели на базовых запросах.
       - Значения метрик BLEU, ROUGE и экспертной оценки.`необходимо определить перечень метрик и их целевые значения`

       - **MVP:**
       - Оценка качества модели на разнообразных запросах, включая сложные сценарии.
       - Сравнение метрик с Baseline версией модели.
    - Результат:
        - Определены значения метрик после обучения модели.
    - Метрики успешности этапа:
        - Каждая из рассчитанных метрик удовлетворяет соответствующим целевым значениям.

6. **Обратная связь и коррекция (Feedback and Refinement):**
    - На данном этапе должно быть следующее:
       - Документированная обратная связь от экспертов и пользователей.
       - Описание внесенных изменений в модель и данных на основе обратной связи.
       - Внесение необходимых корректировок (возможно, возврат на предыдущие этапы)
    - Результат:
       - В модель внесены корректировки, согласно ОС от экспертов и пользователей.
    - Метрики успешности этапа:
       - Экспертная оценка, удовлетворённость пользователей.

7. **Формирование отчёта (Creation Report):**
   - На данном этапе должно быть следующее:
       - Создание отчёта, содержащего оценку производительности модели и качества результатов.
       - Сформирован перечень рекомендаций по доработке модели или дальнейшему развитию проекта.
       - Демонстрация отчёта бизнес-заказчику.
   - Результат:
       - Получена обратная связь от бизнес-заказчика о статусе проекта.
   - Метрики успешности этапа:
       - Удовлетворённость бизнес-заказчика, полное или частичное выполнение бизнес-цели проекта.

8. **Пилот (Pilot):**
   - На данном этапе должно быть следующее:
       - Подготовка инфраструктуры для запуска пилотной версии модели.
       - Документирование планов и результатов пилотного запуска.
   - Результат:
       - Запуск пилота.
   - Метрики успешности этапа:
       - Достижение ранее расчитанных целевых значений метрик, удовлетворённость пользователей, экспертов и бизнес-заказчика.
  
### 3. Подготовка пилота  
  
#### 3.1. Способ оценки пилота  
  `Требуется добавить описание дизайна пилота`
- Будут использоваться следующие спосбы оценки пилота:
   - Сравнение с Baseline (по заранее выбранным метрикам)
   - Сбор обратной связи и оценок от экспертов
   - Сбор и анализ обратной связи от пользователей с различным уровнем знаний в Process Mining.
  
#### 3.2. Что считаем успешным пилотом  
  
Формализованные в пилоте метрики оценки успешности `Product Owner`   
  
#### 3.3. Подготовка пилота  
  
- Что можем позволить себе, исходя из ожидаемых затрат на вычисления. Если исходно просчитать сложно, то описываем этап расчетов ожидаемой вычислительной сложности на эксперименте с бейзлайном. И предусматриваем уточнение параметров пилота и установку ограничений по вычислительной сложности моделей. `Data Scientist` 

### 4. Внедрение `для production систем, если требуется`    

> Заполнение раздела 4 требуется не для всех дизайн документов. В некоторых случаях результатом итерации может быть расчет каких-то значений, далее используемых в бизнес-процессе для пилота.  
  
#### 4.1. Архитектура решения   
  
- Блок схема и пояснения: сервисы, назначения, методы API `Data Scientist`  
  
#### 4.2. Описание инфраструктуры и масштабируемости 
  
- Какая инфраструктура выбрана и почему `Data Scientist` 
- Плюсы и минусы выбора `Data Scientist` 
- Почему финальный выбор лучше других альтернатив `Data Scientist` 
  
#### 4.3. Требования к работе системы  
  
- SLA, пропускная способность и задержка `Data Scientist`  
  
#### 4.4. Безопасность системы  
  
- Потенциальная уязвимость системы `Data Scientist`  
  
#### 4.5. Безопасность данных   
  
- Нет ли нарушений GDPR и других законов `Data Scientist`  
  
#### 4.6. Издержки  
  
- Расчетные издержки на работу системы в месяц `Data Scientist`  
  
#### 4.5. Integration points  
  
- Описание взаимодействия между сервисами (методы API и др.) `Data Scientist`  
  
#### 4.6. Риски  
  
- Описание рисков и неопределенностей, которые стоит предусмотреть `Data Scientist`   
  
> ### Материалы для дополнительного погружения в тему  
> - [Шаблон ML System Design Doc [EN] от AWS](https://github.com/eugeneyan/ml-design-docs) и [статья](https://eugeneyan.com/writing/ml-design-docs/) с объяснением каждого раздела  
> - [Верхнеуровневый шаблон ML System Design Doc от Google](https://towardsdatascience.com/the-undeniable-importance-of-design-docs-to-data-scientists-421132561f3c) и [описание общих принципов его заполнения](https://towardsdatascience.com/understanding-design-docs-principles-for-achieving-data-scientists-53e6d5ad6f7e).
> - [ML Design Template](https://www.mle-interviews.com/ml-design-template) от ML Engineering Interviews  
> - Статья [Design Documents for ML Models](https://medium.com/people-ai-engineering/design-documents-for-ml-models-bbcd30402ff7) на Medium. Верхнеуровневые рекомендации по содержанию дизайн-документа и объяснение, зачем он вообще нужен  
> - [Краткий Canvas для ML-проекта от Made with ML](https://madewithml.com/courses/mlops/design/#timeline). Подходит для верхнеуровневого описания идеи, чтобы понять, имеет ли смысл идти дальше.  

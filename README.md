# Расчётно-пояснительная записка

## Тема и целевая аудитория

В качестве сервиса для проектирования был выбран **iCloud** - облачное хранилище и синхронизационный сервис. Данный сервис отвечает требованиям к теме:

- **Имеет реальные аналоги**, доказывающие существование рыночной ниши — Google Drive, Dropbox, Microsoft OneDrive.
- **Аудитория сервиса** превышает 500 миллион активных пользователей в месяц.
  
| Регион                 | Количество пользователей |
|------------------------|--------------------------|
| **США**                | 119 млн                  |
| **Китай**              | 125 млн                  |
| **Европа** (5 стран)   | 56.7 млн                 |
| **Всего по миру**      | 850 млн                  |

Эти данные основаны на источниках: [Worldmetrics](https://worldmetrics.org/apple-icloud-statistics/) и [ChargeASAP](https://chargeasap.com/blogs/news/breakdown-of-iphone-users-by-country).
- **Имеет сложную архитектуру**.

## Функционал

Ключевой функционал для данного сервиса:

1. **Облачное хранилище данных**
   - Возможность загружать, хранить и управлять файлами в облаке, с доступом из любой точки мира. **Поддержка синхронизации** данных между устройствами в режиме реального времени. При включении функции Фото iCloud оригиналы фото автоматически начинают храниться в облаке, что позволяет экономить память устройства.

2. **Синхронизация данных между устройствами**
   - Автоматическая синхронизация контактов, фотографий, заметок, документов и других данных между устройствами Apple. Пользователи могут продолжать работу с одного устройства на другом без необходимости переносить данные вручную.

3. **Система резервного копирования**
   - Возможность создания резервных копий данных, включая настройки устройств, файлы и приложения. **Автоматическое резервное копирование** происходит при подключении устройства к Wi-Fi и зарядному устройству.

4. **Совместная работа и доступ к файлам**
   - Поддержка **общего доступа к файлам** и папкам с другими пользователями iCloud, например, из семьи пользователя, с возможностью редактирования и комментирования. Интеграция с приложениями для совместной работы, такими как Pages, Numbers, и Keynote.

5. **Безопасность и шифрование данных**
   - **Шифрование данных** как на уровне хранения, так и при передаче данных между устройствами и облаком гарантирует высокий уровень защиты данных пользователей.

## Сокращение до MVP

Для создания MVP (минимально жизнеспособного продукта) iCloud можно урезать функционал до следующих ключевых функций:

1. **Регистрация и аутентификация** (с поддержкой авторизации с нескольких устройств).
2. **Облачное хранилище данных** (с базовыми функциями загрузки и хранения файлов).
3. **Синхронизация данных между устройствами** (ограничена основными данными, такими как контакты и фотографии).
4. **Система резервного копирования** (с поддержкой резервного копирования основных данных устройства).
5. **Совместная работа и доступ к файлам** (с упрощенной функцией общего доступа без сложных прав редактирования).

## Продуктовые метрики

1. **Месячная аудитория (MAU)**: В 2023 году количество пользователей iCloud составляет более 850 миллионов активных пользователей по всему миру.
2. **Дневная аудитория (DAU)**: Примерно 119 млн пользователей в США и 125 млн в Китае, что позволяет предполагать значительное количество ежедневных активных пользователей, ориентировочно 10-20% от MAU, т.е. около 85-170 млн.
3. **Средний размер хранилища пользователя**: iCloud предлагает тарифные планы от 50GB до 12TB на пользователя. У 80% пользователей бесплатный тарифный план - 5GB. у 13% - 50GB, 5% - 200GB, 1% - 2TB, <1% - 6TB, <1% - 12TB, Средний объем хранилища может составлять около 50GB, в зависимости от типа пользователей [Apple Support](https://support.apple.com/en-us/108047) [Statista](https://www.statista.com/topics/1695/cloud-computing/).

Так как подписка ежемесечная, то проценты и количество пользователей вычисляются на основе MAU:

| Тарифный план   | Процент пользователей      | Количество пользователей |
|-----------------|----------------------------|--------------------------|
| 5GB             | 90%                        | 765 млн                  |
| 50GB            | 7%                         | 59.5 млн                 |
| 200GB           | 2.9%                       | 24.65 млн                |
| 2TB             | 0.09%                      | 0.765 млн                |
| 6TB             | 0.009%                     | 0.0765 млн               |
| 12TB            | 0.001%                     | 0.0085 млн               |

Подсчитаем среднее значение на пользователя: 
(765 млн * 5 GB + 59.5 млн * 50 GB + 24.65 млн * 200 GB + 0.765 млн * 2,048 GB + 0.0765 млн * 6,144 GB + 0.0085 млн * 12,288 GB) / 850 млн =  13,871.184 млн GB / 850 млн = 16.31904 GB, что можно округлить до 17 GB. 

Итого:
| Метрика                                   | Значение                   |
|-------------------------------------------|----------------------------|
| Месячная аудитория (MAU)                  | 850 млн                    |
| Дневная аудитория (DAU)                   | 85-170 млн                 |
| Средний размер хранилища на пользователя  | 17 GB                      |

Основываясь на личном опыте и опыте знкомых, я составил таблицу:

| Тип запроса                              | Среднее количество действий в день на пользователя |
|------------------------------------------|----------------------------------------------------|
| Аутентификация                           | 0.01                                               |
| Аутентификация (по куке)                 | 1                                                  |
| Загрузка файлов на облако                | 1                                                  |
| Просмотр/скачивание файлов               | 2                                                  |
| Удаление файлов                          | 0.2                                                |
| Создание/доступ к общим папкам/файлам    | 0.01                                               |
| Синхронизация данных (контакты, фото)    | 3                                                  |
| Резервное копирование                    | 0.02                                               |


## Технические метрики

### Размер хранения в разбивке по типам данных для iCloud для пользователя с платным тарифом

| Тип данных           | Количество файлов на пользователя | Средний размер файла | Общий размер на пользователя | Общий размер для 85 млн пользователей (DAU) |
|----------------------|-----------------------------------|----------------------|------------------------------|---------------------------------------------|
| Фотографии           | 1,500                             | 5 MB                 | 7.5 GB                       | ~637,500 ТБ                                 |
| Видео                | 200                               | 100 MB               | 30 GB                        | ~2,550,000 ТБ                               |
| Документы (PDF, Word) | 50                               | 1 MB                 | 0.05 GB                      | ~4,250 ТБ                                   |
| Контакты              | 1,000                            | 2 KB                 | 0.002 GB                     | ~170 ТБ                                     |
| Резервные копии       | -                                | -                    | 10 GB                        | ~850,000 ТБ                                 |
| Прочие файлы          | 100                              | 100 MB               | 10 GB                        | ~850,000 ТБ                                 |

**Примечание:**
- **Фотографии** и **видео** — значительная часть объема данных, так как большинство пользователей хранят фото и видео с мобильных устройств.
- **Документы** составляют меньшую часть по объему, но они многочисленны.
- **Контакты** занимают минимальное место, но их количество велико.
- **Резервные копии** имеют значительный вес из-за большого количества данных, сохраняемых для каждого устройства.
- **Прочие файлы** могут включать такие данные, как заметки, приложения, или другие типы файлов.

**Общий объем хранилища iCloud** может составлять около 850 млн * 17 GB = **14.45 EB** (эксабайт)

### RPS

**RPS = DAU * количесво действий на пользователя / 86,400**

| Тип запроса                           | RPS (DAU = 85 млн)     | RPS (Пиковый, DAU = 170 млн) |
|---------------------------------------|----------|---------------|
| Аутентификация                        | 10       | 20            |
| Аутентификация (по куке)              | 984      | 1,968         |
| Загрузка файлов на облако             | 984      | 1,968         |
| Просмотр/скачивание файлов            | 1,968    | 3,936         |
| Удаление файлов                       | 197      | 394           |
| Создание/доступ к общим папкам/файлам | 10       | 20            |
| Синхронизация данных (контакты, фото) | 2,951    | 5,902         |
| Резервное копирование                 | 20       | 40            |
| **Итого**                             | **7,124** | **14,248**    | 


### Сетевой трафик
**Таблица трафика на один запрос по каждому действию:**

| Тип запроса                           | Входящий трафик (КБ) | Исходящий трафик (КБ) | Примечание                                          |
|---------------------------------------|----------------------|-----------------------|-----------------------------------------------------|
| Аутентификация                        | 2 КБ                 | 8 КБ                  | Отправка данных для входа и получение токена сессии.|
| Аутентификация по куке                | 1 КБ                 | 5 КБ                  | Обновление сессии без ввода данных.                 |
| Загрузка файла (средний файл 10 МБ)   | 10,240 КБ            | 5 КБ                  | В облако.                                            |
| Скачивание файла (средний файл 10 МБ) | 5 КБ                 | 10,240 КБ             | Из облака.                                           |
| Удаление файла                        | 5 КБ                 | 5 КБ                  | -                                                   |
| Создание/доступ к общим папкам/файлам | 5 КБ                 | 10 КБ                 | Создание файлов и настройка доступа.                 |
| Синхронизация данных                  | 50 КБ                | 50 КБ                 | Контакты, календари, фото.                           |
| Резервное копирование (средний объем) | 102,400 КБ           | 5 КБ                  | Создание резервной копии некоторых данных устройства (~100 МБ)|

**Примечания к таблице:**

1. **Аутентификация** — небольшой объем данных, так как происходит передача токенов или данных авторизации.
2. **Загрузка и скачивание файлов** — основные операции, которые занимают значительную часть трафика, особенно для мультимедийных файлов (фото, видео). Например, файл размером 10 МБ.
3. **Синхронизация данных** — небольшие, но частые запросы, так как происходит обмен информацией о состоянии данных (например, изменение контактов или добавление фотографий).
4. **Резервное копирование** — значительный входящий трафик, связанный с отправкой данных на сервер, особенно для больших файлов резервных копий (около 100 МБ за один бэкап).

### Таблица 1: Пиковое потребление в течение суток (Гбит/с)

Для каждого типа запроса рассчитаем пиковую сетевую нагрузку с учетом **RPS** (запросов в секунду) и трафика на один запрос.

| **Тип запроса**                           | **RPS (Пиковый)** | **Входящий трафик (Гбит/с)** | **Исходящий трафик (Гбит/с)** | **Общий трафик (Гбит/с)** |
|-------------------------------------------|-------------------|------------------------------|-------------------------------|---------------------------|
| Аутентификация                            | 20                | 0.00032                      | 0.00128                       | 0.0016                    |
| Аутентификация (по куке)                  | 1,968             | 0.0157                       | 0.0787                        | 0.0944                    |
| Загрузка файлов                           | 1,968             | 161.22                       | 0.0787                        | 161.2987                  |
| Скачивание файлов                         | 3,936             | 0.1574                       | 322.44                        | 322.5974                  |
| Удаление файлов                           | 394               | 0.0157                       | 0.0157                        | 0.0314                    |
| Создание/доступ к общим папкам/файлам     | 20                | 0.0004                       | 0.0008                        | 0.0012                    |
| Синхронизация данных (контакты, фото)     | 5,902             | 2.36                         | 2.36                          | 4.72                      |
| Резервное копирование                     | 40                | 3.28                         | 0.00032                       | 3.28032                   |
| **Итого**                                 | **14,248**        | **167**                      | **324**                       | **491**                   |

### Таблица 2: Суммарный суточный трафик (Гбайт/сутки)

Для каждого типа запроса рассчитаем суммарный трафик за сутки с учетом **RPS** (пиковое) и объема данных на один запрос.

| **Тип запроса**                           | **RPS (Пиковый)** | **Входящий трафик (Гбайт/сутки)** | **Исходящий трафик (Гбайт/сутки)** | **Общий трафик (Гбайт/сутки)** |
|-------------------------------------------|-------------------|-----------------------------------|------------------------------------|--------------------------------|
| Аутентификация                            | 20                | 3.456                             | 12.574                             | 16                             |
| Аутентификация (по куке)                  | 1,968             | 169.56                            | 849.96                             | 1,019.52                       |
| Загрузка файлов                           | 1,968             | 1,741,176                         | 849.96                             | 1,742,025.96                   |
| Скачивание файлов                         | 3,936             | 1,699.92                          | 3,482,352                          | 1,001,554.048                  |
| Удаление файлов                           | 394               | 134.784                           | 134.784                            | 3,484,051.92                   |
| Создание/доступ к общим папкам/файлам     | 20                | 4.32                              | 8.64                               | 12.96                          |
| Синхронизация данных (контакты, фото)     | 5,902             | 25,488                            | 25,488                             | 50,976                         |
| Резервное копирование                     | 40                | 354,816                           | 1.728                              | 354,817.728                    |
| **Итого**                                 | **14,248**        | **2,098,030**                     | **3,509,698**                      | **5,607,728**                  |

### Выводы:
- **Пиковый сетевой трафик** составляет около **500 Гбит/с**.
- **Суммарный суточный трафик** составляет около **5.6 Пбайт/сутки**.

## Глобальная балансировка нагрузки для iCloud

1. **Функциональное разбиение по доменам**  
   Для iCloud балансировка нагрузки выполняется по доменам, связанным с конкретными функциями (например, хранение файлов, синхронизация, работа с почтой). Это позволяет разграничить ключевые функции по инфраструктуре и улучшить их производительность:
  - **`files.icloud.com`** – используется для доступа к файлам в iCloud Drive. Этот домен обслуживает запросы, связанные с загрузкой, хранением и синхронизацией файлов пользователей.
   
  - **`photos.icloud.com`** – отвечает за хранение и управление фотографиями в iCloud Photos. Запросы, связанные с доступом, синхронизацией и загрузкой фотографий, обрабатываются через этот домен.
   
  - **`mail.icloud.com`** – домен для работы с почтовым сервисом iCloud Mail. Все операции, связанные с отправкой, получением и управлением электронной почтой, происходят через этот домен.
   
  - **`calendar.icloud.com`** – домен для управления календарями и синхронизации событий между устройствами, используя сервис iCloud Calendar.
   
  - **`contacts.icloud.com`** – используется для хранения и синхронизации контактов через iCloud Contacts. Все запросы, связанные с обновлением и доступом к контактам, проходят через этот домен.
   
  - **`findmy.icloud.com`** – отвечает за работу функции "Найти iPhone/iPad" (Find My). Этот домен обслуживает запросы на отслеживание и управление потерянными устройствами.
   
  - **`backup.icloud.com`** – используется для управления резервными копиями устройств. Включает как создание, так и восстановление резервных копий через iCloud Backup.
   
  - **`keychain.icloud.com`** – отвечает за синхронизацию паролей и других данных из "Связки ключей iCloud" (iCloud Keychain), обеспечивая защиту и доступ к учетным данным на всех устройствах пользователя.

  - **`notes.icloud.com`** – этот домен обрабатывает запросы, связанные с синхронизацией и управлением заметками через iCloud Notes.

  - **`reminders.icloud.com`** – отвечает за синхронизацию и доступ к напоминаниям через сервис iCloud Reminders.

  - **`settings.icloud.com`** – используется для синхронизации настроек между устройствами пользователя, что обеспечивает унифицированный опыт использования разных устройств с iCloud.

Такое разбиение по доменам позволяет разделить функциональные нагрузки между разными компонентами системы, облегчая управление и масштабирование различных сервисов iCloud.

2.  **Расположение дата-центров**
![DC apple](https://github.com/user-attachments/assets/de9c0fc7-dd14-46ba-ba6e-48635a852c9e)
![DC apple USA](https://github.com/user-attachments/assets/c1846db3-8104-403b-8b55-c89579f702b7)
  - **Мейден, Северная Каролина, США:** Это один из крупнейших центров обработки данных Apple площадью более 1 миллиона квадратных футов. Играет важную роль в работе iCloud.
  - **Рино, штат Невада, США:** дата-центр Apple в Рино со временем расширился и обеспечивает большую часть трафика iCloud, особенно в западной части США.
  - **Меса, штат Аризона, США:** этот центр служит глобальным командным центром данных и логистическим узлом для управления операциями с данными Apple по всему миру.
  - **Прайнвилл, штат Орегон, США:** еще один крупный объект, поддерживающий iCloud и другие сервисы Apple.
  - **Вауки, штат Айова, США:** этот центр является одним из самых новых и обслуживает значительный объем трафика для центральных регионов США.
  - **Выборг, Дания:** Первый европейский центр обработки данных Apple, ориентированный на предоставление услуг европейским пользователям с низкой задержкой.
  - **Голуэй, Ирландия:** Поддержка сервисов iCloud по всей Европе.
  - **Гуйчжоу и Уланкаб, Китай:** Эти центры играют важную роль в обслуживании пользователей Apple в Китае и отвечают местным законам о суверенитете данных.


3.  **Обоснование расположения дата-центров**
   Apple размещает свои дата-центры стратегически для минимизации задержек (latency) и улучшения пользовательского опыта. Основные метрики:
   - **Задержка**: Чем ближе дата-центр к пользователю, тем ниже задержка, что особенно важно для синхронизации данных и облачного хранения.
   - **Надежность**: Apple распределяет дата-центры по регионам для повышения отказоустойчивости. Например, на одни только США приходится 6 крупных Дата Центров.
   - **Законы о данных**: Важный фактор, так как законодательство некоторых стран требует хранения данных пользователей внутри страны. Например, данные китайских пользователей хранятся в местных дата-центрах из-за законодательства о персональных данных.
   - **Экономическая выгода**: Компания старается сэкномить деньги на налогах, поэтому выбираются страны с выгодным налоговым законодательством, непример, Ирландия.
     
4.  **Распределение запросов по ДЦ**
  Распределение запросов зависит от физической близости пользователя к определённому дата-центру. В основном оно выполняется с помощью механизмов DNS-балансировк и Anycast, которые перенаправляют запросы пользователя на ближайший и наиболее загруженный ДЦ. Примерное     распределение:
  - **Северная Америка**: около 40-50% общего трафика iCloud.
  - **Европа**: около 25-30% трафика.
  - **Азия**: около 20-25% трафика.

  Конкретные типы запросов:
  - **Аутентификация и сессии**: обрабатываются в дата-центрах, близких к пользователю.
  - **Загрузка/скачивание файлов**: зависит от места хранения данных (файлы могут быть дублированы в нескольких ДЦ для ускорения).
  - **Резервное копирование**: выполняется через распределённые системы, с выбором ближайшего ДЦ.

5.  **Схема DNS-балансировки**
  DNS-балансировка используется для распределения запросов по нескольким дата-центрам. Когда пользователь обращается к iCloud, DNS-сервер перенаправляет запрос на ближайший по географии дата-центр. Этот процесс автоматизирован и основан на механизмах географического      разрешения DNS.

  - **Географическое разрешение DNS**: Запросы пользователей направляются на ближайший дата-центр с помощью **GeoDNS** для уменьшения задержек и снижения нагрузки на основной ДЦ.
  - **Автоматическое переключение**: В случае перегрузки или недоступности одного ДЦ запросы перенаправляются на другой ближайший центр обработки данных.

6. Механизм регулировки трафика между ДЦ
  Для регулировки трафика и обеспечения баланса нагрузки между дата-центрами используются несколько методов:
  - **Глобальные системы управления трафиком (Global Traffic Manager, GTM)**: GTM управляет направлением трафика в зависимости от нагрузки на конкретные дата-центры. Если один ДЦ перегружен, запросы перенаправляются в другой.
  - **Механизмы синхронизации данных**: iCloud поддерживает синхронизацию данных между дата-центрами. При этом дублируются файлы, необходимые для обеспечения резервного копирования и защиты данных.
  - **Автоматическое переключение при сбоях**: В случае отказа одного ДЦ, механизм автоматически перенаправляет трафик на другой доступный центр, что минимизирует время простоя для пользователей.

## Локальная балансировка

### 1. Схема балансировки

iCloud, как крупный облачный сервис Apple, использует различные уровни балансировки для эффективного распределения трафика и обеспечения отказоустойчивости.
Схема:
![image](https://github.com/user-attachments/assets/7230499c-f55d-4e3a-8ba7-1e8eed620582)

1. **L4 (Транспортный уровень)**:
  **Virtual Server via IP Tunneling** решает основные проблемы перегрузки балансировщика трафиком и по CPU и при этом не требует использования широковещательных ethernet-сегментов. Его основные преимущества в том, что он инкапсулирует оригинальные запросы в новые IP-пакеты и передаёт их на серверы, которые имеют локальный интерфейс с одинаковым VIP балансировщика.   Сервер, в свою очередь, отправляет ответ уже сразу клиенту.
  **Virtual Router Redundancy Protocol** используется для отказоустойчивости балансировщиков. Заключается в том, что несколько балансировщиков объединяются в виртуальную группу, и один становится master, а остальные — backup. Если главный выходит из строя, то один из резервных берёт на себя его функции и становится master.
  Чтобы понять, что сервер вышел из строя, используем **health check** с помощью HTTP/HTTPS. Это позволит убедиться в том, что не только сервер, но и приложение на нём работает.
  У L4 существует несколько серверов, которые привязаны к балансировщику L4. Он выдает пакету IP балансировщика L7. 

2. **L7 (Прикладной уровень)**:
  На уровне L7 балансировки используется **HTTP Reverse Proxy** в реализации **Nginx**, он является многофункциональным и распространённым.
  Реверс-прокси максимально упрощает управление запросами и выполняет:
    - Объединение TCP-соединений (поддерживает постоянные соединения с серверами, уменьшая количество соединений, которое требуется для обработки от каждого клиента).
    - Сохранение сессий (чтобы запросы от одного клиента всегда попадали на один и тот же сервер).
    - Кеширование (чтобы не отправлять постоянно каждый запрос на сервер, можно что-то сохранять на сервере прокси).
    - SSL Termination (расшифровка HTTPS на прокси, а на сервер шлём уже HTTP запросы).

3. **Kubernetes**
  Будем использовать систему оркестрации Kubernetes, чтобы не запускать экземпляры приложения вручную на серверах. Kubernetes берет на себя service discovery — управляет сервисами и динамически отслеживает список активных экземпляров с     помощью механизма Service и Endpoints.
  Kubernetes добавляет экземпляр в реестр после успешного прохождения readiness-пробы, что подтверждает его готовность принимать трафик. Он также распределяет поды (экземпляры) по узлам, перезапускает их или перераспределяет при сбоях.     Кроме того, Kubernetes автоматически выполняет масштабирование с помощью auto-scaling, таких как Horizontal Pod Autoscaler (HPA), который регулирует количество подов в зависимости от нагрузки.



### 2. Расчет нагрузки по терминации SSL

SSL/TLS терминация требует значительных вычислительных ресурсов, особенно для крупномасштабных сервисов, таких как iCloud. Она обрабатывает шифрование и дешифрование трафика для обеспечения безопасных соединений. Рассчитывается нагрузка на основе следующих параметров:

- **Количество SSL соединений**: Например, если среднее количество запросов в секунду составляет 9,000, это 9,000 новых SSL сессий каждую секунду. SSL терминация обрабатывает их на уровне балансировщиков или специализированных SSL прокси серверов.
  
- **SSL Offloading**: Терминация SSL может выполняться на уровне балансировщика нагрузки или специализированного SSL-терминатора. Это снижает нагрузку на веб-серверы и позволяет им работать с незашифрованным трафиком.

- **Аппаратные решения**: Внедрение аппаратных SSL акселераторов (например, в F5 или других балансировщиках) позволяет ускорить процесс шифрования/дешифрования, снижая задержки и нагрузку на вычислительные ресурсы.

### Расчет:
**Данные:**
- 14,248 запросов в секунду.
- Время выполнения SSL handshake для **TLS 1.2** составляет около 150 мс.
- Время выполнения SSL handshake для **TLS 1.3** можно сократить до 100 мс.

**Расчёт нагрузки:**

**Для TLS 1.2:**
1. **Число параллельных соединений**:
   14,248 соединений * 150 мс = 2,137,200 мс/сек
2. Чтобы рассчитать количество параллельных соединений, мы делим общее время на 1000 (так как 1000 мс = 1 секунда):
   2,137,200 мс/сек / 1000 = 2,137 соединений, обрабатываемых одновременно.

#### Для TLS 1.3:
1. **Число параллельных соединений** при 100 мс на handshake:
   14,248 соединений * 100 мс = 1,424,800 мс/сек.
2. Разделим это на 1000:
   1,424,800 мс/сек / 1000 = 1,425 соединений, обрабатываемых одновременно.

### Итог:
- Для **TLS 1.2**: около **2,137 параллельных соединений**.
- Для **TLS 1.3**: около **1,425 параллельных соединений**.

Таким образом, при нагрузке в 14,248 запросов в секунду, балансировщик должен поддерживать примерно от 1,425 до 2,137 параллельных соединений, в зависимости от используемой версии протокола.

## Логическая схема БД

![image](https://github.com/user-attachments/assets/8084f6be-6ebf-46e1-a10f-4f071c685c86)


### Таблица Users
  Cодержит информацию о пользователях, их учетные данные и подписки.
| Поле          | Тип данных  | Описание                                               |
|---------------|-------------|--------------------------------------------------------|
| `UserID`      | INT         | Уникальный идентификатор пользователя (PRIMARY KEY).    |
| `Username`    | VARCHAR     | Логин пользователя.                                    |
| `Email`       | VARCHAR     | Адрес электронной почты, используется для входа.       |
| `PasswordHash`| VARCHAR     | Хэшированный пароль для аутентификации.                |
| `StoragePlan` | ENUM        | Текущий тарифный план хранения.                        |
| `SignUpDate`  | TIMESTAMP   | Дата и время регистрации пользователя.                 |

### Таблица `Files`
  Хранит метаданные файлов, таких как их имя, размер, и версия. К каждому файлу привязан набор чанков и небольшой кэш.
| Поле          | Тип данных  | Описание                                               |
|---------------|-------------|--------------------------------------------------------|
| `FileID`      | INT         | Уникальный идентификатор файла (PRIMARY KEY).           |
| `UserID`      | INT         | Идентификатор пользователя (FOREIGN KEY, Users).       |
| `FileName`    | VARCHAR     | Имя файла.                                             |
| `FileSize`    | BIGINT      | Общий размер файла в байтах.                           |
| `CurrentVersion`| INT       | Текущая версия файла.                                  |
| `UploadDate`  | TIMESTAMP   | Дата и время загрузки файла.                           |

### Таблица `Chunks`
  Хранит информацию о чанках, на которые разбит каждый файл. К каждому чанкy привязан номер версии файла.
| Поле          | Тип данных  | Описание                                               |
|---------------|-------------|--------------------------------------------------------|
| `ChunkID`     | INT         | Уникальный идентификатор блока (PRIMARY KEY).          |
| `FileID`      | INT         | Идентификатор файла, к которому относится блок (FOREIGN KEY, Files). |
| `ChunkIndex`  | INT         | Порядковый номер блока в файле.                        |
| `ChunkHash`   | VARCHAR     | Хэш блока для проверки целостности.                    |
| `ChunkSize`   | BIGINT      | Размер блока в байтах.                                 |
| `ChunkData`   | BLOB        | Данные блока.                                          |
| `VersionNumber`| INT        | Номер версии файла, к которому относится блок.         |
| `UploadDate`  | TIMESTAMP   | Дата и время загрузки блока.                           |

### Таблица `Cache`
  Хранит часто используемые части файлов, то есть кэшированные чанки данных, которые необходимы для ускорения доступа к файлам.
| Поле          | Тип данных  | Описание                                               |
|---------------|-------------|--------------------------------------------------------|
| `CacheID`     | INT         | Уникальный идентификатор кэша (PRIMARY KEY).           |
| `FileID`      | INT         | Идентификатор файла (FOREIGN KEY, Files).              |
| `ChunkIndex`  | INT         | Порядковый номер чанка в файле, который кэшируется.    |
| `CacheTime`   | TIMESTAMP   | Время создания кэша.                                   |
| `CacheData`   | BLOB        | Кэшированные данные чанка.                             |
| `Expiration`  | TIMESTAMP   | Время истечения срока действия кэша.                   |

### Таблица Access Control
  Определяет права доступа пользователей к файлам для совместного использования.
| Поле          | Тип данных  | Описание                                               |
|---------------|-------------|--------------------------------------------------------|
| `AccessID`    | INT         | Уникальный идентификатор записи доступа (PRIMARY KEY).  |
| `FileID`      | INT         | Идентификатор файла (FOREIGN KEY, Files).              |
| `SharedWithID`| INT         | Идентификатор пользователя, с которым делятся файлом (FOREIGN KEY, Users). |
| `AccessLevel` | ENUM        | Уровень доступа: `read`, `write`, `owner`.             |
| `AccessDate`  | TIMESTAMP   | Дата и время предоставления доступа.                   |

### Таблица Sessions
  Хранит информацию о сессиях пользователей, включая активные подключения и авторизационные данные.
| Поле          | Тип данных  | Описание                                               |
|---------------|-------------|--------------------------------------------------------|
| `SessionID`   | INT         | Уникальный идентификатор сессии (PRIMARY KEY).          |
| `UserID`      | INT         | Идентификатор пользователя (FOREIGN KEY, Users).       |
| `LoginTime`   | TIMESTAMP   | Дата и время начала сессии.                            |
| `LogoutTime`  | TIMESTAMP   | Дата и время окончания сессии (NULL, если сессия активна). |
| `SessionToken`| VARCHAR     | Токен сессии для идентификации пользователя.           |


### Описание таблиц
Вот обновленная сводная таблица, добавленная с учётом нагрузки на таблицу **Chunks**:

### Описание таблиц

| **Таблица**       | **Размеры данных**                       | **Нагрузка на чтение (RPS)**   | **Нагрузка на запись (RPS)**  | **Консистентность**                                                                                   |
|-------------------|------------------------------------------|--------------------------------|-------------------------------|---------------------------------------------------------------------------------------------------------|
| **Users**         | Около 1–2 КБ на пользователя             | 994 (аутентификация)           | 10 (создание аккаунта)         | **Строгая консистентность**. Необходима высокая консистентность для аутентификации и обновления данных пользователей. Любое расхождение данных может привести к сбоям доступа. |
| **Files**         | Средний файл может быть от 1 МБ до нескольких ГБ | 1,968 (просмотр/скачивание файлов) | 984 (загрузка файлов)        | **Строгая консистентность**. Запись и доступ к файлам требует строгой консистентности, чтобы избежать потери данных. |
| **Chunks**        | В среднем от нескольких КБ до 4–8 МБ на чанк                 | 3,936 (просмотр/скачивание файлов, синхронизация данных) | 1,968 (загрузка файлов) | **Строгая консистентность**. Синхронизация данных и загрузка чанков требуют строгой консистентности для обеспечения целостности файлов и минимизации потерь данных. |
| **Access Control**| Маленькие (несколько КБ на объект доступа) | 20 (доступ к общим файлам/папкам) | 10 (создание доступа)         | **Строгая консистентность**. Для корректного управления правами доступа нужно поддерживать строгую консистентность. Любое нарушение может привести к утечкам данных. |
| **Sessions**      | Несколько КБ на сессию                   | 984 (по куке)                  | 10 (создание новых сессий)    | **Строгая консистентность**. Данные о сессиях должны быть всегда актуальны, чтобы избежать ошибок в авторизации. |
| **Cache**         | Зависит от кешируемых данных             | 5,902 (синхронизация данных, кэшируется большинство операций) | Зависит от кешируемых данных | **Eventual Consistency**. Для кеша можно использовать eventual consistency, чтобы улучшить производительность за счет допустимых задержек. |

## Физическая схема БД
![image](https://github.com/user-attachments/assets/57a5068c-6c2d-4e5a-83cb-ba60e1ae69d8)

### 1. Индексы
Индексы улучшают скорость запросов к таблицам за счет быстрого поиска по индексированным полям. В моей схеме:
- **Таблица `Users`**: Индексируем поля `Username` и `Email`, чтобы ускорить авторизацию и поиск пользователей.
- **Таблица `Files`**: Поле `FileName` можно проиндексировать для поиска файлов по имени, а поле `UploadDate` — для сортировки и выборок по дате загрузки.
- **Таблица `Access Control`**: Поля `SharedWithID` и `FileID` должны быть проиндексированы, чтобы ускорить проверку доступа к файлам для конкретного пользователя.

### 2. Денормализация
Денормализация может быть полезна для повышения производительности, особенно при частых операциях чтения данных, уменьшении количества сложных JOIN-запросов.
- **Files**: Можно добавить денормализованную информацию о владельце файла, например, поле `OwnerUsername`, что уменьшит количество JOIN-запросов к таблице `Users`.
- **Cache**: В зависимости от частоты обновления данных, можно денормализовать часто используемую информацию о файлах, например, имя файла или размер, что ускорит кэширование данных.

### 3. Выбор СУБД
- **Users, Files, Access Control**: Для этих таблиц подойдет реляционная СУБД, например, **PostgreSQL** или **MySQL** (остановимся на первом), поскольку они требуют согласованности данных (ACID-транзакции) и хорошо подходят для структурированных данных. Будем кэшировать ответы в **Redis**.
- **Chuncks**: Здесь можно использовать **NoSQL**, например, **Cassandra**, совместно с S3 хранилищем. Это обеспечит быструю работу с кэшем и хранение данных в виде «ключ-значение» или больших объемов бинарных данных.
- **Sessions**, **Cache**: В данном случае воспользуемся **Redis**, который может обеспечить быстрый доступ к часто используемым данным.

### 4. Шардирование и резервирование СУБД
PostgreSQL не поддерживает горизонтальное шардирование «из коробки», но это можно настроить с помощью сторонних решений, таких как **Citus** или через логическое шардирование (разделение данных на несколько кластеров). В твоем случае:
- **Шардирование по `UserID`** для таблицы `Users`, что позволит разделить данные пользователей на несколько нод.
- **Шардирование по `FileID`** для таблицы `Files`, чтобы уменьшить нагрузку на отдельные узлы базы данных.
Это позволит распределить нагрузку на чтение/запись и поддерживать высокую производительность при масштабировании.
- **Горизонтальное шардирование по `FileID`** для таблицы `Chuncks`. Если данные распределяются по миллионам различных файлов, использование `FileID` в качестве основного ключа партиционирования позволит равномерно распределить нагрузку между нодами Cassandra.
- **Гибридное шардирование по `FileID` и `ChunkIndex`** для таблицы `Chuncks`. Для крупных файлов, состоящих из большого числа чанков, разумно добавить в шардирование и `ChunkIndex`, чтобы отдельные чанки одного и того же файла могли распределяться по разным узлам. Это повысит параллельность при доступе к частям файлов.


### 5. Балансировка запросов / мультиплексирование подключений
Необходимо настроить балансировку запросов и мультиплексирование подключений для масштабируемости:
- **Балансировщики L7** (например, Nginx) для реляционных БД. 
- Для NoSQL-систем Cassandra можно использовать внутренние инструменты балансировки.
- **Мультиплексирование** позволяет управлять большим количеством подключений одновременно, уменьшая нагрузку на базу данных.

### 6. Схема резервного копирования
Для обеспечения высокой доступности и отказоустойчивости, необходимо настроить резервное копирование данных:
- **PostgreSQL**: Использовать регулярные **снапшоты** базы данных, а также инкрементные бэкапы.
- **Cassandra**: Настроить резервирование на уровне узлов и хранить снапшоты или использовать кластерную репликацию для создания геораспределенных копий данных.

## Источники
- https://worldmetrics.org/apple-icloud-statistics/
- https://chargeasap.com/blogs/news/breakdown-of-iphone-users-by-country
- https://support.apple.com/en-us/108047
- https://www.statista.com/topics/1695/cloud-computing/
- https://www.datacenterknowledge.com/servers/apple-data-center-and-servers-faq
- https://www.datacenters.com/providers/apple-inc/data-center-locations
- https://xakep.ru/2016/05/18/hack-ios-backup/

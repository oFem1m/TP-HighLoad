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
6. **Безопасность и шифрование данных** (с базовым шифрованием данных при передаче).

## Продуктовые метрики
1. **Месячная аудитория (MAU)**: В 2023 году количество пользователей iCloud составляет более 850 миллионов активных пользователей по всему миру.
2. **Дневная аудитория (DAU)**: Примерно 119 млн пользователей в США и 125 млн в Китае, что позволяет предполагать значительное количество ежедневных активных пользователей, ориентировочно 10-20% от MAU, т.е. около 85-170 млн.
3. **Средний размер хранилища пользователя**: iCloud предлагает тарифные планы от 50GB до 12TB на пользователя. У 80% пользователей бесплатный тарифный план - 5GB. у 13% - 50GB, 5% - 200GB, 1% - 2TB, <1% - 6TB, <1% - 12TB, Средний объем хранилища может составлять около 50GB, в зависимости от типа пользователей [Apple Support](https://support.apple.com/en-us/108047) [Statista](https://www.statista.com/topics/1695/cloud-computing/).

Так как подписка ежемесечная, то проценты и количество пользователей вычисляются на основе MAU:

| Тарифный план   | Процент пользователей      | Количество пользователей |
|-----------------|----------------------------|--------------------------|
| 5GB             | 80%                        | 680 млн                  |
| 50GB            | 13%                        | 110.5 млн                |
| 200GB           | 5%                         | 42.5 млн                 |
| 2TB             | >1%                        | 11.05 млн                |
| 6TB             | <1%                        | 5.1 млн                  |
| 12TB            | <1%                        | 0.85 млн                 |

Подсчитаем среднее значение на пользователя: 
(680 млн * 5 GB + 110.5 млн * 50GB + 42.5 млн * 200GB + 11.05 млн * 2048GB + 5.1 * 6144GB + 0.85 млн * 12288GB) / 850 млн =  81834.6 GB / 850 млн = 96,276, что можно округлить до 100GB. 

Итого:
| Метрика                                   | Значение                   |
|-------------------------------------------|----------------------------|
| Месячная аудитория (MAU)                  | 850 млн                    |
| Дневная аудитория (DAU)                   | 85-170 млн                 |
| Средний размер хранилища на пользователя  | 100 GB                     |

Основываясь на личном опыте и опыте знкомых, я составил таблицу

| Тип запроса                              |   Среднее количество действий в день на пользователя   |
|------------------------------------------|--------------------------------------------------------|
| **Аутентификация (вход с разных устройств)** | 1.5                                                |
| **Загрузка файлов на облако**            | 5                                                      |
| **Просмотр/скачивание файлов**           | 10                                                     |
| **Удаление файлов**                      | 2                                                      |
| **Создание/доступ к общим папкам/файлам**| 0.5                                                    |
| **Синхронизация данных (контакты, фото)**| 15                                                     |
| **Резервное копирование**                | 0.1                                                    |
| **Обновление настроек/параметров учетной записи** | 0.5                                           |


## Технические метрики
1. **Размер хранения по типам данных**: Общие данные пользователей распределяются по категориям — фото, видео, документы. Основной объем занимают медиафайлы, что может составлять до 80% от общего объема хранения. Если средний объем хранения пользователя 50GB, это будет эквивалентно 14 эксабайт данных для всего сервиса (170000000 * 50 / 1024^3 + 680000000 * 5 / 1024^3)
2. **Сетевой трафик**:
   - **Пиковое потребление**: пиковая скорость может достигать 100-200 Гбит/с в зависимости от времени суток и региона.
   - **Суммарный суточный трафик**: составляет порядка нескольких петабайт в сутки.
3. **RPS (requests per second)**: Для таких операций, как загрузка данных, синхронизация и резервное копирование, запросы могут составлять от 10k до 100k запросов в секунду в часы пик.

| Метрика                     | Среднее значение   |
|-----------------------------|--------------------|
| Размер хранения (всего)     | 14 EB              |
| Сетевой трафик (в сутки)    | ~20-25 PB          | 
| RPS по запросам             | 10k–100k           |

### Сетевой трафик по типам операций:

1. **Регистрация и авторизация**:
   - Регистрация в системе требует передачи базовых данных пользователя (например, имя, email, пароли), что занимает около **5-10 МБ** на одну операцию.
   - Авторизация использует меньший объем данных — около **1-3 МБ** на запрос.
   - Если в день регистрируется 100 тысяч пользователей и авторизуются 17 миллионов, то дневной трафик от этих операций составит:
     - Регистрация: 100000 * 10 МБ = 1 ТБ
     - Авторизация: 17000000 * 3 МБ = 51 ТБ

2. **Загрузка и синхронизация фотографий**:
   - Каждая фотография на iPhone весит от **1 до 10 МБ** в зависимости от качества и формата (JPEG, HEIC).
   - Предположим, что каждый пользователь загружает в среднем 5 фото в день, что даёт следующий расчёт для 170 млн активных пользователей:
     - 170000000 * 5 МБ * 5 фото = 4.25 ПБ в день.

3. **Загрузка и синхронизация видео**:
   - Видео занимают гораздо больше места — от **100 МБ до 1 ГБ** за минуту видео в высоком качестве (например, 4K).
   - Предположим, что 10% пользователей загружают или синхронизируют по 1 минуте видео в день:
     - 170000000 * 10% * 1 минута * 500 МБ = 8.5 ПБ в день.

4. **Поиск контента (документы, фото и т.д.)**:
   - Поиск данных требует небольших объемов данных — около **0.5-1 МБ** за запрос.
   - Если каждый пользователь совершает 30 крупных запросов в день:
     - 170000000 * 30 * 1 МБ = 5 ПБ в день.

5. **Резервное копирование**:
   - Основной объем резервных копий приходится на документы, настройки и мультимедиа. Это может занимать от **50 МБ до нескольких ГБ**.
   - Если 50% пользователей делают автоматические резервные копии один раз в неделю, а размер копии в среднем составляет 500 МБ, то дневной объем трафика будет:
     - 170000000 * 50% * (1/7) * 500 МБ = 6.07 ПБ в день.

6. **Остальные операции (доступ к документам, контакты и т.д.)**:
   - Мелкие операции, такие как синхронизация контактов и заметок, занимают значительно меньше трафика — от **0.1 до 1 МБ** за каждую операцию.
   - Общий трафик на эти операции можно оценить в **100-200 ТБ в день**.

### Итоговая таблица трафика:

| Действие                         | Трафик на одного пользователя | Общее количество пользователей | Общий трафик в день |
|-----------------------------------|-------------------------------|--------------------------------|---------------------|
| Регистрация и авторизация         | 1-10 МБ                       | 17  млн                        | 51  ТБ              |
| Загрузка и синхронизация фото     | 1-10 МБ за фото               | 170 млн                        | 4.25 ПБ             |
| Загрузка и синхронизация видео    | 500 МБ за минуту              | 17 млн (10% пользователей)     | 8.5 ПБ              |
| Поиск контента                    | 0.5-1 МБ за запрос            | 170 млн                        | 5 ПБ                |
| Резервное копирование             | 500 МБ за копию               | 85 млн (50%)                   | 6.07 ПБ             |
| Мелкие операции (контакты, документы)| 0.1-1 МБ                     | 170 млн                        | 100-200 ТБ          |

### Сетевой трафик по сумме:

Суммарный дневной трафик iCloud составит **примерно 20-25 ПБ** (включая все операции).

### Пиковые значения:

- **Пиковое потребление** может быть в 2-3 раза выше среднего из-за интенсивного использования в определённые часы (вечер, выходные), что дает до **600-700 Гбит/с** трафика.

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

2. **Обоснование расположения дата-центров**  
   Apple размещает свои дата-центры стратегически для минимизации задержек (latency) и улучшения пользовательского опыта. Основные метрики:
   - **Задержка**: Чем ближе дата-центр к пользователю, тем ниже задержка, что особенно важно для синхронизации данных и облачного хранения.
   - **Надежность**: Apple распределяет дата-центры по регионам для повышения отказоустойчивости. Например, дата-центры в США, Европе (Дания), Азии (Китай), Австралии.
   - **Законы о данных**: Важный фактор, так как законодательство некоторых стран требует хранения данных пользователей внутри страны. Например, данные китайских пользователей хранятся в местных дата-центрах из-за законодательства о персональных данных.

3. **Распределение запросов по типам и дата-центрам**  
   Запросы от пользователей iCloud распределяются по типам:
   - **Хранение файлов**: Основная нагрузка на дата-центры в США и Европе, где хранится большая часть пользовательских данных.
   - **Почта и синхронизация**: Нагрузка распределена по всем дата-центрам в зависимости от местоположения пользователя.
   - **Резервное копирование и восстановление**: Включает запросы на хранение резервных копий устройств, распределённые по дата-центрам с большим количеством хранилищ.

4. **Схема DNS-балансировки**  
   iCloud использует **GeoDNS**, что позволяет направлять запросы на ближайшие дата-центры в зависимости от географического местоположения пользователя. GeoDNS определяет, из какого региона поступает запрос, и направляет его на соответствующий дата-центр, тем самым снижая задержку и увеличивая скорость отклика.

5. **Схема Anycast-балансировки**  
   Anycast используется для улучшения отказоустойчивости и повышения скорости доступа. Запросы направляются на ближайший узел сети, независимо от его географического положения. Это позволяет сократить маршрутизацию и уменьшить задержку для глобальных пользователей.

6. **Механизм регулировки трафика между ДЦ**  
   Для балансировки трафика между дата-центрами Apple использует динамическую маршрутизацию и решения на базе SDN (Software-Defined Networking). Трафик перераспределяется в случае перегрузки одного из центров, аварийных ситуаций или сбоев, что обеспечивает стабильную работу iCloud без простоев. В некоторых случаях может использоваться миграция запросов на резервные центры обработки данных.



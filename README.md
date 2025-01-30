# Тестовое задание на позицию Backend-разработчика

## Описание задания

Необходимо разработать API для загрузки и обработки Excel-файлов (`.xlsx`), а также сохранения данных в базу данных.

## Технические требования
- **PHP**: ≥ 8.1
- **Фреймворк**: Slim 4
- **База данных**: MariaDB
- **HTTP-запросы**: guzzlehttp/guzzle
- **Работа с БД**: illuminate/database
- **Логирование**: monolog/monolog
- **Docker**: предустановлен в репозитории

## Установка
```sh
# Клонируем репозиторий
git clone <ваш_репозиторий>
cd <ваш_репозиторий>

# Инициализация окружения
make init
```

## Задачи

### 1. Разработка структуры БД
Необходимо создать три таблицы:

#### Таблица объявлений (**ads**):
- `id` (PK, int, auto_increment) — ID объявления
- `date_spent` (date) — Дата расхода
- `amount_spent` (decimal) — Сумма расхода
- `ad_name` (varchar) — Название объявления
- `campaign_id` (FK, int) — ID кампании
- `group_id` (FK, int) — ID группы
- `impressions` (int) — Показы
- `clicks` (int) — Клики

#### Таблица кампаний (**campaigns**):
- `id` (PK, int, auto_increment) — ID кампании
- `campaign_name` (varchar) — Название кампании

#### Таблица групп (**groups**):
- `id` (PK, int, auto_increment) — ID группы
- `group_name` (varchar) — Название группы

### 2. Реализация моделей

Создать и реализовать методы в моделях (`/src/Models`):
- `Ads.php` — Модель объявлений
- `AdsAdset.php` — Модель групп
- `AdsCampaign.php` — Модель кампаний

Методы для каждой модели:
- **Добавление одной записи**
- **Множественная вставка записей**
- **Обновление записи**
- **Удаление записи**

> При обработке файла использовать созданные модели.

### 3. Реализация API для загрузки файла
Добавить маршрут (`/src/Config/routes.php`):
- **Метод:** `GET`
- **Маршрут:** `/upload`
- **Действие:** Загружает файл `ads.xlsx` из `/var/excel/ads.xlsx`

### 4. Реализация скрипта обработки файла

Скрипт: `/src/Console/ImportCsvAds.php`
Запуск:
```sh
php bin/app.php import-csv-ads
```

**Этапы работы:**
1. Загружаем `ads.xlsx` через API.
2. Обрабатываем файл и сохраняем данные в БД.
3. Поддержка двух режимов обработки (`fileProcessingMode`):
   - `true` — множественная вставка
   - `false` — одиночная вставка
4. **Обновление данных** при повторном запуске, если:
   - Название кампаний/групп/объявлений изменилось
   - Дата расхода, сумма, показы, клики изменились
5. **Логирование:** все действия фиксируются в логах.

### 5. Финальный шаг
После выполнения задания:
1. Загрузите код в репозиторий.
2. Отправьте ссылку на репозиторий.
3. Укажите время выполнения задачи.


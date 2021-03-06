# MediaWiki Bot

## Содержание

- [Установка](#Установка)
- [Конфигурация проекта](#Конфигурация-проекта)

## Установка

**1. Клонирование репозитория**

Склонируйте репозиторий с ботом в нужную папку

```bash
git clone https://github.com/quranacademy/MediaWiki-Bot .
```

**2. Установка зависимостей проекта (Composer)**

Установите зависимости проекта выполнив команду:

```bash
composer install
```

**3. Установка прав на чтение и запись для папки хранилища**

```bash
sudo chmod -R 777 storage/
```

**4. Конфигурация**

Выполните команду и следуйте инструкциям:

```bash
php setup.php
```

**5. Создание нового проекта**

Выполните команду и следуйте инструкциям:

```bash
php create-project.php
```

## Конфигурация проекта

Все проекты расположены в папке projects:

```
projects/<project-name>.php
```

Взаимодействие бота и сайта происходит посредством API - интерфейса, который сайт предоставляет внешним приложениям. После установки бота нужно указать ему адрес(а) API сайта.

### Как узнать адрес API?

Адрес API указан на служебной странице "Служебная:Версия" ("Special:Version") в разделе "Адреса точек входа" ("Entry point URLs") в строке `api.php`. Указанный адрес следует добавить к домену, на котором расположен сайт. Например, если вики расположена по адресу `http://example.com`, а на странице указан путь `/w/api.php`, то API вики будет находится по адресу `http://example.com/w/api.php`.

Попробуйте перейти по полученному URL через браузер и если страница найдена (должна открыться справка по API), то все сделано верно.

**Важное замечание:** для мультиязычных вики, где для каждого языка установлен свой движок, API не является общим и его необходимо указать отлельно для каждого сайта.

Метод **getApiUrls** (класс проекта) должен возвращать адрес(а) API:

```php
/**
 * @return array
 */
public function getApiUrls()
{
    return [
        'ar' => 'http://ar.example/api.php',
        'az' => 'http://az.example/api.php',
        'en' => 'http://en.example/api.php',
        'tr' => 'http://tr.example/api.php',
        'ru' => 'http://ru.example/api.php',
    ];
}
```

Метод **getApiUsernames** должен возвращать имена пользователей. Пример:

```php
/**
 * @return array
 */
public function getApiUsernames()
{
    return [
        'ar' => 'MediaWiki-Bot',
        'az' => 'MediaWiki-Bot',
        'en' => 'MediaWiki-Bot',
        'ru' => 'MediaWiki-Bot',
        'tr' => 'MediaWiki-Bot',
    ];
}
```

**Важное замечание:** пользователей для бота необходимо регистрировать на сайте самостоятельно через веб-интерфейс. Для мультиязычных вики, где для каждого языка установлен свой движок, пользователей необходимо регистрировать отдельно на каждом сайте.

На этом конфигурация проекта завершена.

## Проверка работоспособности

Для начала попробуем вывести список проектов. Для этого выполните команду:

```bash
php mediawiki.php projects
```

А теперь попробуем авторизоваться:

```bash
php mediawiki.php login
```

Также мы можем указать язык сайта, на котором хотим авторизоваться:

```bash
php mediawiki.php login <lang>
```

Пример:

```bash
php mediawiki.php login en
```

В случае, когда язык не указан, будет использован язык проекта по умолчанию (тот, что был указан при создании проекта).

Если нужно просто выйти выполните команду с флагом `--logout`:

```bash
php mediawiki.php login <lang> --logout
```

Пример:

```bash
php mediawiki.php login en --logout
```

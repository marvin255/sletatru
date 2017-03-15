Php клиент для api sletat.ru(слетать.ру)
==========================================

Php обертка для [api sletat.ru(слетать.ру)](http://sletat.ru/).


Установка
---------

**С помощью [Composer](https://getcomposer.org/doc/00-intro.md).**

Добавьте в ваш composer.json в раздел `require`:

```javascript
"require": {
    "marvin255/sletatru": "*"
}
```

**Обычная**

Скачайте библиотеку и распакуйте ее в свой проект. Убедитесь, что файл `Autoloader.php` подключен в вашем скрипте.

```php
require_once 'lib/Autoloader.php';
```


Сервис для поиска туров
-----------------------

Soap сервис для поиска туров с использованием API слетать.ру


**Использование**

```php
//инициируем новый объект xml сервиса
$xml = new \sletatru\XmlGate([
	'login' => 'ваш логин для авторизации на сервисе',
	'password' => 'ваш пароль для авторизации на сервисе',
]);
//получаем список городов вылета
$departCities = $xml->GetDepartCities();
```


**Настройка**

При инициализации:

```php
$xml = new \sletatru\XmlGate([
	'login' => 'ваш логин для авторизации на сервисе',
	'password' => 'ваш пароль для авторизации на сервисе',
]);
```

После инициализации:

```php
$xml->config([
	'login' => 'ваш логин для авторизации на сервисе',
	'password' => 'ваш пароль для авторизации на сервисе',
]);
```

**Опции**

* `wsdl` - ссылка на описание wsdl, по умолчанию `'http://module.sletat.ru/XmlGate.svc?wsdl'`;

* `login` - логин для авторизации на сервисе;

* `password` - пароль для авторизации на сервисе;

* `soapOptions` - настройки [SoapClient](http://php.net/manual/ru/soapclient.soapclient.php), по умолчанию `[]`;

* `catchExceptions` - если значение истинно, то все исключения будут перехвачены классом и внесены во внутренний массив ошибок, в противном случае исключения не будут обрабатываться, по умолчанию `true`;


**Методы**

Названия и сигнатуры методов совпадают с названиями и сигнатурами методов api. [Подробнее](http://static.sletat.ru/Files/Manual/XML_gate_Search.pdf).


**Дополнительне методы**

* `array \sletatru\XmlGate::getErrors( void )` - возвращает массив ошибок, полученных во время запросов к сервису.

* `bool \sletatru\XmlGate::hasErrors( void )` - возвращает истину, если во время выполнения запроса были ошибки.

* `void \sletatru\XmlGate::clearErrors( void )` - очищает список ошибок.

* `array \sletatru\XmlGate::getHotelImageUrl( int $id, int $count[, int $width, int $height, int $method] )` - формирует ссылку на фотографию с порядковым номером $count отеля с идентификатором $id, указанной ширины и высоты.


Сервис для поиска горящих туров
-------------------------------

Rest сервис для поиска горящих туров с использованием API слетать.ру

**Внимание** функционал реализован только для поиска горящих туров (только метод `GetTours`). Все остальное можно получить с помощью XML шлюза, описанного выше, в том числе и актуализацию горящего тура.

**Внимание** параметры туров, возвращаемых из поиска максимально приближены к параметрам туров, возвращаемых при поиске через XML шлюз, поэтому названия параметров не совпадают с нумерованием параметров в документации.


**Использование**

```php
//инициируем новый объект json сервиса
$json = new \sletatru\JsonGate([
	'login' => 'ваш логин для авторизации на сервисе',
	'password' => 'ваш пароль для авторизации на сервисе',
]);
//получаем список горящих ткров по фильтру
$tours = $json->GetTours($cityFrom, $countryTo);
```


**Настройка**

При инициализации:

```php
$json = new \sletatru\JsonGate([
	'login' => 'ваш логин для авторизации на сервисе',
	'password' => 'ваш пароль для авторизации на сервисе',
]);
```

После инициализации:

```php
$json->config([
	'login' => 'ваш логин для авторизации на сервисе',
	'password' => 'ваш пароль для авторизации на сервисе',
]);
```


**Опции**

* `url` - ссылка на сервис, по умолчанию `'http://module.sletat.ru/Main.svc'`;

* `login` - логин для авторизации на сервисе;

* `password` - пароль для авторизации на сервисе;



**Методы**

Названия и сигнатуры методов совпадают с названиями и сигнатурами методов api. [Подробнее](http://static.sletat.ru/Files/Manual/JSON_gate_hottours.pdf).


**Дополнительне методы**

* `array \sletatru\JsonGate::getErrors( void )` - возвращает массив ошибок, полученных во время запросов к сервису.

* `bool \sletatru\JsonGate::hasErrors( void )` - возвращает истину, если во время выполнения запроса были ошибки.

* `void \sletatru\JsonGate::clearErrors( void )` - очищает список ошибок.

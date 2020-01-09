# dd-alicization

Go-модуль для работы с Яндекс.Станцией

Установка:

``
go get github.com/anvlad11/dd-alicization
``

Модуль содержит пакет glagol
* glagol.APIClient - работа с API Яндекса для получения списка устройств пользователя;
* glagol.Conversation - работа с Яндекс.Станцией через веб-сокеты;
* glagol.HttpGateway - HTTP-gateway для проброса запросов из внешних сервисов к Яндекс.Станции

## Конфигурация

Для конфигурации используются следующие переменные окружения

* `YANDEX_OAUTH_TOKEN` - токен для запросов к API Яндекса, необходим для работы `glagol.APIClient`. Его можно вытащить из запросов мобильного приложения Яндекс.Музыка;
* `GLAGOL_USE_STATION_CONFIG` - флаг для использования конфига для подключения к определённой станции, 1 или 0;
* `GLAGOL_STATION_ID` - ID станции, можно получить из настроек Станции в Квазаре (https://quasar.yandex.ru/) или приложении Яндекс;
* `GLAGOL_STATION_ADDRESS` - локальный IP станции, только IPv4;
* `GLAGOL_STATION_PORT` - websocket-порт станции, по-умолчанию 1961;
* `GLAGOL_CONFIRM_CONNECTION` - подверждение подключения к станции голосом, 1 или 0;
* `HTTP_HOST` - хост, на котором будет подниматься HTTP Gateway, по-умолчанию :58080 (то же самое, что и localhost:58080)

## HTTP Gateway

Частичное описание API для работы с Станцией через гейтвей - https://documenter.getpostman.com/view/525400/SWLfd8et?version=latest

Станция раз в N (сейчас N = 1) секунд отправляет свой статус к подключенному клиенту, а не отвечает им на запрос, поэтому для получения свежего статуса Станции после отправки POST-запроса через гейтвей необходимо сделать пустой GET-запрос.

## Пример сервиса

В `main.go` есть пример сервиса, который получит список устройств на аккаунте пользователя, токенов доступа для них, сделает поиск доступных устройств в локальной сети, подключится к первому найденному и поднимет HTTP Gateway до него.

## TODO

- [x] Сделать TODO-лист
- [ ] Получение OAuth-токена Яндекса
- [ ] Dockerfile/docker-compose для примера сервиса
- [ ] Более лучшая документация
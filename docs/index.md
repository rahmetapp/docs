# RahmetPay

Ниже представлена документация для RahmetPay

## Авторизация

Для отправки запросов вам потребуется токен, который выдается после авторизации.  
`https://gateway.chocodev.kz/auth/token`  

Заголовки:  

* `client_id` - ID клиента, выдается нами.
* `client_secret` - Ключ клиента, выдается нами.
* `grant_type` - Тип авторизации. Сюда ставим client_credentials
  
Далее, во всех методах, описанных ниже, в заголовках отправлять полученный токен -  
**Authorization: Bearer TOKEN**

## Размещение заказа

### Размещение
Для создания заказа отправить POST запрос на адрес  
`https://gateway.choco.kz/orders/v1/preorder/create`  
со следующими данными:

Ключ | Описание | Пример
--- | --- | ---
merchant_order_id | ID заказа в вашей системе **required** | 100500
amount | Сумма заказа для оплаты через Rahmet **required** | 2500
token | Токен для определения филиала **required** | hash, выдается нами
backlink | DeepLink приложения, на которое мы отправим пользователя (чаще всего, ThankYouPage) | https://project.kz/backend/setStatus?id=100500&paid=true
postlink | Ссылка для оповещения вашего бэка после оплаты (GET) | https://project.kz/backend/order/100500/setPaid

### Ответ
```
{
    "error_code": 0,
    "status": "success",
    "message": "Предзаказ создан",
    "data": {
        "preorder_id": 111,
        "url": "https://rahmetapp.kz/?id=HASH"
    }
}
```
_url - ставить эту ссылку для оплаты или сформировать с нее QR_

## Проверка статуса заказов

Для создания заказа отправить POST запрос на адрес  
`https://gateway.chocodev.kz/auth/token`  
со следующими данными:

Ключ | Описание | Пример
--- | --- | ---
merchant_order_id | ID заказа в вашей системе **required** | 100500
amount | Сумма заказа для оплаты через Rahmet **required** | 2500
token | Токен для определения филиала **required** | hash, выдается нами
backlink | DeepLink приложения, на которое мы отправим пользователя (чаще всего, ThankYouPage) | https://project.kz/backend/setStatus?id=100500&paid=true
postlink | Ссылка для оповещения вашего бэка после оплаты (GET) | https://project.kz/backend/order/100500/setPaid

## Возврат

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs help` - Print this help message.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.

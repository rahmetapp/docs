## Запрос и пример

Для создания активного заказа  
`PUT https://gateway.chocodev.kz//orders/v2/preorder/external/status`  
(в заголовке не забываем [Content-Type](/#_3) и [токен](/en/latest/auth))  

Параметры запроса:

Ключ | Описание | Примечание | Значение | Тип
--- | --- | --- | --- | ---
merchant_order_id | ID заказа в вашей системе | Обязательное | 12344323 | string
user_id | ID пользователя в choco users | Обязательное | 1 | int
external_status<sup>1</sup> | Статус заказа в вашей системе | Обязательное | created | string
deeplinks[0][link] | DeepLink, на которое мы отправим пользователя | Обязательное | https://rahmetapp.kz/webapp/1/orders?tab=3 | string
deeplinks[0][type] | Тип deeplink | Обязательное | active_order_call_to_action/active_order_card | string
external_data[expired_at] <sup>2</sup> | Дата и время до которого действует статус | Обязательное | 2021-10-10 00:00:00 | string
external_data[title_active_order_card] <sup>3</sup> | Заголовок в карточке активного заказа | Обязательное | Заказ создан | string
external_data[title_call_to_action] <sup>4</sup> | Заголовок кнопки | Обязательное | Показать на карте | string
is_need_timer | Нужно ли отображать таймер обратного отсчёта | Обязательное | true | bool

- <sup>1</sup> Статусы необходимо предварительно передать нам.
- <sup>2</sup> Формат даты и времени 2021-10-10 00:00:00
- <sup>3</sup> Ограничение 30 символов.
- <sup>4</sup> Ограничение 30 символов.

Пример запроса: 
```
{
            "merchant_order_id": "WEE-11122",
            "user_id": 1234567,
            "external_status": "created",
            "deeplinks": [
                {"link": "https://rahmetapp.kz/100/orders?tab=3", "type": "active_order_call_to_action"},
                {"link": "https://rahmetapp.kz/100/orders?tab=5", "type": "active_order_card"},
            ],
            "external_data": {
                "expired_at": "2021-10-20 16:49:36",
                "title_active_order_card": "Ожидает оплаты",
                "title_call_to_action": "К заказу"
            },
            "is_need_timer": true,
}
```

### Ответ и пример

В ответ сервер возвращает JSON с указанными [здесь](/#_4) составляющими.  

Пример ответа: 
```
{
    "error_code": 0,
    "status": "success",
    "message": "Статус успешно обновлён",
    "data": {
        "id": 1111,
        "merchant_order_id": "WEE-11122",
        "filial_id": 1,
        "amount": "1",
        "qr_code_id": 1,
        "postlink": "http://postlink/",
        "backlink": null,
        "created_at": "2021-10-18 16:49:36",
        "updated_at": "2021-11-03 04:09:52",
        "merchant_id": 1234,
        "failed_postlink": "http://failed_post/",
        "expired_at": "2021-10-18 17:19:36",
        "type": 0,
        "scanned_user_id": 12234,
        "merchant_slug": null,
        "supplementary_data": null,
        "external_filial_id": null,
        "external_status_id": 7,
        "checklink": "http://checklink/",
        "failed_on_check": true,
        "request_from_type": "miniapp"
    }
}
```
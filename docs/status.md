## Запрос и пример

Для проверки статуса оплаты заказа необходимо выполнить вызов метода  
`POST https://gateway.chocodev.kz/orders/v1/preorder/status`  
(в заголовке не забываем [Content-Type](/#_3) и [токен](/en/latest/auth))  

Параметры запроса:

Ключ | Описание | Примечание
--- | --- | ---
merchant_order_ids[] | Массив ваших ID заказов для проверки статуса | Обязательное

Пример запроса: 
```
merchant_order_ids[]: 100500
merchant_order_ids[]: 100501
merchant_order_ids[]: 100502
```

### Ответ и пример

В ответ сервер возвращает JSON с указанными [здесь](/#_4) составляющими.  

Пример ответа: 
```
{
    "error_code": 0,
    "status": "success",
    "message": "Статусы заказов",
    "data": {
        "100500": {
            "is_paid": true,
            "reference": 123456,
            "amount": 3000,
            "balance_amount": 100,
            "device": "ANDROID",
            "cashback": 300,
            "refund": {
                "refunded_amount": 1500,
                "refunded_cashback": 150
            }
        },
        "100501": {
            "is_paid": true,
            "reference": 123457,
            "amount": 5000,
            "balance_amount": 100,
            "device": "IOS",
            "cashback": 250
        },
        "100502": {
            "is_paid": false,
            "reference": 123458,
            "amount": null,
            "cashback": null
        }
    }
}
```

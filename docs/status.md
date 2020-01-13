## Запрос и пример

Для проверки статуса оплаты заказа необходимо выполнить вызов метода  
`POST https://gateway.chocodev.kz/orders/v1/preorder/status`  
(в заголовке не забываем [Content-Type](/#_3) и [токен](/auth))  

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
            "amount": 3000,
            "cashback": 300,
            "refund": {
                "refunded_amount": 1500,
                "refunded_cashback": 150
            }
        },
        "100501": {
            "is_paid": true,
            "amount": 5000,
            "cashback": 250
        },
        "100502": {
            "is_paid": false,
            "amount": null,
            "cashback": null
        }
    }
}
```
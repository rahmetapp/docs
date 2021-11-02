## Запрос и пример

Для возврата средств по заказу необходимо выполнить вызов метода  
`POST https://gateway.chocodev.kz/orders/v1/preorder/refund` (idempotent method)  
(в заголовке не забываем [Content-Type](/#_3) и [токен](/en/latest/auth))  

Чтобы использовать этот метод как идемпотентный, необходимо в заголовках отправить  
`X-Idempotency-Key: UUID-V4`

Параметры запроса:

Ключ | Описание | Примечание
--- | --- | ---
merchant_order_id | ID заказа в вашей системе | Обязательное
amount | Сумма для возврата | Обязательное

Пример запроса: 
```
merchant_order_id: 100500
amount: 500
```

### Ответ
```
{
    "error_code": 0,
    "status": "success",
    "message": "Заявка на возврат принята в обработку.",
    "data": {
        "refund_request": {
            "id": 156,
            "amount": 500,
            "comment": "Возврат по заказу мерчанта #100500",
            "commission_amount": 25,
            "cashback_amount": 100,
            "requested_amount": 500,
            "idempotency_key": "29492e44-cbe6-4a5f-ae38-c21a114f4a70"
        }
    }
}
```
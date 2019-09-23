## Возврат

Для возврата средств по заказу необходимо отправить POST запрос на адрес
`https://gateway.chocodev.kz/orders/v1/preorder/refund` (idempotent method)  
Headers:  
`Content-Type: x-application/x-www-form-urlencoded`  

с данными:  

Ключ | Описание 
--- | --- 
merchant_order_id | ID заказа для возврата средств **required** 
amount | Сумма, которую необходимо вернуть **required** 

Чтобы использовать этот метод как идемпотентный, необходимо в заголовках отправить  
`X-Idempotency-Key: UUID-V4`

### Ответ
```
{
    "error_code": 0,
    "status": "success",
    "message": "Заявка на возврат принята в обработку.",
    "data": {
        "refund_request": {
            "id": 156,
            "order_id": 1788,
            "amount": 500,
            "status": 1,
            "comment": "Возврат по заказу мерчанта #111235",
            "created_user_id": 11619734,
            "processed_user_id": 11619734,
            "chocobalance_id": 4448,
            "create_at": "2019-09-18 16:32:07",
            "processed_at": "2019-09-18 16:32:10",
            "commission_amount": 25,
            "cashback_amount": 100,
            "requested_amount": 500,
            "idempotency_key": "29492e44-cbe6-4a5f-ae38-c21a114f4a70"
        }
    }
}
```
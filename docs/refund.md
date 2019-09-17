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
    "message": "Заявка на возврат принята в обработку",
    "data": {
        
    }
}
```
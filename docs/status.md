Для проверки статуса оплаты заказа отправить POST запрос на адрес  
`https://gateway.chocodev.kz/orders/v1/preorder/status`  
Headers:  
`Content-Type: x-application/x-www-form-urlencoded`  
со следующими данными:  

Ключ | Описание 
--- | --- 
merchant_order_ids[] | Массив ваших ID заказов для проверки статуса **required** 
is_extended | 1 (если необходимы доп.данные)

### Ответ
```
{
    "error_code": 0,
    "status": "success",
    "message": "Статусы заказов",
    "data": {
        "100500": true,
        "100501": false
    }
}
```

### Ответ с доп.данными
```
{
    "error_code": 0,
    "status": "success",
    "message": "Статусы заказов",
    "data": {
        "200": {
            "is_paid": true,
            "amount": 3000,
            "cashback": 300,
            "refund": {
                "refunded_amount": 1500,
                "refunded_cashback": 150
            }
        }
    }
}
```
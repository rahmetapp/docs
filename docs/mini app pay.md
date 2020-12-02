## Оплата 
- Создать заказ через наш метод [здесь](https://github.com/ulan61/docs/blob/master/docs/order.md) 
- Полученный url из ответа отправить в метод RahmetApp.pay(url), который определен в нативном приложении.
- И дождаться ответа в методах(которые определены в Mini App):
    - *RahmetWebApp.onPaySuccess()*, при успешной оплате;
    - *RahmetWebApp.onNativePayViewClosed()*, при отмене оплаты;

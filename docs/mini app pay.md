### Оплата производится через приложение. Вам лишь необходимо выполнить следующие шаги: 
1) Создать заказ через наш метод [здесь](https://github.com/ulan61/docs/blob/master/docs/order.md) 
2) Полученный url из ответа отправить в метод RahmetApp.pay(url) определенный в User Script.
3) И дождаться ответов в методах(которые определяются у Вас):
    - RahmetWebApp.onPaySuccess(), при успешной оплате;
    - RahmetWebApp.onNativePayViewClosed(), при отмене оплаты;
### Документация по интеграции Mini App в Рахмет

Добро пожаловать в документацию по интеграции Mini App. Mini App - это интеграция стороннего проекта/сервиса внутри приложения Rahmet с помощью webView. Это реализовано через js message handlers и работает так: webview iOS/Android вызывает функции JS (*RahmetWebApp.onPaySuccess()*), а JS - нативные методы(*RahmetApp.pay(url)*). Со стороны Mini app нужно определить методы RahmetWebApp, чтоб нативное приложение могло вызывать их. А также нужно делать проверку на доступность функции RahmetApp, потому что ее может не быть (например, Реферальная программа доступна с версии 3.7.1).
На данный момент доступны следующие интеграции(авторизация и оплата обязательны): 

- [**Бесшовная авторизация**](https://github.com/ulan61/docs/blob/master/docs/mini%20app%20auth.md)
- [**Оплата**](https://github.com/ulan61/docs/blob/master/docs/mini%20app%20pay.md)
- [**Реферальная программа**](https://github.com/ulan61/docs/blob/master/docs/mini%20app%20referral%20program.md)
- [**Haptic Touch**](https://github.com/ulan61/docs/blob/master/docs/mini%20app%20haptic.md)

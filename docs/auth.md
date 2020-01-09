## Токен авторизации

Для работы с методами Rahmet Pay требуется токен, который выдается после авторизации.  
Токен авторизации валиден 10800 секунд (3 часа). Вы можете сохранить его или же инициировать авторизацию при каждом запросе.  

Во всех методах в заголовках необходимо отправлять полученный токен  
**Authorization: Bearer TOKEN**

## Запрос и пример

Для авторизации необходимо выполнить вызов метода  
`https://gateway.chocodev.kz/auth/token`  
(в заголовке не забываем [Content-Type](/#_3))

Значения для параметров (ID, Secret) мы выдадим заранее.

Параметры запроса:

Ключ | Описание | Примечание
--- | --- | ---
client_id | ID клиента | Обязательное
client_secret | Секретный ключ клиента | Обязательное
grant_type | Тип авторизации | Постоянное значение: `client_credentials`

Пример запроса (данные для авторизации в тестовом окружении): 
```
client_id: 12697011
client_secret: 7k4fv685jckshj5wljplsot707olo2x9sn58uba6l8djhomu4sk92y5xaurd66q8
grant_type: client_credentials
```
## Ответ

В ответ сервер возвращает JSON с указанными [здесь](/#_4) составляющими.  

Два возможных варианта ответа: 
```
{
    "error_code": 4,
    "status": "error",
    "message": "Client authentication failed",
    "data": null
}
```
```
{
    "error_code": 0,
    "status": "success",
    "message": "Токен успешно создан",
    "data": {
        "token_type": "Bearer",
        "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6IjAzOGUyYjE5MjA0ZDZmMzZmMWFlNzBhZTZmODAwZTc5YjM3ZWQ1ZjRlZTA0OGRhYzk5NjUxZGYyYzMzODZjMjg0MDIyZGY4Zjk3MTkxYzc3In0.eyJhdWQiOiIxMjYxMDY3MiIsImp0aSI6IjAzOGUyYjE5MjA0ZDZmMzZmMWFlNzBhZTZmODAwZTc5YjM3ZWQ1ZjRlZTA0OGRhYzk5NjUxZGYyYzMzODZjMjg0MDIyZGY4Zjk3MTkxYzc3IiwiaWF0IjoxNTY4NzE3MzIyLCJuYmYiOjE1Njg3MTczMjIsImV4cCI6MTU2ODcyODEyMiwic3ViIjoiMTI2MTA2NzIiLCJzY29wZXMiOlsyMF19.cKHDxuMDJnme9Foh3xaXJ0Edg_0woVBDPHQSpyDxQDnvTC5TrlVT3q3mw8gZJn_yyJ8ldP6RxKyfIqWvpcTPgFOa818K6x9XYA64LjmLvMxDM9O1XSklJAOqiYVKUCLdSubK_Lj1RWejNLeSPn73WE4MfpOC1LRkktNAPCLudJfO0-UcoCOGyqnurimDw5wl0CXzf91-1AwlbzWddCJ6J_-9yl0GRuyUaEHw8zDGwbLF_4383lLcbvEB3y60T46C-afTvsUGVPB0KaOmMxZAr1jAXPfEki7d5bPdojhm1iHjdR4ur_fLNjLrshPFgWtGPqKTJxNPFoA0iWswF2F-Dw",
        "expire_in": 10800
    }
}
```
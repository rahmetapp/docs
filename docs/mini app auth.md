## Авторизация

### Пользователь авторизован в Рахмете. 
- В этом случае в url передается query "track_id", c помощью которого нужно сделать запрос на gateway "auth/token" с полями в хедере: 
    - *client_id* (выдается заранее)
    - *client_secret* (выдается заранее)
    - *track_id* 
    - *grant_type* (= authorization_track_id)

- В теле ответа получаете token, который будет необходим в дальнейшем, для обращения к gateway:
    ```json
    {
      "error_code": 0,
      "message": "string",
      "status": "string",
      "data": {
        "token_type": "string",
        "token": "string",
        "refresh_token": "string",
        "expire_in": 0
      }
    }
    ```
- Также в query url передается device_id и session_id. Это обычные uuid с той лишь разницей, что device_id хранится в памяти приложения, а session_id пока пользователь находится в мини апп. 
### Пользователь неавторизован в Рахмете. 
- В этом случае в *url* не передается *track_id*, но передаются *device_id* и *session_id*. Для получения *track_id* нужно вызвать метод *RahmetApp.authorize()*, который определен в *User Script*. 
- Ответ придет в *RahmetWebApp.onAuthSuccess(track_id)*. Дальнейшие действия такие же, как и у авторизовнного пользователя. 

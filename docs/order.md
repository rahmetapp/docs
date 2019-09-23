## Запрос и пример

Для создания заказа необходимо выполнить вызов метода  
`https://gateway.chocodev.kz/orders/v1/preorder/create`  
(в заголовке не забываем [Content-Type](/#_3) и [токен](/auth))  

Параметры запроса:

Ключ | Описание | Примечание
--- | --- | ---
merchant_order_id | ID заказа в вашей системе | Обязательное
amount | Сумма заказа | Обязательное
token | Токен филиала | hash, выдается нами
backlink<sup>1</sup> | DeepLink приложения, на которое мы отправим пользователя | Необязательное
postlink<sup>2</sup> | Ссылка для оповещения после успешной оплаты | Необязательное
failed_postlink<sup>3</sup> | Ссылка для оповещения случае ошибки оплаты | Необязательное
image_size<sup>4</sup> | Размер картинки | Необязательное
timeout | Срок оплаты заказа (в секундах) | Необязательное

- <sup>1</sup> После успешной оплаты заказа, мы отправим пользователя по этому DeepLink. Это может быть ваше приложение или веб-сайт со страницей "Спасибо за заказ" или дальнейшими инструкциями.
- <sup>2</sup> После успешной оплаты, мы оповестим вашу систему по этой ссылке GET-запросом.
- <sup>3</sup> В случае ошибки в процессе оплаты, мы оповестим вашу систему по этой ссылке GET-запросом.
- <sup>4</sup> Размер картинки QR-кода в пикселях, в случае если у вас нет возможности сгенерировать QR. Вернем Base64 PNG Image

Пример запроса: 
```
merchant_order_id: 123543
amount: 1000
token: YOUR_FILIAL_TOKEN
backlink: http://project.kz/rahmet/pay/123543/thankyou
postlink: http://project.kz/rahmet/pay/123543/true
failed_postlink: http://project.kz/rahmet/pay/123543/false
image_size: 300
timeout: 10000
```

### Ответ и пример

В ответ сервер возвращает JSON с указанными [здесь](/#_4) составляющими.  

Пример ответа: 
```
{
    "error_code": 0,
    "status": "success",
    "message": "Заказ создан",
    "data": {
        "preorder_id":      111,
        "url":              "https://rahmetapp.kz/?id=HASH",
        "qr_image_base_64": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAASwAAAEsCAIAAAD2HxkiAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAFLElEQVR4nO3dS2okMRBAwbHx/Y9s5gLDWBihl6qKWDdd30dtEunjz4t9f3//+JvPz89Rx1r5nxW7jnXyf57qvVcOQ4gQYiKEmAghJkKIiRBiIoSYCCEmQoiJEGIihNjXyo92zSuedHIWcdf9uXHG8uS78dT3cNYThRcSIcRECDERQkyEEBMhxEQIMRFCTIQQEyHERAixpdnRFTfOau461lPX3jy55uouN76Hs546vJAIISZCiIkQYiKEmAghJkKIiRBiIoSYCCEmQohtmx19sxv3o19x47zrjdxBiIkQYiKEmAghJkKIiRBiIoSYCCEmQoiJEGIihJjZ0R9Mm/lcOdbJmc8b95GfxpcQYiKEmAghJkKIiRBiIoSYCCEmQoiJEGIihJgIIbZtdvTNM4Qn50tXTDufk268Ll9CiIkQYiKEmAghJkKIiRBiIoSYCCEmQoiJEGIihNjS7Kh9yf/v5J71T/2fFU99D595VXAREUJMhBATIcRECDERQkyEEBMhxEQIMRFCTIQQ+7pxncanunG90F3nM+26TvIlhJgIISZCiIkQYiKEmAghJkKIiRBiIoSYCCEmQoh9nDzYtPUnd62refJYJ2csT65NetK093DW3YEXEiHERAgxEUJMhBATIcRECDERQkyEEBMhxEQIsaV1R7fNyB2cjZy2b/tJJ89n2j28ckb32JGAfxIhxEQIMRFCTIQQEyHERAgxEUJMhBATIcRECLGj647uMm2ec9o6ljfOau5y47X7EkJMhBATIcRECDERQkyEEBMhxEQIMRFCTIQQEyHEltYdnWbaupEnnVyX9aSnns/SfOmWIwG/JkKIiRBiIoSYCCEmQoiJEGIihJgIISZCiIkQYh/TZvZO7oF+45qZu0y7rqfOA1t3FC4gQoiJEGIihJgIISZCiIkQYiKEmAghJkKIiRBiXys/mjbPuWLafOmb97XfZdp86a77M+suwwuJEGIihJgIISZCiIkQYiKEmAghJkKIiRBiIoTYx64/unEWccW0WcRp57PLjde1652/rwp4GBFCTIQQEyHERAgxEUJMhBATIcRECDERQkyEENu2Z701PM+Ydp9vfF4rjj7TY0cC/kmEEBMhxEQIMRFCTIQQEyHERAgxEUJMhBATIcS2rTu6YtqM5S7TZiOfugbsLuPmpXecDPB7IoSYCCEmQoiJEGIihJgIISZCiIkQYiKEmAghtm3d0aeaNoN648zntJnhaedz3xOFhxEhxEQIMRFCTIQQEyHERAgxEUJMhBATIcRECLGvG2cRd1mZIXzq/u+77Hp/brz2Xd5bIAwhQoiJEGIihJgIISZCiIkQYiKEmAghJkKIiRBiXys/unFm7+RM4y7T5lRPuvEdW2HPeriACCEmQoiJEGIihJgIISZCiIkQYiKEmAghJkKIfaz8aNos4o1reE47nxXT5kt32XWft80nb/kX4NdECDERQkyEEBMhxEQIMRFCTIQQEyHERAgxEUJsad1Rzji5puiu+clp53Nyvdld1+5LCDERQkyEEBMhxEQIMRFCTIQQEyHERAgxEUJMhBAzO/qDXTOE2+YML5yN3OWp1+5LCDERQkyEEBMhxEQIMRFCTIQQEyHERAgxEUJMhBDbNjs6bb/1k6bNl06b+Vxx8nxOrrm6YtaTgBcSIcRECDERQkyEEBMhxEQIMRFCTIQQEyHERAixpdnRaXOGN5p2D0/O+t64r/3JY816M+CFRAgxEUJMhBATIcRECDERQkyEEBMhxEQIMRFC7C9/2YhD8YM5vwAAAABJRU5ErkJggg==""
    }
}
```
- Если интегрируете Rahmet Pay в веб-сайт, то показываете пользователю QR-код
- Если интегрируете Rahmet Pay в мобильное приложение, то оформляете кнопку со ссылкой.


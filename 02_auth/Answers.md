## Задание аутентификация по сертификатам X.509

### Решение задания

Для выполнения задания пришлите документы:

1. Файлы ca.crt, client.pfx и пароль для импорта, server.crt.  
[ca.crt](keys/ca.crt)  
[client.pfx](keys/client.pfx)  
[server.crt](keys/server.crt)  
`Пароль: 12345`  

2. Скриншот страницы с информацией о сертификате.  
![](pic/certificate_info.png)  

## Задание «Аутентификация»

### Решение задания

В качестве результата пришлите информацию:

1. В каком хранилище и какие данные хранятся после аутентификации, хранится ли что-то ещё помимо токена аутентификации.  
Данные хранятся в Session Storage
![](pic/session_storage_info.png)  

2. В какой части запроса и в каком виде отправляется токен доступа.  
Заголовках запроса в виде JWT  
`Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJsb2dpbiI6InZhc3lhIn0.JmhHh8NXwfqktXSFbzkPohUb90gnc3yZ9tiXa0uUpRY`  
![](pic/jwt_info.png)  
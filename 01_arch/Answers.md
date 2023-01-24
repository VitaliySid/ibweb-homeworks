### Карта взаимодействия

```text
1. Client --> Server 1 (запрос):

PUT http://localhost:9001/users
Content-Type: application/x-www-form-urlencoded

login=user&password=111111

2. Server 1 --> Client (ответ):

HTTP/1.1 200 OK
Content-Type: application/json


{
  "token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjIsImxvZ2luIjoidXNlciIsInJvbGVzIjpbIlVTRVIiXSwiaWF0IjoxNjc0NTQ1NTM4LCJleHAiOjE2NzQ1NDkxMzh9.Z-HPcu9iOOChW01YCPHF5jACjv7YWHa4vB-1hl4PrYOfcwsjaLwbtw-h6ETYaHXAIx-LsZ8ko1yIJmUDTgPMjcorUturk0cgXCYXttASoL5C6dlwKJ4UKVmxww4LA6b392nnJx-Hj4XixbGmjA3wRMVzpoP5u_4yeqdByiY7wnExisqdMHOucaPWkkQPxgxC_cCpy_gn04gj1zWEYtpW9lmPP9dQA4PGf5IqrDIAjgdlHsBnN9NBw4v1Fy_FZJINvKrTX7BUYCNk8zyKstL0DyLHhFAGC3SLyFVE6Uzw6kw48hz0txAKHm4M2B4DjXwe-bKFFnwoVrtpJywe4tgQVg"
}

3. Client --> Server 2 (запрос):

GET http://localhost:9002/api/transactions
Authorization: eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjIsImxvZ2luIjoidXNlciIsInJvbGVzIjpbIlVTRVIiXSwiaWF0IjoxNjc0NTQ1NTM4LCJleHAiOjE2NzQ1NDkxMzh9.Z-HPcu9iOOChW01YCPHF5jACjv7YWHa4vB-1hl4PrYOfcwsjaLwbtw-h6ETYaHXAIx-LsZ8ko1yIJmUDTgPMjcorUturk0cgXCYXttASoL5C6dlwKJ4UKVmxww4LA6b392nnJx-Hj4XixbGmjA3wRMVzpoP5u_4yeqdByiY7wnExisqdMHOucaPWkkQPxgxC_cCpy_gn04gj1zWEYtpW9lmPP9dQA4PGf5IqrDIAjgdlHsBnN9NBw4v1Fy_FZJINvKrTX7BUYCNk8zyKstL0DyLHhFAGC3SLyFVE6Uzw6kw48hz0txAKHm4M2B4DjXwe-bKFFnwoVrtpJywe4tgQVg

4. Server 2 --> Server 3 (запрос):

GET http://localhost:9003/api/transactions
X-Userid: 2

5. Server 3 --> Server 4 (запрос):

GET http://localhost:9003/api/transactions
X-Userid: 2

6. Server 4 --> Server 3 (ответ):
HTTP/1.1 200 OK
Content-Type: application/json
Date: Tue, 24 Jan 2023 07:57:28 GMT
Content-Length: 291


[
  {
    "id": 1,
    "userId": 2,
    "category": "auto",
    "amount": 1000000,
    "created": 1674547039
  },
  {
    "id": 2,
    "userId": 2,
    "category": "auto",
    "amount": 100000,
    "created": 1674547039
  },
  {
    "id": 3,
    "userId": 2,
    "category": "food",
    "amount": 100000,
    "created": 1674547039
  }
]

7. Server 3 --> Server 2 (ответ):
HTTP/1.1 200 OK
Content-Type: application/json
Date: Tue, 24 Jan 2023 07:57:28 GMT
Content-Length: 291


{
  "transactions": [
    {
      "id": 1,
      "userId": 2,
      "category": "auto",
      "amount": 1000000,
      "created": 1674547039
    },
    {
      "id": 2,
      "userId": 2,
      "category": "auto",
      "amount": 100000,
      "created": 1674547039
    },
    {
      "id": 3,
      "userId": 2,
      "category": "food",
      "amount": 100000,
      "created": 1674547039
    }
  ],
  "categoryStats": {
    "auto": 1100000,
    "food": 100000
  }
}

8. Server 2 --> Client (ответ):
HTTP/1.1 200 OK
Content-Type: application/json
Date: Tue, 24 Jan 2023 07:57:28 GMT
Content-Length: 291


{
  "transactions": [
    {
      "id": 1,
      "userId": 2,
      "category": "auto",
      "amount": 1000000,
      "created": 1674547039
    },
    {
      "id": 2,
      "userId": 2,
      "category": "auto",
      "amount": 100000,
      "created": 1674547039
    },
    {
      "id": 3,
      "userId": 2,
      "category": "food",
      "amount": 100000,
      "created": 1674547039
    }
  ],
  "categoryStats": {
    "auto": 1100000,
    "food": 100000
  }
}

```

## Задание «Токен»
### Решение задания

В качестве решения пришлите информацию:
1. Для чего и на каком этапе используется, если используется, каждый ключ из каталога `keys1`.  
По идее использует Server 1 при генерации JWT-токена.
{
  "alg": "RS256",
  "typ": "JWT"
}.
{
  "userId": 2,
  "login": "user",
  "roles": [
    "USER"
  ],
  "iat": 1674545538,
  "exp": 1674549138
}.SIGNATURE
  
2. Для чего и на каком этапе используется, если используется, ключ из каталога `keys2`.  
Использует сервер 2 при проверке JWT-токена.

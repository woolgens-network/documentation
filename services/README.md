# Microservice Web API documention

## Auth Service

### POST `/login/basic`

Request:
```js
{
  userName: string,
  password: string,
  tokenLifetime: "DAY" | "WEEK" | "MONTH",
}
```
Response:
```js
{
  user: WebUser,
  token: string,
}
```

### POST `/login/token`

Request:
```js
{
  token: string,
}
```
Response:
```js
{
  user: WebUser,
}
```

## User Service

### GET `/users`

Query parameters:
```js
?sorted=stats.playtime // switch to database variable
```

Response:
```js
MinecraftUser[]
```

### GET `/users/{uuid}`

Response:
```js
MinecraftUser
```

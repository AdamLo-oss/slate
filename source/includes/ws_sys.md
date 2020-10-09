# 系统接口

## 发送心跳

>请求:

```json
{
    "method":"server.ping",
    "params":[],
    "id":100
}
```

>响应:

```json
{
    "error":null,
    "result":"pong",
    "id":100
}
```

- method: server.ping
- params: []

### 请求参数
无

### 响应数据
无



## 获取系统时间

>请求:

```json
{
    "method":"server.time",
    "params":[],
    "id":100
}
```

>响应:

```json
{
    "error":null,
    "result":1511941406,
    "id":100
}
```

- method: system.time
- params: []

### 请求参数
无

### 响应数据
服务器时间




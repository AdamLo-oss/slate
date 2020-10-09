# System Interface

## Send Heartbeat

>Request:

```json
{
    "method":"server.ping",
    "params":[],
    "id":100
}
```

>Response:

```json
{
    "error":null,
    "result":"pong",
    "id":100
}
```

- method: server.ping
- params: []

### Request Parameter
No

### Response Data
No



## Retrieve System Time

>Request:

```json
{
    "method":"server.time",
    "params":[],
    "id":100
}
```

>Response:

```json
{
    "error":null,
    "result":1511941406,
    "id":100
}
```

- method: system.time
- params: []

### Request Parameter
No

### Response Data
Server Time



## User Verification

>Request:

```json
{
    "method":"server.auth",
    "params":[api_key,sign],
    "id":100
}
```

>Response:

```json
{
    "error": null,
    "result": {
        "status": "success"
    },
    "id": 100
}
```


- method: server.auth
- params: 

### Request Parameter

| Name of Parameter  | Type of Parameter | Required | Description        |
| ------- | -------- | ---- | ----------- |
| api_key | String   | Yes   | User's api_key |
| sign    | String   | Yes   | Signature Value      |


### Response Data
Successful or not 


---
title: "ListUser"
description: 'list users'
---调用该接口list users。



## Request


```
get \tenants\{tenant_id}\users
```

| Name | Located in | Type | Description | 
| ---- | ---------- | ----------- | ----------- | 
| tenant_id | path | string |  |  

###  Request Parameters

| Name | Located in | Type | Description |  Required |
| ---- | ---------- | ----------- | ----------- |  ---- |
| page_num | query | integer |  |  false |
| page_size | query | integer |  |  false |
| order_by | query | string |  |  false |
| is_descending | query | boolean |  |  false |
| key_words | query | string |  |  false |

## Response

### Response  200 
| Code2 | Description | Type | Schema |
| ---- | ----------- | ------ | ------ |
| 200 | OK | Object | [v1ListUserResponse](#v1ListUserResponse) |

#### v1ListUserResponse

| Name | Type | Description | 
| ---- | ---- | ----------- |     
| page_num | integer |  |      
| page_size | integer |  |      
| total | integer |  |          
| users | Array[v1UserListData] |  [ 具体参数可见下面 [v1UserListData](#v1UserListData) ] |    

### v1UserListData
| Name | Type | Description | 
| ---- | ---- | ----------- |     
| avatar | string |  |      
| create_at | string |  |      
| email | string |  |      
| external_id | string |  |      
| nick_name | string |  |         
| roles | Array[ string ] |  |       
| tenant_id | string |  |      
| user_id | string |  |      
| username | string |  |   



### Response  default 
| Code2 | Description | Type | Schema |
| ---- | ----------- | ------ | ------ |
| default | An unexpected error response. | Object | [rpcStatus](#rpcStatus) |

#### rpcStatus

| Name | Type | Description | 
| ---- | ---- | ----------- |     
| code | integer |  |          
| details | Array[protobufAny] |  [ 具体参数可见下面 [protobufAny](#protobufAny) ] |       
| message | string |  |   

### protobufAny
| Name | Type | Description | 
| ---- | ---- | ----------- |     
| @type | string |  |   




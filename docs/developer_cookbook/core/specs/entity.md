---
title: 实体
sidebar_position: 1
---

## 实体（Entity）

> 物联网世界里的操作对象，以及这些对象组合抽象出来的对象，包括网关，设备，设备的聚合抽象等等。


## 组成

实体（Entity）由两部分组成：
- 实体的属性，用于描述实体的各种指标。
- 实体的属性配置信息，用于定义实体的属性。

属性具有 **固定** 且 **必须** 的字段，也有 *可选* 的字段，属性以 Key-Value 的形式存在，以提供良好的扩展性。

- 实体具有零个或多个属性。
- 实体属性的类型可以是 *任意类型*，满足 `json` 规范 。
- 实体 **必须** 具有如下字段：

    |名称|类型|描述|
    |---|----|---|
    |id|string|实体的id，用于唯一标识实体。|
    |type|string|实体的类型，用于实体分类，诸如设备，空间等。|
    |owner|string|实体的拥有者ID。|
    |source|string|创建实体的插件名称。|
    |version|int64|实体的版本号。|
    |last_time|int64|实体的最近修改时间。|



```bash
# Example
{
    "id": "device123",
    "source": "dm",
    "owner": "admin",
    "type": "DEVICE",
    "configs": {
        "temp": {
            "define": {
                "max": 500,
                "min": 10,
                "unit": "°"
            },
            "description": "",
            "enabled": true,
            "enabled_search": false,
            "enabled_time_series": false,
            "id": "temp",
            "last_time": 0,
            "type": "int",
            "weight": 0
        }
    },
    "properties": {
        "status": "end",
        "temp": 20
    }
}
```



## 实体的两种存在形式

实体是对物联网世界中的操作对象的数字化抽象，我们不仅抽象其状态，也对其行为进行抽象。所以我们为实体创建 `状态存储` 和 `运行时Actor`，用于现物理世界中`对象`的`状态`和`行为`。


## 实体的生命周期

实体的生命周期从用户创建，存在于状态存储，当有实体的消息到达，实体被加载到内存，执行收到的消息，当消息执行完成，再无消息可执行则从 `runtime` 卸载实体。当用户删除实体，实体则从状态存储，Runtime，搜索引擎删除。

![entity-life-cycle](/images/core/entity=life-cycle.png)

## 实体状态的存储

实体的状态数据，即实体的属性数据，我们根据需求将其选择性的存储到状态存储，时序存储 和 搜索引擎。

实体状态数据的持久化具有两方面特征：选择性，策略性。

- 选择性是指用户可以对实体的属性进行配置，来指定所配置的属性是否进行持久化，[详情请查看](model.md)。
- 策略性是指用户可以根据对服务节点配置信息进行调节，来控制实体数据的[持久化策略](persistent-strategy.md)。




## 平铺实体属性

`id, type, owner, source` 等字段也可以看做实体的必须属性字段，是被 Core 保留的，用于描述实体，用户不能重新定义。


故，实体可以存在两种展示形式：

**Structured:**

```json
{
    "id": "device123",
    "source": "dm",
    "owner": "admin",
    "type": "DEVICE",
    "configs": {
        "temp": {
            "define": {
                "max": 500,
                "min": 10,
                "unit": "°"
            },
            "description": "",
            "enabled": true,
            "enabled_search": false,
            "enabled_time_series": false,
            "id": "temp",
            "last_time": 0,
            "type": "int",
            "weight": 0
        }
    },
    "properties": {
        "status": "end",
        "temp": 20
    }
}
```

**Tiled：**

```json
{
    "id": "device123",
    "source": "dm",
    "owner": "admin",
    "type": "DEVICE",
    "configs": {
        "temp": {
            "define": {
                "max": 500,
                "min": 10,
                "unit": "°"
            },
            "description": "",
            "enabled": true,
            "enabled_search": false,
            "enabled_time_series": false,
            "id": "temp",
            "last_time": 0,
            "type": "int",
            "weight": 0
        }
    },
    "status": "end",
    "temp": 20
}
```




### 实体保留字段


|名称|类型|描述|
|---|----|---|
|id|string|实体的id，用于唯一标识实体。|
|type|string|实体的类型，用于实体分类，诸如设备，空间等。|
|owner|string|实体的拥有者ID。|
|source|string|创建实体的插件名称。|
|version|int64|实体的版本号。|
|last_time|int64|实体的最近修改时间。|
|template|string|标识实体的模板ID|
|properties|object|用于结构化展示实体属性。|
|configs|object|用于展示实体属性定义信息。|
|config_file|string| 用于存储实体属性定义。|
|mappers|object|用于展示实体的映射。|



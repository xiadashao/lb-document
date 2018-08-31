### 统一约定

* 后端返回数据统一为json格式。

* http请求头参数 `Content-Type: application/x-www-form-urlencoded`

* http响应头参数 `Content-Type: application/json; charset=utf-8`

### 请求方法

* `get`查询获取资源        参数传递拼接在url后面

* `post`新增、更新          参数传递放在body

* `delete`删除资源          参数传递同get

### 响应结果

##### 1. 组成

status 响应状态

code 响应码

message 响应信息

data 业务数据

##### 2. 示例

成功响应-单条数据

```
{
    "status":1

    "code" :0,

    "message":"",

    "data":{

        "id":1,

        "name":"test",

        "age":22

    }
}
```

成功响应-多条数据

```
{
    "status":1

    "code" :0,

    "message":"",

    data:[

        {

            "id":1,

            "name":"test",

            "age":22

        },{

            "id":2,

            "name":"test2",

            "age":22

        }

    ]
}
```

成功响应-分页数据

```
{
    "status":1

    "code" :0,

    "message":"",

    "data":{

        "total": 2, 

        "pageNum": 1, 

        "pageSize": 10, 

        "list": [ 

            { "id": 1, "name": "test", "age": 22 },

            { "id": 2, "name": "test2", "code": 22 } 

        ], 

        "totalPage": 1

    }
}
```

total: 总记录数

pageNum: 当前页码

pageSize: 每页大小

totalPage: 总页数

失败响应：

```
{
    "code" :-1000,

    "message":"未找到数据",

    "data":{}
}
```

返回状态status===1表请求成功，code返回0，message返回"";

返回状态status===0表请求失败，code返回错误码，message返回详细的错误信息；

多条数据和分页数据返回数据条数为0时，返回\[\]；

##### 3.特殊数据（暂时这些，开发中遇到进行补充）

下拉框，单选，多选         获取数据由后台提供默认选中标识

日期        JSON数据传输中一律使用字符串，具体日期格式因业务而定

Boolean类型     JSON数据传输中一律使用1/0来标示，1为是/True，0为否/False


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

code 响应码    自定义码表

message 响应信息    自定义码表

data 业务数据

##### 2. 示例

成功响应-单条数据

```
{
    code :”00000000”,

    message:”操作成功”,

    data:{

        id:1,

        name:test,

        age:22

    }
}
```

成功响应-多条数据

```
{
    code :”00000000”,

    message:”操作成功”,

    data:[

        {

            id:1,

            name:test,

            age:22

        },{

            id:2,

            name:test2,

            age:22

        }

    ]
}
```

成功响应-分页数据

```
{
    code :”00000000”,

    message:”操作成功”,

    data:{

        totalCount: 2, 

        pageNo: 1, 

        pageSize: 10, 

        list: [ 

            { id: 1, name: "test", age: 22 },

            { id: 2, name: "test2", code: 22 } 

        ], 

        totalPage: 1

    }
}
```

totalCount: 总记录数

pageNo: 当前页码

pageSize: 每页大小

totalPage: 总页数

失败响应：

```
{
    code :”01020300”,

    message:”未找到数据。”,

    data:{}
}
```

##### 3.特殊数据（暂时这些，开发中遇到进行补充）

下拉框，单选，多选         获取数据由后台提供默认选中标识

日期        JSON数据传输中一律使用字符串，具体日期格式因业务而定

Boolean类型     JSON数据传输中一律使用1/0来标示，1为是/True，0为否/False

### 码表

暂定8位字符，“00000000”标识成功，其余根据各业务进行自定义

00  00   0000，响应码可以按照223的标准（初步），进行分配、定义

例如：订单服务 01，下单模块02，参数异常0003；组合起来返回错误码是01020003

各个服务可以根据自己的需求进行自定义状态码，最后汇总成对外提供的码表。


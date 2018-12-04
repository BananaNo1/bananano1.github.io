---
title: Swagger注解
date: 2018-12-04 09:50:10
tags: [记录]
categories: Swagger
---

####  注解详解

 1. @Api() : 用于类(controller)；标识这个类是swagger的资源  

    ```
    tags: 表示说明,设置这个值、value的值会被覆盖
    value: url的路径值
    description: 对api资源的描述
    ```

	2. @ApiOperation() :用于方法(controller里面的方法);

    ```
    value:url的路径值
    tags:设置这个值，value的值会被覆盖
    description：对该方法的描述
    ```

	3. @ApiParame:属性描述，用于解释方法中的参数

    ```
    name:属性名称
    value：属性值
    required:是否属性必填
    hidden:隐藏该属性
    ```

	4. @ApiResponse:请求返回信息描述,用于controller方法之上

    ```
    code: 请求返回的状态码（http请求码）
    message：信息描述
    ```

	5. @ApiModel() : 用于返回对象类上,对类进行说明；描述返回对象的意义

	6. @ApiModelProperty: 描述一个model的属性。 
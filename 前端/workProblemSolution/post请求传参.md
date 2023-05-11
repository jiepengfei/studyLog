

payload面板
类型为request payload,展开类似js对象结构
使用request.body

类型为Form Data
参数聚成一坨,类似JSON.stringify后的产物
使用request.post



类型为Query String Parameters

这类是属于get请求,在请求url路径后面的查询参数

如果post请求需要Query String Parameters

可以在请求url路径中像get请求一样携带查询参数



一般不需要设置request head
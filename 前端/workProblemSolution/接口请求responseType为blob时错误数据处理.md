





```js
axios({
  method: 请求方式,
  url: 接口路径,
  data: 接口参数,
  dataType: 'json',
  responseType: 'blob',
  headers: {
    // 项目中请求头需要的信息（如果不需要可不写），如用户登录信息验证：
    authorization: localStorage.getItem('authorization')
  }
}).then(response => {
  // 方法一：
  try {
    const jsonData = JSON.parse(fileReader.result) // 说明是普通对象数据，后台转换失败
    // 后台信息
    console.log(jsonData)
  } catch (err) { // 解析成对象失败，说明是正常的文件流
    // 下载文件
    downloadFile(resData)
  }
  // 方法二：
    if (response.type === 'application/json') {
      const fileReader = new FileReader()
      fileReader.readAsText(response.data)
      fileReader.onload = () => {
        const jsonData = JSON.parse(fileReader.result)
        // 后台信息
        console.log(jsonData)
      }
    } else {
      // 下载文件
      downloadFile(response)
    }
}).catch(error => {
  ...
})
```


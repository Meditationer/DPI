# JS 将字符串转换成日期类型(Date)，与当前时间比较(数据库为datetime)

```html
 let start = new Date(Date.parse(startTime.replace(/-/g,"/")));//字符串为yyyy-MM-dd hh:mm:ss
 let end = new Date(Date.parse(endTime.replace(/-/g,"/")));
 let now = new Date();
    if(start<new Date() && new Date()<end)
	{}
```

## 字符串格式转换

```js
 var str = "yyyy-MM-dd HH:mm:ss";
 str = str.split(" ")[0]; // yyyy-MM-dd 格式固定的字符串
```
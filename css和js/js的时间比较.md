# JS 将字符串转换成日期类型(Date)，与当前时间比较(数据库为datetime)

```html
 let start = new Date(Date.parse(startTime.replace(/-/g,"/")));
 let end = new Date(Date.parse(endTime.replace(/-/g,"/")));
 let now = new Date();
    if(start<new Date() && new Date()<end)
	{}
```
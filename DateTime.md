**获取时间段的方式**

```c#
model.date = orderInfo[0].OrderDate.ToString("yyyy-MM-dd");
model.time = orderInfo[0].OrderDate.ToString("HH:mm:ss");
```

**获取一个月内的数据**

```c#
var order = DB.Queryable<NCLab_Order>().Where(it => it.UserId == userId && it.OrderDate >= DateTime.Now.AddDays(-30)).ToList();
```

  **设置时间格式**

~~~c#
var date = DateTime.Now;
date.ToString("yyyy-MM-dd HH:mm:ss")
~~~


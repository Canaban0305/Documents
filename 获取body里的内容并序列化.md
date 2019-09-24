# 获取body里的内容并序列化

获取body里的内容并序列化

~~~c#
using (var reader = new StreamReader(HttpContext.Request.Body, Encoding.UTF8))
{
	resultBody = reader.ReadToEnd();
}
var resultJson = JsonConvert.DeserializeObject<OpenDoorParameter>(resultBody);
~~~


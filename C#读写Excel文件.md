# C#读写Excel文件

### 1、上传文件到指定服务器文件夹

**前端**

```web-idl
<form method="post" enctype="multipart/form-data" action="/Home/FileUpload">
    <div>
        <input type="file" name="file" />
    </div>
    <div>
        <input type="submit" value="上传" />
    </div>
</form>
```

**后台**

```c#
[HttpPost]
public ActionResult FileUpload([FromForm(Name = "file")]IFormFile file)
{
	//获取当前执行应用程序的路径      path = E:\\An1\\Test\\RetailTest\\RetailTest
	var path = Directory.GetCurrentDirectory();
	var filePath = path + "\\Excel\\" + 							 			   		 	 file.FileName.Substring(file.FileName.LastIndexOf("\\") + 1);

	if (file.Length > 0)
	{
		using (var stream = new FileStream(filePath, FileMode.Create))
		{
			file.CopyTo(stream);        //复制
		}
	}
	return Content("succ");
}
```

### 2、导入

**前端**

~~~web-idl
<form method="post" enctype="multipart/form-data" action="/Home/ExcelToDataTable2">
    <div>
        <input type="file" name="file" />
    </div>
    <div>
        <input type="submit" value="上传" />
    </div>
</form>
~~~

**后台** =>	**引用：**using OfficeOpenXml;

~~~c#
/// <summary>  
/// 将excel导入到datatable  
/// </summary>  
/// <param name="file">excel路径</param>  
/// <returns>返回datatable</returns>  
public ActionResult ExcelToDataTable2([FromForm(Name = "file")]IFormFile file)
{
	//连接数据库
	SqlSugarClient db = new SqlSugarClient(new ConnectionConfig()
    {
    	ConnectionString = "Data Source=.;Initial Catalog=NopiSIM;Integrated Security=True",
        DbType = DbType.SqlServer,
        InitKeyType = InitKeyType.Attribute
   	    });

        //获取当前执行应用程序的路径      path = E:\\An1\\Test\\RetailTest\\RetailTest
        var path = Directory.GetCurrentDirectory();
        var filepath = path + "\\Excel\\" + file.FileName.Substring(file.FileName.LastIndexOf("\\") + 1);

        if (file.Length > 0)
        {
        	using (var stream = new FileStream(filepath, FileMode.Create))
            {
            	file.CopyTo(stream);        //复制到指定文件夹
            }
        }
        FileInfo filePath = new FileInfo(Path.Combine(filepath));       //格式化路径
        try
        {
        	using (ExcelPackage package = new ExcelPackage(filePath))   //打开文件
            {
            	StringBuilder sb = new StringBuilder();
                ExcelWorksheet worksheet = package.Workbook.Worksheets[0];   //获得的Excel中的第一张表  
                int rowCount = worksheet.Dimension.Rows;   //行数  
                int ColCount = worksheet.Dimension.Columns;  //列数  
                                                               
                //遍历Excel表并同时赋值到对象实体对象中  
                for (int i = 2; i <= rowCount; i++)
                {
                    //表格第一行是编号，编号为自增列，需要忽略，从第二列开始
                    int col = 2;
                    //声明实体对象并且进行赋值                     
                    NCLab_CommodityInfo commodity = new NCLab_CommodityInfo();
                    commodity.CommodityName = worksheet.Cells[i, col].Value.ToString();//2
                    commodity.CommodityWeight = Convert.ToInt32(worksheet.Cells[i, col+1].Value);//3
                    commodity.CommodityQuantity = Convert.ToInt32(worksheet.Cells[i, col+2].Value);//4
                    commodity.CommodityPrice = Convert.ToDecimal(worksheet.Cells[i, col+3].Value);//5
                    commodity.CabinetId = Convert.ToInt32(worksheet.Cells[i, col + 4].Value.ToString());//6
                    commodity.LayerId = Convert.ToInt32(worksheet.Cells[i, col+5].Value);//7
                    commodity.CommodityErrorRange = Convert.ToInt32(worksheet.Cells[i, col + 7].Value);//9
                    commodity.CommodityStatus = Convert.ToInt32(worksheet.Cells[i, col+6].Value);//8
                    //判断单元格是否为空不能使用ToString()
                    if(string.IsNullOrEmpty(worksheet.Cells[i, col + 8].Text))
                    {                   //为空则忽略
                        //插入数据库
                        int qq = db.Insertable<NCLab_CommodityInfo>(commodity).IgnoreColumns(it => new { it.Id, it.CommodityBrand }).ExecuteCommand();
                    }
                    else
                    {
                        //插入数据库
                        commodity.CommodityBrand = worksheet.Cells[i, col + 8].Value.ToString();
                        int rr = db.Insertable<NCLab_CommodityInfo>(commodity).IgnoreColumns(it => new { it.Id}).ExecuteCommand();
                    }
                           
                }
            }
            return Content("succ");
        }
        catch (Exception ex)
        {
            string message = ex.Message;
            return Content("fail");
        }
}
~~~

### 3、导出：

~~~c#
public FileResult ToFile()
{
    //连接查询数据库所需要的表的内容
    var list = db.Queryable<NCLab_CommodityInfo>().ToList();
    var sbHtml = new StringBuilder();
    sbHtml.Append("<table>");
    sbHtml.Append("<tr>");
    //表头对应名称
    var lstTitle = new List<string> { "编号", "名称", "重量", "数量", "价格","设备号", "层数", "状态", "误差", "品牌" };
    foreach (var item in lstTitle)
    {
    	sbHtml.AppendFormat("<td>{0}</td>", item);
    }
    sbHtml.Append("</tr>");

    //循环赋值
    for (int i = 0; i < list.Count; i++)
    {
    	sbHtml.Append("<t>");
    	sbHtml.AppendFormat("<td>{0}</td>", list[i].Id);
    	sbHtml.AppendFormat("<td>{0}</td>", list[i].CommodityName);
    	sbHtml.AppendFormat("<td>{0}</td>", list[i].CommodityWeight);
    	sbHtml.AppendFormat("<td>{0}</td>", list[i].CommodityQuantity);
    	sbHtml.AppendFormat("<td>{0}</td>", list[i].CommodityPrice);
    	sbHtml.AppendFormat("<td>{0}</td>", list[i].CabinetId);
    	sbHtml.AppendFormat("<td>{0}</td>", list[i].LayerId);
    	sbHtml.AppendFormat("<td>{0}</td>", list[i].CommodityStatus);
    	sbHtml.AppendFormat("<td>{0}</td>", list[i].CommodityErrorRange);
    	sbHtml.AppendFormat("<td>{0}</td>", list[i].CommodityBrand);
    	sbHtml.Append("</tr>");
    }
    byte[] fileContents = Encoding.Default.GetBytes(sbHtml.ToString());
    return File(fileContents, "application/ms-excel", "Commodify.xls");
}
~~~


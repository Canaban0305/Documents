# C#.Net Core解决跨域问题

#### 1、修改startup.cs中的ConfigureServices类

~~~C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
    services.AddCors(options =>
    {
        options.AddPolicy("any", builder =>
        {
            builder.AllowAnyOrigin()
            .AllowAnyMethod()
            .AllowAnyHeader();
            //.AllowCredentials();
        });
    });
}
~~~

#### 2、在Configure中添加Cors

~~~C#
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        // The default HSTS value is 30 days. You may want to change this for production scenarios, see https://aka.ms/aspnetcore-hsts.
        app.UseHsts();
    }
    app.UseCors("any");
    app.UseHttpsRedirection();
    app.UseMvc();
}
~~~

 <div style="color:red">注：app.UseCors("any")不能在app.UseMvc下方，否则不起跨域作用</div>


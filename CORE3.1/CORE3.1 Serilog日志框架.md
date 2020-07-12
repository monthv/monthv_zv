# CORE3.1 WebAPI Serilog日志框架

## 一、安装NuGet包：

- Serilog v2.9.0 
- Serilog..AspNetCore v3.2.0 

- Serilog.Sinks.Console v3.1.1 输出到控制台

- Serilog.Sinks.File v4.1.0 输出到文件


## 二、修改Program.cs文件

```c#
public static IHostBuilder CreateHostBuilder(string[] args) =>
            Host.CreateDefaultBuilder(args)
                .ConfigureWebHostDefaults(webBuilder =>
                {
                    webBuilder.UseStartup<Startup>();
                })
                .UseSerilog((context, configuration) =>
                {
                    var path = AppDomain.CurrentDomain.BaseDirectory;
                    path = path.Substring(0, path.LastIndexOf("bin") + 3);
                    configuration
                        .MinimumLevel.Debug()
                        .MinimumLevel.Override("Microsoft", LogEventLevel.Error)
                        .Enrich.FromLogContext()
                        .WriteTo.Console()
                        .WriteTo.File(path: Path.Combine(path, "log.log"), rollingInterval: RollingInterval.Day);          
                });//注入管道
```

## 三、在控制器打印日志

```c#
	[Route("[controller]")]
    [ApiController]
    public class SerilogController : ControllerBase
    {
        private readonly ILogger<SerilogController> _logger;
        public SerilogController(ILogger<SerilogController> logger)
        {
            _logger = logger;
        }
        [HttpGet]
        public void Name()
        {
            _logger.LogError("输出日志成功");
            var v = "你好";
            var vv = "世界";
            _logger.LogInformation("{0}{1}", v, vv);//占位符
            var v1 = "你好";
            var vv1 = 18;
            _logger.LogInformation("{0}{1}", v1, vv1>=18);//添加条件判断
            var model = new { Name = "你是谁", age = 14 };
            _logger.LogInformation("{@model}",model);//JSON格式打印日志
        }
```


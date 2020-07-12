# EFCore

## EFCore使用DBFirst

#### 1、安装NuGet包

- Microsoft.EntityFrameworkCore
- Microsoft.EntityFrameworkCore.SqlServer
- Microsoft.EntityFrameworkCore.Tools

#### 2、生成model

- 在项目中添加EFModel文件夹，打开NuGet控制台，输入命令：


- [Scaffold-DbContext]() "Data Source=ip地址;Initial Catalog=数据库名称;User ID=登录名;Password=登录密码" Microsoft.EntityFrameworkCore.SqlServer [-OutputDir]() EFModel

#### 3、数据库表的修改，同步更新Model时，命令加-Force 参数

- [Scaffold-DbContext]() "Data Source=ip地址;Initial Catalog=数据库名称;User ID=登录名;Password=登录密码" Microsoft.EntityFrameworkCore.SqlServer [-OutputDir]() EFModel [-Force]()

- 系统会自动生DbContext上下文及数据表实体